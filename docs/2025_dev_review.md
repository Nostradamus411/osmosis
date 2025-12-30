# Osmosis 2025 Development Review

## Executive Summary (Non-Technical)
- Early 2025 patches focused on keeping nodes healthy by fixing smart account events, enabling async pruning, and tightening pruning safety so operators could upgrade without downtime [v28.0.1 release](https://github.com/osmosis-labs/osmosis/releases/tag/v28.0.1) [#8858](https://github.com/osmosis-labs/osmosis/pull/8858) [#8923](https://github.com/osmosis-labs/osmosis/pull/8923) [#9334](https://github.com/osmosis-labs/osmosis/pull/9334).
- Spring upgrades in the v29 line tidied legacy code and aligned with upstream Cosmos and Wasm updates, smoothing governance queries and performance while keeping features stable for end users [v29.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v29.0.0) [#8996](https://github.com/osmosis-labs/osmosis/pull/8996) [#9372](https://github.com/osmosis-labs/osmosis/pull/9372).
- The v30 family delivered visible experience changes: higher base gas prices, permissionless supercharged pools, and mempool fairness fixes reduced congestion and front-running risk for traders [v30.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v30.0.0) [#9434](https://github.com/osmosis-labs/osmosis/pull/9434) [#9454](https://github.com/osmosis-labs/osmosis/pull/9454) [#9469](https://github.com/osmosis-labs/osmosis/pull/9469).
- v31.0.0 capped the year by automating taker-fee burns, adding an inflation API, and smoothing staking rewards so the community could watch supply trends while benefiting from stronger deflationary pressure [v31.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v31.0.0) [#9526](https://github.com/osmosis-labs/osmosis/pull/9526) [#9530](https://github.com/osmosis-labs/osmosis/pull/9530) [#9541](https://github.com/osmosis-labs/osmosis/pull/9541) [#9559](https://github.com/osmosis-labs/osmosis/pull/9559).

## Executive Summary (Technical)
- Store and pruning reliability improved through targeted Cosmos SDK bumps, tagged store releases, and IAVL fixes, reducing stalled pruning and keeping async pruning safe on busy validators [#8906](https://github.com/osmosis-labs/osmosis/pull/8906) [#8923](https://github.com/osmosis-labs/osmosis/pull/8923) [#8940](https://github.com/osmosis-labs/osmosis/pull/8940) [#9334](https://github.com/osmosis-labs/osmosis/pull/9334) [#9340](https://github.com/osmosis-labs/osmosis/pull/9340).
- Protocol functionality advanced with pfm v8.1.1, Wasmd 0.53.2, Cosmos SDK 0.50.14, and new taker-fee routing, enabling supercharged pools and cleaner fee accounting [#8996](https://github.com/osmosis-labs/osmosis/pull/8996) [#8880](https://github.com/osmosis-labs/osmosis/pull/8880) [#9455](https://github.com/osmosis-labs/osmosis/pull/9455) [#9434](https://github.com/osmosis-labs/osmosis/pull/9434).
- Mempool fairness and latency were priorities across v30 with FIFO ordering, gas-floor enforcement, cometbft deforking, and timeout tuning to prevent stuck queues [#9469](https://github.com/osmosis-labs/osmosis/pull/9469) [#9493](https://github.com/osmosis-labs/osmosis/pull/9493) [#9527](https://github.com/osmosis-labs/osmosis/pull/9527) [#9528](https://github.com/osmosis-labs/osmosis/pull/9528).
- Observability and rewards telemetry matured through the inflation endpoint, consensus min-fee increases, and staking reward smoothing, improving dashboards and validator UX [#9440](https://github.com/osmosis-labs/osmosis/pull/9440) [#9526](https://github.com/osmosis-labs/osmosis/pull/9526) [#9559](https://github.com/osmosis-labs/osmosis/pull/9559).


## Detailed Changes by Release
### v28.0.1 – 7 Jan 2025
- Fixed smart account event emission so downstream indexers receive consistent hook data [#8858](https://github.com/osmosis-labs/osmosis/pull/8858).
- Upgraded to Cosmos SDK 0.50.11, picking up upstream bug fixes and security hardening [#8906](https://github.com/osmosis-labs/osmosis/pull/8906).
- Tagged the cosmos-sdk store module to v1.1.1 to allow async pruning deployments [#8923](https://github.com/osmosis-labs/osmosis/pull/8923).

### v28.0.2 – 16 Jan 2025
- Bumped store dependencies to v1.1.1-v0.50.11-v28-osmo-2 so pruning improvements ship with the chain [#8940](https://github.com/osmosis-labs/osmosis/pull/8940).
- Decoupled node releases from SQS packaging to speed up binary distribution [#8886](https://github.com/osmosis-labs/osmosis/pull/8886).
- Removed duplicate root key fetches in IAVL pruning, yielding a 9% speedup on Osmosis [cosmos/iavl#1026](https://github.com/cosmos/iavl/pull/1026).

### v28.0.3 – 30 Jan 2025
- Pulled in a forked Block SDK patch to stop CheckTx panics [#8968](https://github.com/osmosis-labs/osmosis/pull/8968).
- Added support for final-hop memos in cross-chain swaps to preserve contextual metadata [#8895](https://github.com/osmosis-labs/osmosis/pull/8895).

### v28.0.4 – 6 Feb 2025
- Upgraded cometbft to v0.38.17 to patch a security vulnerability [#8978](https://github.com/osmosis-labs/osmosis/pull/8978).
- Switched Block SDK imports to the forked version maintained for Osmosis [#8985](https://github.com/osmosis-labs/osmosis/pull/8985).
- Hardened force prune logic to avoid data corruption during manual pruning [#8983](https://github.com/osmosis-labs/osmosis/pull/8983).

### v28.0.5 – 12 Mar 2025
- Adopted ibc-go v8.7.0 to stay current with upstream relayer fixes [#9050](https://github.com/osmosis-labs/osmosis/pull/9050).
- Exposed raw state queries for CosmWasm-managed pools, simplifying contract integrations [#9006](https://github.com/osmosis-labs/osmosis/pull/9006).

### v28.0.6 – 28 Mar 2025
- Allowed pruning to skip stuck versions instead of halting the node [#9334](https://github.com/osmosis-labs/osmosis/pull/9334).
- Limited pool manager cache writes to finalize execution mode to prevent cache corruption [#9332](https://github.com/osmosis-labs/osmosis/pull/9332).
- Updated IAVL to ignore broken legacy state while upgrading [#9340](https://github.com/osmosis-labs/osmosis/pull/9340).

### v29.0.0 – 2 Apr 2025
- Upgraded Packet Forward Middleware to v8.1.1 for cross-chain routing improvements [#8996](https://github.com/osmosis-labs/osmosis/pull/8996).
- Bumped Wasmd from 0.53.0 to 0.53.2 to pick up CosmWasm fixes [#8880](https://github.com/osmosis-labs/osmosis/pull/8880).
- Raised ibc-go to v8.6.1 for relayer stability [#9005](https://github.com/osmosis-labs/osmosis/pull/9005).
- Removed the obsolete superfluid Balancer→CL migration path so calls now return an error [#9011](https://github.com/osmosis-labs/osmosis/pull/9011).
- Updated tagged submodules to align dependencies [#9059](https://github.com/osmosis-labs/osmosis/pull/9059).
- Continued using the forked Block SDK in app wiring [#8985](https://github.com/osmosis-labs/osmosis/pull/8985).
- Increased target block time slightly for operational stability [#9021](https://github.com/osmosis-labs/osmosis/pull/9021).
- Removed legacy IAVL state reliance to avoid replaying corrupted snapshots [#9340](https://github.com/osmosis-labs/osmosis/pull/9340).

### v29.0.1 – 10 Apr 2025
- Resolved codec errors when querying all proposals so clients receive complete results [#9372](https://github.com/osmosis-labs/osmosis/pull/9372).

### v29.0.2 – 14 Apr 2025
- Fixed pagination for governance proposals, ensuring API parity with on-chain data [#9375](https://github.com/osmosis-labs/osmosis/pull/9375).

### v30.0.0 – 31 Jul 2025
- Upgraded to Go 1.23 to access newer runtime optimizations [#9355](https://github.com/osmosis-labs/osmosis/pull/9355).
- Bumped Wasmd to the latest release to inherit CosmWasm improvements [#9427](https://github.com/osmosis-labs/osmosis/pull/9427).
- Segregated non-OSMO taker-fee revenue onto a dedicated whitelist for quote assets [#9434](https://github.com/osmosis-labs/osmosis/pull/9434).
- Refreshed chain seeds shipped with `osmosisd init` [#9420](https://github.com/osmosis-labs/osmosis/pull/9420).
- Restored the missing coinbase Rosetta dependency for exchange integrations [#9396](https://github.com/osmosis-labs/osmosis/pull/9396).
- Removed authorized quote denom validation to simplify pool creation [#9436](https://github.com/osmosis-labs/osmosis/pull/9436).
- Raised the consensus minimum fee to 0.01 uosmo per gas, discouraging spam [#9440](https://github.com/osmosis-labs/osmosis/pull/9440).
- Upgraded Cosmos SDK to 0.50.14 for security and performance patches [#9455](https://github.com/osmosis-labs/osmosis/pull/9455).
- Routed top-of-block auction proceeds to the community pool [#9456](https://github.com/osmosis-labs/osmosis/pull/9456).
- Updated submodules to the tagged release set [#9457](https://github.com/osmosis-labs/osmosis/pull/9457).
- Synced the mempool-1559 base fee with the new consensus minimum [#9460](https://github.com/osmosis-labs/osmosis/pull/9460).
- Ensured tokenfactory hooks check parent gas meters before proceeding [#9465](https://github.com/osmosis-labs/osmosis/pull/9465).

### v30.0.1 – 12 Aug 2025
- Upgraded the Go toolchain to 1.23.4 to avoid runtime timer panics under load [#9473](https://github.com/osmosis-labs/osmosis/pull/9473).

### v30.0.2 – 14 Aug 2025
- Fixed Block SDK ordering by address so mempool ordering cannot be gamed by crafted accounts [#9469](https://github.com/osmosis-labs/osmosis/pull/9469) [#9395](https://github.com/osmosis-labs/osmosis/issues/9395).

### v30.0.3 – 8 Sep 2025
- Corrected protorev post-handler values to avoid inaccurate routing profits [#9467](https://github.com/osmosis-labs/osmosis/pull/9467).
- Updated base fee defaults and clamps for EIP-1559 style mempool management [#9476](https://github.com/osmosis-labs/osmosis/pull/9476).
- Bumped Block SDK to v2.1.8-mempool for FIFO ordering support [#9488](https://github.com/osmosis-labs/osmosis/pull/9488).
- Pulled in the staled mempool fix and associated tests from the Block SDK [#9493](https://github.com/osmosis-labs/osmosis/pull/9493).

### v30.0.4 – 24 Sep 2025
- Consumed child-context gas when CosmWasm contracts panic due to out-of-gas, mirroring the original fix from #9511 [#9542](https://github.com/osmosis-labs/osmosis/pull/9542) [#9511](https://github.com/osmosis-labs/osmosis/pull/9511).

### v30.0.5 – 26 Sep 2025
- Repointed to upstream cometbft after deforking the dependency [#9527](https://github.com/osmosis-labs/osmosis/pull/9527).
- Lowered consensus timeout configs to shorten block proposal cycles [#9528](https://github.com/osmosis-labs/osmosis/pull/9528).

### v31.0.0 – 27 Oct 2025
- Reduced tokenfactory hook gas to keep token operations affordable [#9511](https://github.com/osmosis-labs/osmosis/pull/9511).
- Added an RPC endpoint for protocol inflation metrics [#9526](https://github.com/osmosis-labs/osmosis/pull/9526).
- Introduced an on-chain taker-fee burn mechanic for OSMO collections [#9530](https://github.com/osmosis-labs/osmosis/pull/9530).
- Converted non-OSMO taker fees into OSMO before burning to reinforce deflation [#9541](https://github.com/osmosis-labs/osmosis/pull/9541).
- Enabled multihop taker-fee swaps so complex trades still contribute to burns [#9547](https://github.com/osmosis-labs/osmosis/pull/9547).
- Refreshed Swagger artifacts for downstream SDKs [#9548](https://github.com/osmosis-labs/osmosis/pull/9548).
- Updated the module path to v31 for Go module consumers [#9560](https://github.com/osmosis-labs/osmosis/pull/9560).
- Smoothed daily staking rewards to reduce payout volatility [#9559](https://github.com/osmosis-labs/osmosis/pull/9559).
- Raised the consensus minimum fee to 0.03 uosmo per gas, building on earlier fee reforms [#9440](https://github.com/osmosis-labs/osmosis/pull/9440).
