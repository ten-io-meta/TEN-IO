# TEN.IO / ERC-8060 — Engineering inventory and release gates

**Snapshot: 2026-11-19.** Scope: 12 repositories under `ten-io-meta`, verified GitHub PR heads and the pinned-block evidence recorded below. This is a *coordination index*, not a production audit, current live-balance oracle, security certification or migration authorization.

**Operating rule:** do not merge, deploy, transfer ETH, execute `burn`, change frontend production routing, deprecate an NFT address holding live assets, or archive a repository with unresolved dependencies as part of documentation cleanup. Draft branches and deployed contracts are separate realities.

## 1. One owner per responsibility

| Repository | Type | Action | Security boundary |
| --- | --- | --- | --- |
| [ERCs](https://github.com/ten-io-meta/ERCs) | Standards fork | **KEEP** | ERC-8060 and ERC-8098 draft specifications; no collection economics or deployment wallets |
| [EIPs](https://github.com/ten-io-meta/EIPs) | Older standards fork | **KEEP AS HISTORY** | Check historical refs before considering archive |
| [erc8060-native-eth-value](https://github.com/ten-io-meta/erc8060-native-eth-value) | Strict ERC-8060 *example reference* | **KEEP / use PR #6** | One no-admin, no-fee reference; not production approved |
| [erc8060-reservable](https://github.com/ten-io-meta/erc8060-reservable) | Optional conditional extension / research | **KEEP SEPARATE** | Accounting reserve locks cannot be advertised as unconditional strict redemption or creditor enforcement |
| [open-erc-composition-laboratory](https://github.com/ten-io-meta/open-erc-composition-laboratory) | OECL capability and evidence laboratory | **KEEP / improve evidence** | Provenance, actual execution and rights verified independently; UNKNOWN on insufficient evidence |
| [agent-reservable-composition](https://github.com/ten-io-meta/agent-reservable-composition) | Agent/composition simulation | **KEEP LAB-ONLY** | Unbacked numerical mock collateral is not ETH backing |
| [TEN-IO](https://github.com/ten-io-meta/TEN-IO) | Product and audiovisual archive | **KEEP** | Collection names, supply limits, fees, recipients, fixed metadata and art belong only to product |
| [tenio-frontend-nuevo](https://github.com/ten-io-meta/tenio-frontend-nuevo) | Live legacy frontend and Umbral V2 evidence | **KEEP; DO NOT REPOINT** | Preserve separate legacy ABI/withdraw panel and contract addresses from future ERC-8060 UI |
| [TENIO-Origin](https://github.com/ten-io-meta/TENIO-Origin) | Historical provenance | **KEEP AS EVIDENCE** | Historical contract does not inherit later ERC-8060 guarantees |
| [TENIO-Fragment](https://github.com/ten-io-meta/TENIO-Fragment) | Historical deployed risky contract | **KEEP AS SECURITY EVIDENCE** | Published burn can succeed with no refund if underfunded; owner withdrawal is not reserve-preserving |
| [DefiLlama-Adapters](https://github.com/ten-io-meta/DefiLlama-Adapters) | Abandoned experiment | **ARCHIVE CANDIDATE ONLY** | Do not delete; verify no CI/workflow/source dependency first |
| [unreplied-mvp](https://github.com/ten-io-meta/unreplied-mvp) | Unrelated experiment | **ARCHIVE CANDIDATE ONLY** | Do not delete; verify no active dependency first |

## 2. Current PR and test status (this snapshot)

| Scope | PR | Verified finding | Decision |
| --- | --- | --- | --- |
| Generic strict ERC-8060 | [native-eth-value #6](https://github.com/ten-io-meta/erc8060-native-eth-value/pull/6) | Exact head `b88323b32edf9def8e35caae7330994651e3f6ec`, [CI 44576693742](https://github.com/ten-io-meta/erc8060-native-eth-value/actions/runs/44576693742) SUCCESS, **20/20 tests**, 15 compiled Solidity files | **DRAFT; one canonical `ERC8060Reference.sol`; do not deploy without an independent audit** |
| Prior ERC-8060 branches | [#1](https://github.com/ten-io-meta/erc8060-native-eth-value/pull/1), [#5](https://github.com/ten-io-meta/erc8060-native-eth-value/pull/5) | **CLOSED WITHOUT MERGE**, superseded by #6; historical test evidence still available | No competing canonical references; do not report their 52/63 tests as current #6 results |
| TEN.IO collection application | [TEN-IO #1](https://github.com/ten-io-meta/TEN-IO/pull/1) | 19 tests reported passing on its independent app branch; immutable fee-route example and cap are **product choices** | **DRAFT**; no production recipient, metadata CID or cap approved |
| Portfolio documentation | [TEN-IO #2](https://github.com/ten-io-meta/TEN-IO/pull/2) | Repository inventory and this coordination index | **DRAFT; documentation only** |
| Frontend contract/ABI audit | [frontend #2](https://github.com/ten-io-meta/tenio-frontend-nuevo/pull/2) | Legacy Mainnet/Sepolia addresses and non-strict ERC-8060 support verified | **DRAFT**; do not silently switch application ABI/addresses |
| Umbral V2 executable and provenance | [frontend #3](https://github.com/ten-io-meta/tenio-frontend-nuevo/pull/3) | Executable runtime match; two-RPC holder/reserve verification; Sepolia direct CREATE and ABI constructor evidence | **DRAFT**; missing full original metadata and Mainnet creation/constructor |
| Conditional research | [Reservable #10–#16](https://github.com/ten-io-meta/erc8060-reservable/pulls) | Differing experimental evidence stages, including forged provenance counterexamples | **RESEARCH**; do not batch-merge as a validated financial protocol |
| Reservable documentation accuracy | [Reservable #17](https://github.com/ten-io-meta/erc8060-reservable/pull/17) | Six-function ABI and explicit limits of accounting-only locks | **DRAFT** |
| Historical evidence | [TENIO-Fragment #3](https://github.com/ten-io-meta/TENIO-Fragment/pull/3), [#4](https://github.com/ten-io-meta/TENIO-Fragment/pull/4), [TENIO-Origin #1](https://github.com/ten-io-meta/TENIO-Origin/pull/1) | Immutable historical deployments and bounded source-matching claims | **PRESERVE; do not repoint holders** |
| Mock warning | [agent-reservable-composition #1](https://github.com/ten-io-meta/agent-reservable-composition/pull/1) | Unfunded simulated reserves clearly labeled | **DRAFT** |

Read the linked PRs for their exact-head status; this table is frozen to the snapshot date. GitHub `main` branches are not automatically changed by draft PRs.

## 3. Umbral V2 — live holder preservation gate

The deployed contracts are independent from the new generic reference, are **not** strict ERC-8060, and have **7 live NFTs each** in the cited snapshots.

| Chain | Contract | Pinned block from verified holder audit | Live token IDs | ETH balance / computed required reserve |
| --- | --- | ---: | --- | --- |
| Ethereum Mainnet | `0x841c6a8e1858fd7daf25824e4d305ff06bd7a525` | **26,450,613** | **2, 3, 7, 8, 9, 10, 11** | **0.086 ETH / 0.070 ETH** |
| Sepolia | `0x47C049d0441dae4D06fd7E8d512e4E91B7E92e77` | **12,169,851** | **1, 6, 7, 9, 10, 14, 26** | **0.076 test ETH / 0.070 test ETH** |

Evidence: [two-RPC holder and reserve CI 44578459622](https://github.com/ten-io-meta/tenio-frontend-nuevo/actions/runs/44578459622) **SUCCESS**, plus [source/constructor CI 44578459379](https://github.com/ten-io-meta/tenio-frontend-nuevo/actions/runs/44578459379) **SUCCESS**. These are *historical snapshots*, not live balances or a forward-looking solvency warranty.

- Actual published source is `contracts/UmbralFragmentV2_flat.sol` in the frontend repository; `contracts/UmbralFragmentV2.sol` is empty. The flattening has an unusual encoding; the audit script decodes it before compiling.
- `solc 0.8.30`, optimizer 200, `viaIR=false`, EVM Cancun reproduce **7,107 executable bytes**. The full 7,160-byte runtime has **different 53-byte CBOR metadata**; exact original compiler-input/source-tree identity remains **unproven**.
- The V2 economic code fixes `MINT_PRICE=0.012 ether`, `BURN_REFUND=0.010 ether`, historical max issuance of 1,000 and owner-only *calculated surplus* withdrawal. The legacy burn requires token ownership and reverts if ETH payout fails. An optional admin `setBaseURI` affects future mints, not stored existing token URIs.
- **Sepolia direct CREATE**: [tx `0x3b732000dd75e323d33ded51c137f0deb8a718ae1344e2521b086f14c6d04e61`](https://sepolia.etherscan.io/tx/0x3b732000dd75e323d33ded51c137f0deb8a718ae1344e2521b086f14c6d04e61), block 9,067,661; receipt and ABI constructor `(string _baseURI,address initialOwner)` were reconstructed. Initial owner `0x75DA787FDA32092079dbe113c5c9DBC22CBBC455`.
- **Mainnet creation transaction and original full Solidity metadata remain UNKNOWN**, and Sepolia creation is *not* a proxy for Mainnet creation.
- All seven observed Mainnet token URIs have the **same hash**; validate metadata expectations before making any uniqueness/visual-content claim.
- **Never** automatically burn, migrate, repoint, overwrite, or replace holders' assets. A future migration, if offered, must be opt-in, explicitly tested, clearly disclosed and independent of the strict reference's deployment.

## 4. ERC-8060 strict reference acceptance gate

The single candidate is [`contracts/ERC8060Reference.sol` at PR #6 exact head](https://github.com/ten-io-meta/erc8060-native-eth-value/blob/b88323b32edf9def8e35caae7330994651e3f6ec/contracts/ERC8060Reference.sol).

- Strict interface: `valueOf(uint256)` and `burn(uint256)` (`ERC-165 0x88495fe7`). Optional `0xcadf338f` is legacy *value-only* detection, **not** proof of owner redemption or custody.
- No `Ownable`, admin, issuer withdrawal, price, mint fee, reserved fee wallet, pause or upgrade. Any positive deposit creates a distinct claim for exactly its deposited ETH; token IDs are not reused; this example has **no global supply cap**.
- Current test gate: **20/20 local Hardhat tests** including reentrancy, owner-only burn, failed payout rollback, rejected safeMint callback, forced-surplus behavior and shadow-ledger accounting. This is not formal proof.
- **Before production**: independently review bytecode and deployment source provenance, stateful invariant/fuzz tests, production threat model, external audit and receiving-contract/redeemability UX. Do not merge the draft merely because CI is green.

TEN.IO's **0.010 ETH backing + 0.002 ETH commercial fee** and **0.10 ETH backing + 0.02 ETH commercial fee** are proposals in TEN.IO's product PR #1, *never normative ERC-8060 requirements*.

## 5. Dependency and cleanup order

1. **Protect history:** Keep Umbral V2/Fragment/Origin contracts and verified evidence visible; complete Mainnet creation/constructor provenance where archival data is accessible. Resolve/clearly badge frontend ABI and the absence of strict `valueOf` before publishing any change to a live interface.
2. **Keep one ERC reference:** Use **PR #6 only** as the candidate for ERC-8060; earlier PRs #1/#5 are closed research. No owner role, no fee routing and no TEN.IO application logic in the generic contract.
3. **Keep products independent:** Review TEN.IO application PR #1 separately, with immutable deployment-time fee destination, finite cap and metadata policy only after sign-off. Do not treat this as a replacement for Umbral V2 holders.
4. **Finish proof gates before OECL adoption:** Reconcile Reservable PR #10–#16 in their research order; never accept an unfunded mock or self-attested factory/codehash as real collateral. In OECL mark insufficient authenticated rights as **UNKNOWN** rather than certifying it.
5. **Archive only if dependency-free:** DefiLlama-Adapters and unreplied-mvp are *candidates*. Review active consumers, releases, external references and GitHub Actions before archiving. Prefer **Archive**, not **Delete**. Keep older ERC/EIP proposal records accessible.

## 6. Limits and change policy

- This inventory does not establish future token holder counts, ETH reserve balances, deployed executable source identity beyond the bounded checks above, or full auditor assurance.
- The legacy TENIO-Fragment `withdraw()` can remove its full balance and its `burn()` can succeed without paying when underfunded. **Do not confuse it with Umbral V2**, which has different executable logic and reserve handling.
- Reservable accounting, ERC-8098 monotone **ERC-20** supply, OECL assessment receipts, ERC-8060 redemption and TEN.IO collection economics are different layers; no implicit security or ERC compliance is inherited from one to another.
- **No automated merges, deployments, funds movement, repository deletes or frontend production reconfiguration from this documentation work.** Keep research PRs as drafts pending review.
