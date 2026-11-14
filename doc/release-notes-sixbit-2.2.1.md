# Sixbit Core 2.2.1 – own network ID and built-in seed

**For everyone on the Sixbit 2.2.0 chain** (the community fork with ASERT + StallGuard and merge-mining).
No rule change: same chain, same blocks, same balances. No resync needed.

**Switch-over: Saturday 21 November 2026, 12:00 UTC.** Please install 2.2.1 on that day (not
earlier – see "How to upgrade"). Shears Mining's public node and pools switch at the same time.

## Why

Since 12 November 2026 there are two Sixbit chains:

- **Sixbit 2.2.0** – the community fork announced on Bitcointalk (ASERT + StallGuard, AuxPoW).
- **Old rules (2.1.x)** – someone restarted mining on the original rules from the same block 34,082
  seven hours after 2.2.0 went live.

Both chains used the same network ID, so 2.2.0 nodes kept connecting to old-rules nodes, rejecting
their blocks and dropping them again ("unstable peers"). New wallets could also end up talking to the
wrong chain first.

## What changes

1. **Own network ID.** Sixbit 2.2.1 nodes use new network "magic bytes" (`e6 b1 7e d2`), so they only
   ever connect to other 2.2.1 nodes. They never see old-rules nodes again, and old-rules nodes never
   see them.
2. **Built-in seed.** The old `seed1/seed2.6bit.dev` seeds no longer work. 2.2.1 finds the network
   through Shears Mining's public node (`stratum.shears.co.uk:16666`) without any `addnode` line.

The P2P port stays **16666**. Consensus rules are exactly as in 2.2.0.

## What does not change

ASERT + StallGuard, the difficulty floor, AuxPoW (chain ID 6006), supply, reward, halvings,
addresses, wallets and balances.

## How to upgrade

On **21 November 2026 from 12:00 UTC**: back up your wallet (File > Backup Wallet), stop Sixbit,
replace the program files with the 2.2.1 ones and start it again. Your data folder and wallet are
used as they are.

2.2.1 and 2.2.0 nodes cannot talk to each other (that is the point of the new network ID), so a
2.2.1 node installed early will have no peers until the switch-over. If that happens, just wait.

## Moving coins safely between the two chains

Coins held before block 34,083 exist on **both** chains, and a transaction on one chain can be
copied ("replayed") onto the other. To make sure a payment only happens on the 2.2.x chain, include
a small amount of coin that only exists on this chain – for example, coin mined (or received from
an address that received coins mined) after block 34,083 – in the same transaction. Such a
transaction is invalid on the old-rules chain and cannot be replayed there. Exchanges should treat
deposits of pre-split coins with care.

## Credits

Sixbit by the original 6bit team. ASERT by Mark Lundeberg and Jonathan Toomim (Bitcoin Cash Node).
AuxPoW by the Namecoin developers. StallGuard and this release: Shears Mining, a community fork not
affiliated with the original team.
