# Sixbit Core 2.2.0 – community release

**A required upgrade (hard fork) at block 34,083.** Every node, wallet, pool and exchange must upgrade
before block 34,083 to stay on the Sixbit chain.

## Why

The Sixbit chain has been stuck at block 34,082 since 12 October 2026. A large miner pushed the
difficulty to 38.8 million and then left. Under Bitcoin's rule the difficulty only changes every
2,016 blocks, and the next change was 190 blocks away – weeks or months of mining for the miners who
were left. The original developers could not be reached, so this release was prepared by the
community (Shears Mining) and published openly, with full source.

## What changes from block 34,083

1. **ASERT with Shears StallGuard** replaces the 2,016-block retarget.
   - The switch-over block restarts at difficulty **~1,000,000**, so the chain can move again at once.
   - After that, every block's difficulty follows how long the previous block took (aserti3-2d
     maths from Bitcoin Cash, applied step by step), with a **2-hour half-life**.
   - **StallGuard:** if no block is found for **2 hours**, the next block may be easier – the
     difficulty halves for every further **30 minutes** of waiting. A big miner leaving can no
     longer freeze the chain.
   - **Floor:** the difficulty never drops below **~100,000**.
   - Block times may be at most **10 minutes** in the future (was 2 hours), so StallGuard cannot be
     triggered early with fake timestamps.
2. **AuxPoW (merge-mining).** Sixbit can be merge-mined alongside Bitcoin (chain ID **6006**), so
   Bitcoin miners can secure Sixbit at no extra cost. **Ordinary (solo) blocks remain valid.**
   New RPCs: `createauxblock` and `submitauxblock`.

## What does not change

Supply, block reward, halving schedule, 10-minute block target, addresses, transactions, wallets and
balances. All history up to block 34,082 is unchanged.

## Other fixes

- The default RPC address and RPC allow-list were set to `1.0.0.1` instead of `127.0.0.1`
  (localhost) by an earlier search-and-replace. This made the node fail to start its RPC server
  unless `rpcbind` was set, and wrongly allowed the `1.0.0.0/8` range. Restored to localhost, as in
  Bitcoin Core.

## Network

Nodes running 2.2.0 announce protocol version 70017. Older nodes will stop following the chain at
block 34,083.

## Testing

Tested on a private test chain: no change to the old rules before the switch-over; the switch-over
block restarts at the start difficulty; merge-mined blocks are accepted from the switch-over and
refused before it; ordinary blocks are still accepted; fast blocks raise the difficulty; StallGuard
eases after the delay as designed; the floor holds; merge-mined blocks are read back correctly
after a restart; `verifychain` passes. The full Sixbit history (blocks 0–34,082) re-validates with
this release.

## Credits

Sixbit was created by the original Sixbit (6bit) team – this release builds on their Sixbit Core 2.1.1,
and all credit for the coin is theirs. ASERT (aserti3-2d): Mark Lundeberg and Jonathan Toomim (Bitcoin
Cash Node). AuxPoW: Namecoin developers (Daniel Kraft et al.). StallGuard: Shears Mining. Built on
Bitcoin Core.
