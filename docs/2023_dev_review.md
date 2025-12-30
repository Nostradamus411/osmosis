# Osmosis 2023 Development Review

## Executive Summary (Non-Technical)
- Q1 deliveries brought geometric TWAPs, downtime detection, and the first ProtoRev integration so contract teams had richer tooling before concentrated liquidity landed [v14.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v14.0.0) [v15.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v15.0.0) [#3609](https://github.com/osmosis-labs/osmosis/pull/3609) [#4244](https://github.com/osmosis-labs/osmosis/pull/4244) [#4107](https://github.com/osmosis-labs/osmosis/pull/4107).
- Mid-year upgrades introduced concentrated liquidity and CosmWasm pools, plus iterative security patches that kept validators upgrading without halts [v16.1.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v16.1.0) [#3014](https://github.com/osmosis-labs/osmosis/issues/3014) [#5354](https://github.com/osmosis-labs/osmosis/pull/5354) [#5822](https://github.com/osmosis-labs/osmosis/pull/5822).
- The v17 through v19 sequence hardened taker fees, refined ProtoRev routing, and upgraded Wasm, making MEV capture and smart-contract integrations safer for traders [v17.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v17.0.0) [v19.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v19.0.0) [#6034](https://github.com/osmosis-labs/osmosis/pull/6034) [#5863](https://github.com/osmosis-labs/osmosis/pull/5863) [#5869](https://github.com/osmosis-labs/osmosis/pull/5869).
- Year-end v20 and v21 tracks tuned mempool EIP-1559 parameters, added protocol revenue tracking, and smoothed governance hooks to prepare for 2024's authz and gauge improvements [v20.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v20.0.0) [v21.0.0 release](https://github.com/osmosis-labs/osmosis/releases/tag/v21.0.0) [#6420](https://github.com/osmosis-labs/osmosis/pull/6420) [#6804](https://github.com/osmosis-labs/osmosis/pull/6804) [#6959](https://github.com/osmosis-labs/osmosis/pull/6959).

## Executive Summary (Technical)
- Geometric TWAP math, BigDec power utilities, and downtime-detection queries expanded oracle accuracy and incident tooling for integrators [#2788](https://github.com/osmosis-labs/osmosis/pull/2788) [#3708](https://github.com/osmosis-labs/osmosis/pull/3708) [#3609](https://github.com/osmosis-labs/osmosis/pull/3609).
- Concentrated liquidity shipping required new CL math APIs, ProtoRev optimizations, and tokenfactory before-send hooks that redefined gas economics [#3014](https://github.com/osmosis-labs/osmosis/issues/3014) [#5281](https://github.com/osmosis-labs/osmosis/pull/5281) [#4382](https://github.com/osmosis-labs/osmosis/pull/4382).
- Taker fee and ProtoRev iterations balanced MEV capture with user cost by enforcing spread-factor updates, hook-based backruns, and route capping [#5045](https://github.com/osmosis-labs/osmosis/pull/5045) [#5930](https://github.com/osmosis-labs/osmosis/pull/5930) [#6034](https://github.com/osmosis-labs/osmosis/pull/6034).
- Mempool and authz reliability improved through EIP-1559 parameter tuning, epoch CPU reductions, and new governance telemetry [#7170](https://github.com/osmosis-labs/osmosis/pull/7170) [#7093](https://github.com/osmosis-labs/osmosis/pull/7093) [#7147](https://github.com/osmosis-labs/osmosis/pull/7147).

## Detailed Changes by Release
### v14.0.0 - 17 Jan 2023
- Introduced downtime detection, geometric TWAP queries, and expanded IBC to Wasm callbacks for richer contract automation [#3609](https://github.com/osmosis-labs/osmosis/pull/3609) [#3847](https://github.com/osmosis-labs/osmosis/pull/3847) [#2387](https://github.com/osmosis-labs/osmosis/pull/3838).
- Enhanced osmomath with BigDec power utilities and log2 math to support upcoming CL features [#3676](https://github.com/osmosis-labs/osmosis/pull/3676) [#3708](https://github.com/osmosis-labs/osmosis/pull/3708).

### v14.0.1 - 15 Feb 2023
- Patched gamm CLI swap estimation and TWAP genesis validation to keep front-end tooling accurate [#4132](https://github.com/osmosis-labs/osmosis/pull/4132) [#4262](https://github.com/osmosis-labs/osmosis/pull/4262).

### v15.0.0 - 10 Mar 2023
- Launched ProtoRev, PoolManager, and Validator Set Preference modules, streamlining swap routing and delegator controls [#4107](https://github.com/osmosis-labs/osmosis/pull/4107) [#3911](https://github.com/osmosis-labs/osmosis/pull/3911) [#4340](https://github.com/osmosis-labs/osmosis/pull/4340).
- Added async ICQ support and strengthened governance rate limits to balance cross-chain risk [#4207](https://github.com/osmosis-labs/osmosis/pull/4207) [#4340](https://github.com/osmosis-labs/osmosis/pull/4340).

### v15.1.0 - 20 Apr 2023
- Upgraded wasmvm for CWA-2023-002 and exposed Protorev liquidity queries plus backrun events for analytics [#4829](https://github.com/osmosis-labs/osmosis/pull/4829) [#4878](https://github.com/osmosis-labs/osmosis/pull/4878) [#5822](https://github.com/osmosis-labs/osmosis/pull/5822).

### v15.1.2 - 25 May 2023
- Pulled in ibc-go 4.3.1 security fixes and relaxed TWAP genesis checks for healthier state exports [#5129](https://github.com/osmosis-labs/osmosis/pull/5129) [#5134](https://github.com/osmosis-labs/osmosis/pull/5134).

### v16.1.0 - 13 Jul 2023
- Reverted the lock-and-superfluid staking change to stabilize the new CL module rollout [#5822](https://github.com/osmosis-labs/osmosis/pull/5822).

### v16.1.1 - 26 Jul 2023
- Published cosmovisor hashes and restored superfluid queries to support validators moving to v16 [#5824](https://github.com/osmosis-labs/osmosis/pull/5824) [#5831](https://github.com/osmosis-labs/osmosis/pull/5831).

### v17.0.0 - 18 Aug 2023
- Added async IBC hooks for contracts and reduced CL state machine breakages during migrations [#5072](https://github.com/osmosis-labs/osmosis/pull/5072) [#5863](https://github.com/osmosis-labs/osmosis/pull/5863) [#5869](https://github.com/osmosis-labs/osmosis/pull/5869).

### v18.0.0 - 24 Aug 2023
- Deployed taker fee spike experiments and cut epoch CPU time to keep block production deterministic [#6034](https://github.com/osmosis-labs/osmosis/pull/6034) [#6161](https://github.com/osmosis-labs/osmosis/pull/6161).

### v19.0.0 - 31 Aug 2023
- Enabled taker fees on mainnet with safeguards for superfluid interactions and tokenfactory events [#6034](https://github.com/osmosis-labs/osmosis/pull/6034) [#6195](https://github.com/osmosis-labs/osmosis/pull/6195).

### v19.1.0 - 20 Sep 2023
- Added mutative BigDec helpers and stricter CL math to curb rounding errors in swaps [#6428](https://github.com/osmosis-labs/osmosis/pull/6428) [#6368](https://github.com/osmosis-labs/osmosis/pull/6368).

### v19.2.0 - 28 Sep 2023
- Bumped IAVL and delivered CW gauge export fixes to unblock state sync scenarios [#6476](https://github.com/osmosis-labs/osmosis/pull/6476) [#6492](https://github.com/osmosis-labs/osmosis/pull/6492).

### v20.0.0 - 17 Oct 2023
- Released Smart Accounts whitelist, URL-encoded send support, and SDK 0.47 upgrade with staking fixes [#6420](https://github.com/osmosis-labs/osmosis/pull/6420) [#6766](https://github.com/osmosis-labs/osmosis/pull/6766) [#6413](https://github.com/osmosis-labs/osmosis/pull/6413).
- Guarded taker fee and poolmanager APIs, adding CosmWasm query coverage and denom metadata protections [#6632](https://github.com/osmosis-labs/osmosis/pull/6632) [#6699](https://github.com/osmosis-labs/osmosis/pull/6699).

### v20.1.0 - 23 Oct 2023
- Shipped PoolManager denoms query improvements and tightened mempool defaults for the new fee market [#6884](https://github.com/osmosis-labs/osmosis/pull/6884) [#6959](https://github.com/osmosis-labs/osmosis/pull/6959).

### v20.1.1 - 1 Nov 2023
- Added taker fee gRPC fixes and affiliate swap filters to prevent arbitrage abuse [#6890](https://github.com/osmosis-labs/osmosis/pull/6890) [#6939](https://github.com/osmosis-labs/osmosis/pull/6939).

### v20.1.2 - 2 Nov 2023
- Reduced epoch CPU load and log2 math overhead to stabilize validator resource usage [#7093](https://github.com/osmosis-labs/osmosis/pull/7093) [#7106](https://github.com/osmosis-labs/osmosis/pull/7106).

### v20.2.1 - 9 Nov 2023
- Enabled mempool EIP-1559 by default and aligned PoolManager spot price APIs with BigDec outputs [#6897](https://github.com/osmosis-labs/osmosis/pull/6897) [#6487](https://github.com/osmosis-labs/osmosis/pull/6487).

### v20.4.0 - 21 Nov 2023
- Patched affiliate swap mempool checks and exposed PoolManager denom helpers for downstream modules [#6906](https://github.com/osmosis-labs/osmosis/pull/6906) [#6863](https://github.com/osmosis-labs/osmosis/pull/6863).

### v20.5.0 - 25 Nov 2023
- Continued mempool gas tuning ahead of the v21 release, backporting Skip improvements (no additional changelog entries).

### v21.0.0 - 12 Dec 2023
- Added protocol revenue tracking across modules, Cosmos SDK 0.47 upgrades, and taker-fee whitelist hooks [#6804](https://github.com/osmosis-labs/osmosis/pull/6804) [#6937](https://github.com/osmosis-labs/osmosis/pull/6937) [#6859](https://github.com/osmosis-labs/osmosis/pull/6859).
- Improved governance metadata handling and raised gas thresholds, preparing for v21 patch cadence [#7243](https://github.com/osmosis-labs/osmosis/pull/7243) [#6959](https://github.com/osmosis-labs/osmosis/pull/6959).

### v21.1.3 - 23 Dec 2023
- Lowered epoch CPU usage and halved log2 computation time, smoothing validator load [#7093](https://github.com/osmosis-labs/osmosis/pull/7093) [#7106](https://github.com/osmosis-labs/osmosis/pull/7106).

### v21.1.4 - 23 Dec 2023
- Dropped consensus timeout-commit to 4 seconds by default to accelerate finality [#7180](https://github.com/osmosis-labs/osmosis/pull/7180).
