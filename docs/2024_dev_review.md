# Osmosis 2024 Development Review

## Executive Summary (Non-Technical)
- January's v22 series tuned the fee market and raised performance ceilings so congestion eased while validators upgraded toolchains without drama [v22.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v22.0.0) [#7285](https://github.com/osmosis-labs/osmosis/pull/7285) [#7272](https://github.com/osmosis-labs/osmosis/pull/7272) [#7249](https://github.com/osmosis-labs/osmosis/pull/7249).
- Spring's v23 updates focused on reliability, landing IAVL v1 pruning support and mempool safeguards that kept upgrades rolling during the cross-chain incident response in March [v23.0.6 release](https://github.com/osmosis-labs/osmosis/releases/tag/v23.0.6) [#7582](https://github.com/osmosis-labs/osmosis/pull/7582) [#7716](https://github.com/osmosis-labs/osmosis/pull/7716) [#7769](https://github.com/osmosis-labs/osmosis/pull/7769).
- Mid-year v24 and v25 releases reworked ProtoRev revenue flows, introduced the Skip block-sdk auction, and hardened smart accounts so traders saw faster finality and clearer fee handling [v24.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v24.0.0) [v25.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v25.0.0) [#7555](https://github.com/osmosis-labs/osmosis/pull/7555) [#7935](https://github.com/osmosis-labs/osmosis/pull/7935) [#8125](https://github.com/osmosis-labs/osmosis/pull/8125).
- Year-end v26 through v28 aligned with Cosmos SDK 0.50, refreshed CosmWasm, and ratcheted down block times, setting the stage for 2025's pruning improvements [v26.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v26.0.0) [v27.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v27.0.0) [v28.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v28.0.0) [#8274](https://github.com/osmosis-labs/osmosis/pull/8274) [#8734](https://github.com/osmosis-labs/osmosis/pull/8734) [#8857](https://github.com/osmosis-labs/osmosis/pull/8857).

## Executive Summary (Technical)
- Fee market tuning lowered base fees, raised mempool gas caps, and synced EIP-1559 targets with consensus parameters, preventing spam from starving block space [#7285](https://github.com/osmosis-labs/osmosis/pull/7285) [#7270](https://github.com/osmosis-labs/osmosis/pull/7270) [#7291](https://github.com/osmosis-labs/osmosis/pull/7291).
- IAVL v1 adoption brought async pruning, cache invalidation fixes, and log-only failure paths so operators could recover without halting nodes [#7994](https://github.com/osmosis-labs/osmosis/pull/7994) [#7750](https://github.com/osmosis-labs/osmosis/pull/7750) [#7582](https://github.com/osmosis-labs/osmosis/pull/7582).
- The Skip block-sdk integration delivered top-of-block auctions, mempool bypass controls, and faster rechecks, while successive patches tightened timeouts and combated spam [#7935](https://github.com/osmosis-labs/osmosis/pull/7935) [#8409](https://github.com/osmosis-labs/osmosis/pull/8409) [#8455](https://github.com/osmosis-labs/osmosis/pull/8455).
- Smart account ergonomics improved with ledger support, additional auth events, and safer fee deductions, helping front-end wallet teams ship richer UX [#8581](https://github.com/osmosis-labs/osmosis/pull/8581) [#8494](https://github.com/osmosis-labs/osmosis/pull/8494) [#8125](https://github.com/osmosis-labs/osmosis/pull/8125).

## Detailed Changes by Release
### v22.0.0 - 12 Jan 2024
- Tuned the dynamic fee market, lowering default base fees while scaling the recheck factor to flush spam faster under load [#7285](https://github.com/osmosis-labs/osmosis/pull/7285).
- Registered consensus gas limits and raised per-tx caps so heavier swaps fit without relayer retries [#7220](https://github.com/osmosis-labs/osmosis/pull/7220) [#7291](https://github.com/osmosis-labs/osmosis/pull/7291).
- Upgraded to Go 1.21 and SDK forks that skip expensive denom lookups in each swap [#7272](https://github.com/osmosis-labs/osmosis/pull/7272) [#7282](https://github.com/osmosis-labs/osmosis/pull/7282).

### v22.0.1 - 20 Jan 2024
- Prevented heavy gRPC clients from forcing full app-hash recomputation, reducing live node stalls [#7346](https://github.com/osmosis-labs/osmosis/pull/7346).

### v22.0.3 - 2 Feb 2024
- Raised the arbitrage minimum gas price to align with new fee dynamics [#7368](https://github.com/osmosis-labs/osmosis/pull/7368).
- Removed an iterator from TWAP updates, trimming per-block compute [#7266](https://github.com/osmosis-labs/osmosis/pull/7266).

### v22.0.5 - 7 Feb 2024
- Added targeted logging to trace incentive truncation issues [#7395](https://github.com/osmosis-labs/osmosis/pull/7395).
- Batched intermediate account fetches and tightened TWAP pruning for lower epoch load [#7411](https://github.com/osmosis-labs/osmosis/pull/7411) [#7415](https://github.com/osmosis-labs/osmosis/pull/7415).

### v23.0.0 - 15 Feb 2024
- Updated CometBFT and IBC to relieve rate-limit regressions while exposing better error paths for staking and incentives [#7400](https://github.com/osmosis-labs/osmosis/pull/7400) [#7357](https://github.com/osmosis-labs/osmosis/pull/7357).
- Improved concentrated liquidity gauges by aligning uptime tracking with gauge durations [#7417](https://github.com/osmosis-labs/osmosis/pull/7417) [#7419](https://github.com/osmosis-labs/osmosis/pull/7419).
- Pruned TWAP records incrementally instead of in one epoch-sized burst [#7427](https://github.com/osmosis-labs/osmosis/pull/7427).

### v23.0.3 - 29 Feb 2024
- Enabled IAVL v1 and associated SDK fixes so pruning no longer ballooned disk usage [#7582](https://github.com/osmosis-labs/osmosis/pull/7582) [#537](https://github.com/osmosis-labs/cosmos-sdk/pull/537).
- Accelerated BigDec math, Protorev routes, and uptime accumulators to shrink swap latency [#7538](https://github.com/osmosis-labs/osmosis/pull/7538) [#7535](https://github.com/osmosis-labs/osmosis/pull/7535) [#7541](https://github.com/osmosis-labs/osmosis/pull/7541).
- Eliminated duplicate CometBFT block decoding to reduce consensus CPU [#3](https://github.com/osmosis-labs/cometbft/pull/3).

### v23.0.6 - 14 Mar 2024
- Re-enabled White Whale pools and bumped CometBFT for stronger P2P logic during the incident response window [#7716](https://github.com/osmosis-labs/osmosis/pull/7716) [#7726](https://github.com/osmosis-labs/osmosis/pull/7726).
- Reduced sqrt price computations and converted CL operations to mutative variants for faster math [#7599](https://github.com/osmosis-labs/osmosis/pull/7599) [#7692](https://github.com/osmosis-labs/osmosis/pull/7692).
- Logged pruning errors instead of panicking so lagging nodes stayed online [#558](https://github.com/osmosis-labs/cosmos-sdk/pull/558).

### v23.0.7-iavl-v1 - 15 Mar 2024
- Pulled in the latest IAVL patch to improve pruning throughput on store-heavy nodes [#7750](https://github.com/osmosis-labs/osmosis/pull/7750).

### v23.0.8 - 20 Mar 2024
- Defaulted timeout-commit to three seconds and added a guard flag to prevent unsafe overrides [#7769](https://github.com/osmosis-labs/osmosis/pull/7769).

### v23.0.8-iavl-v1 - 20 Mar 2024
- Mirrored the timeout policy while tagging the IAVL-enabled binaries for operators [#7769](https://github.com/osmosis-labs/osmosis/pull/7769).

### v23.0.11 - 8 Apr 2024
- Soft-forked the bundled IBC to respond to ASA-2024-007 without full chain downtime [#7987](https://github.com/osmosis-labs/osmosis/pull/7987).

### v23.0.11-iavl-v1 - 8 Apr 2024
- Shipped the same security fork for IAVL nodes to keep the store variants aligned [#7987](https://github.com/osmosis-labs/osmosis/pull/7987).

### v23.0.12-iavl-v1 - 9 Apr 2024
- Backported async pruning support directly to the IAVL build so archival nodes could upgrade immediately [#7994](https://github.com/osmosis-labs/osmosis/pull/7994).

### v24.0.0 - 5 Apr 2024
- Restructured ProtoRev distributions to split profits between burn and community pool destinations each epoch [#7509](https://github.com/osmosis-labs/osmosis/pull/7509) [#7564](https://github.com/osmosis-labs/osmosis/pull/7564).
- Added IBC wasm light clients and expanded before-send hook queries for richer cross-chain integrations [#7503](https://github.com/osmosis-labs/osmosis/pull/7503) [#7623](https://github.com/osmosis-labs/osmosis/pull/7623).
- Accelerated concentrated liquidity paths by trimming hook marshalling, limiting uptime fetches, and raising the gas floor [#7550](https://github.com/osmosis-labs/osmosis/pull/7550) [#7685](https://github.com/osmosis-labs/osmosis/pull/7685) [#7833](https://github.com/osmosis-labs/osmosis/pull/7833).

### v24.0.1 - 9 Apr 2024
- Enabled async pruning for legacy IAVL stores, closing the gap with v23.0.12 tags [#7994](https://github.com/osmosis-labs/osmosis/pull/7994).

### v24.0.2 - 24 Apr 2024
- Delivered massive BigDec speedups and removed legacy lockup quirks that blocked testnets [#8006](https://github.com/osmosis-labs/osmosis/pull/8006) [#8030](https://github.com/osmosis-labs/osmosis/pull/8030).
- Hardened config overwrites and defaulted min-gas-prices to the EIP-1559 value to keep blocks full [#8118](https://github.com/osmosis-labs/osmosis/pull/8118) [#8131](https://github.com/osmosis-labs/osmosis/pull/8131).

### v24.0.3 - 24 Apr 2024
- Moved noisy websockets logs to debug and fixed txSearch pagination to keep RPC responsive [#21](https://github.com/osmosis-labs/cometbft/pull/21) [#22](https://github.com/osmosis-labs/cometbft/pull/22).
- Optimized Merkle hashing in CometBFT for faster proof generation [#25](https://github.com/osmosis-labs/cometbft/pull/25).

### v24.0.4 - 26 Apr 2024
- Added single-authenticator queries and whitelisted them for Stargate access, improving wallet UX [#8142](https://github.com/osmosis-labs/osmosis/pull/8142).
- Lowered timeout-commit defaults to 1.5 seconds to accelerate finality [#8149](https://github.com/osmosis-labs/osmosis/pull/8149).

### v25.0.0 - 8 May 2024
- Integrated Skip's block-sdk and top-of-block auction, enabling MEV capture without centralizing ordering [#7935](https://github.com/osmosis-labs/osmosis/pull/7935).
- Reworked smart account fee handling and protorev accumulators for more predictable deductions [#8125](https://github.com/osmosis-labs/osmosis/pull/8125) [#8157](https://github.com/osmosis-labs/osmosis/pull/8157).
- Allowed IBC wasm clients to perform Stargate queries and limited CL hook writes, reducing latency [#8144](https://github.com/osmosis-labs/osmosis/pull/8144) [#7689](https://github.com/osmosis-labs/osmosis/pull/7689).

### v25.0.1 - 23 May 2024
- Upgraded to IBC-go v7.4.1 and cached poolmodule lookups to reduce per-swap overhead [#8293](https://github.com/osmosis-labs/osmosis/pull/8293) [#8128](https://github.com/osmosis-labs/osmosis/pull/8128).
- Shortened timeout-commit to one second and aligned cometside async mempool updates for better throughput [#8298](https://github.com/osmosis-labs/osmosis/pull/8298) [#69](https://github.com/osmosis-labs/cometbft/pull/69).

### v25.0.2 - 29 May 2024
- Raised gossip throttles while stripping IBC rate-limit checks from CheckTx to cut admission latency [#8312](https://github.com/osmosis-labs/osmosis/pull/8312) [#8308](https://github.com/osmosis-labs/osmosis/pull/8308).
- Added LRU caches and per-thread randomness in CometBFT gossip to shrink contention [#73](https://github.com/osmosis-labs/cometbft/pull/73) [#76](https://github.com/osmosis-labs/cometbft/pull/76) [#77](https://github.com/osmosis-labs/cometbft/pull/77).

### v25.0.3 - 13 Jun 2024
- Relaxed the flush throttle to 80ms, letting peers catch up faster under high load [#8329](https://github.com/osmosis-labs/osmosis/pull/8329).

### v25.1.0 - 18 Jun 2024
- Lowered JSON unmarshalling overhead across IBC packet paths to reduce CPU spikes [#8398](https://github.com/osmosis-labs/osmosis/pull/8398).

### v25.1.1 - 19 Jun 2024
- Dropped timeout-commit to 600ms, added an IBC spam filter, and bumped block-sdk for faster rechecks [#8394](https://github.com/osmosis-labs/osmosis/pull/8394) [#8409](https://github.com/osmosis-labs/osmosis/pull/8409) [#8408](https://github.com/osmosis-labs/osmosis/pull/8408).

### v25.1.2 - 21 Jun 2024
- Reset cached pool data on creation and patched CometBFT block selection to avoid regressions introduced in v25.1.1 [#8415](https://github.com/osmosis-labs/osmosis/pull/8415) [#8417](https://github.com/osmosis-labs/osmosis/pull/8417).

### v25.1.3 - 21 Jun 2024
- Removed redundant IBC acknowledgement checks and cached the tx decoder to lighten CheckTx workloads [#8420](https://github.com/osmosis-labs/osmosis/pull/8420) [#8421](https://github.com/osmosis-labs/osmosis/pull/8421).
- Fixed indexer configs so `osmosisd init` ships functional defaults [#8431](https://github.com/osmosis-labs/osmosis/pull/8431).

### v25.2.0 - 12 Jul 2024
- Landed additional CometBFT mempool optimizations from Skip's upstream work [#8455](https://github.com/osmosis-labs/osmosis/pull/8455).

### v25.2.1 - 26 Jul 2024
- Cut commit timeouts to 500ms and refined timeout-propose to 1.8s, pushing block time lower [#8546](https://github.com/osmosis-labs/osmosis/pull/8546).
- Added a missing module params CLI query for parity with REST clients [#8504](https://github.com/osmosis-labs/osmosis/pull/8504).

### v26.0.0 - 19 Sep 2024
- Upgraded to Cosmos SDK 0.50 and CometBFT 0.38, enabling ledger-ready smart account auth and new taker-fee sharing [#8274](https://github.com/osmosis-labs/osmosis/pull/8274) [#8581](https://github.com/osmosis-labs/osmosis/pull/8581) [#8310](https://github.com/osmosis-labs/osmosis/pull/8310).
- Hardened before-send hooks, boosted unauthenticated gas, and refreshed tagged dependencies for the new branch [#8535](https://github.com/osmosis-labs/osmosis/pull/8535) [#8573](https://github.com/osmosis-labs/osmosis/pull/8573) [#8649](https://github.com/osmosis-labs/osmosis/pull/8649).
- Added richer module events and telemetry for lockup, superfluid, and CL actions [#8494](https://github.com/osmosis-labs/osmosis/pull/8494).

### v26.0.1 - 19 Sep 2024
- Ensured delegation iteration continues through errors so migrations do not abort mid-run [#8732](https://github.com/osmosis-labs/osmosis/pull/8732).

### v26.0.2 - 3 Oct 2024
- (Release contained packaging updates only; no changelog entry was authored.)

### v27.0.0 - 14 Nov 2024
- Updated CosmWasm VM and optimizer, refreshed tagged SDK/Comet versions, and fixed constitution state exports ahead of the Dragonberry fork [#8734](https://github.com/osmosis-labs/osmosis/pull/8734) [#8777](https://github.com/osmosis-labs/osmosis/pull/8777) [#8779](https://github.com/osmosis-labs/osmosis/pull/8779).
- Corrected OSMO supply offsets and expanded x/gauges queries for better indexer coverage [#8751](https://github.com/osmosis-labs/osmosis/pull/8751) [#8563](https://github.com/osmosis-labs/osmosis/pull/8563).
- Fixed concurrency issues in x/lockup tests, eliminating heisenbugs before rollout [#8765](https://github.com/osmosis-labs/osmosis/pull/8765).

### v27.0.1 - 18 Nov 2024
- Bumped CometBFT, corrected a cross-chain swap channel misconfiguration, and tracked previously uncounted tokenfactory inflows [#8831](https://github.com/osmosis-labs/osmosis/pull/8831) [#8876](https://github.com/osmosis-labs/osmosis/pull/8876) [#8922](https://github.com/osmosis-labs/osmosis/pull/8922).

### v28.0.0 - 10 Dec 2024
- Updated the math package dependency as the first step toward the 2025 pruning upgrades [#8857](https://github.com/osmosis-labs/osmosis/pull/8857).
