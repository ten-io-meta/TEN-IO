# TEN.IO / ERC-8060 — GitHub portfolio audit and retention map

**Review date:** 2026-11-19. **Scope:** 12 repositories visible through the connected ten-io-meta GitHub account, priority source/ABI review, open draft PRs and historic onchain evidence. NOT a completed line-by-line audit of every dependency or every deployment. No changes to main or to deployed code; no funds transferred.

## Target organization

| Repository | Classification | Proposed action | Why |
|---|---|---|---|
| ten-io-meta/ERCs | STANDARDS DOCUMENTATION | KEEP / edit normative drafts only here | Contains draft erc-8060 and erc-8098; a standards fork, not production financial contracts |
| ten-io-meta/EIPs | LEGACY STANDARDS FORK | KEEP AS REFERENCE, review whether to archive | Generic fork and historic proposal work; current application-layer ERC changes belong under ERCs |
| ten-io-meta/erc8060-native-eth-value | CORE STRICT REFERENCE RESEARCH | KEEP, CONSOLIDATE PRs #1/#5 | main still contains older Ownable reference; PR #1 fixes strict ABI, PR #5 adds generic zero-admin reference, PR #4 mixes product fees into standard repo and should be retired after preserving its experiments |
| ten-io-meta/erc8060-reservable | OPTIONAL CONDITIONAL RESEARCH | KEEP, REVIEW STACKED PRs #10-16 | Six-function reserve accounting, experimental economic application witnesses and forged-provenance counterexamples; main is NOT the final v6 candidate |
| ten-io-meta/open-erc-composition-laboratory | INDEPENDENT VERIFICATION LAB | KEEP, INTEGRATE VERIFIED EVIDENCE | Original scientific OECL baseline and onchain witnesses; manifest currently DISABLES local Reservable source entries, CI only covers a subset |
| ten-io-meta/agent-reservable-composition | EXPERIMENTAL VALIDATION SUITE | KEEP AS A LAB OR MOVE AFTER TEST AUDIT | ERC-8004/other ERC agent workflow testing; includes MOCKS with fictional token value, not deployable backed collateral |
| ten-io-meta/TEN-IO | PRODUCT / COLLECTIONS / CULTURAL ARCHIVE | KEEP, RESTRUCTURE README | Product-specific Umbral, metadata, audiovisual archive and draft fee collection implementation belong here, not in ERC-8060 standard repo |
| ten-io-meta/tenio-frontend-nuevo | LIVE/LEGACY PRODUCT FRONTEND | KEEP BUT QUARANTINE UNVERIFIED ONCHAIN ADAPTERS | React app contains legacy Ownable surplus panel and ABI mismatches; its configured deployments are now verified distinct legacy V2-like Mainnet/Sepolia contracts holding seven live NFTs each; see read-only PR #2 |
| ten-io-meta/TENIO-Origin | HISTORICAL GENESIS DOCUMENTATION | KEEP / mark historical | Source provenance and Mainnet chain history; do not present as strict modern ERC-8060 deployment |
| ten-io-meta/TENIO-Fragment | HISTORICAL VULNERABLE PRODUCT CONTRACT | KEEP AS EVIDENCE / ARCHIVE ONLY AFTER REVIEW | Published burn can destroy a token without ETH if underfunded; full owner withdraw; executable instructions reproduced by audit PR #3; old contracts are immutable |
| ten-io-meta/DefiLlama-Adapters | OBSOLETE USER EXPERIMENT | ARCHIVE CANDIDATE, not part of protocol | User explicitly identifies as an abandoned initial trial |
| ten-io-meta/unreplied-mvp | UNRELATED EXPERIMENT | ARCHIVE CANDIDATE, not part of protocol | User explicitly identifies as irrelevant |

## Real code risks and inconsistencies found

1. **Two competing strict references:** erc8060-native-eth-value main / PR #1 retains an Ownable surplus role, while PR #5 adds a separate no-admin reference. PR #4 adds fee accounting despite the decision that TEN.IO fees are product-level. Before any merge select ONE canonical no-admin security reference and keep historic one marked legacy. PR #4 can be closed as superseded only after saving its distinct tests/evidence.
2. **Legacy Fragment financial flaw:** TENIOFragment.sol burns and then pays ETH only if balance >= 0.10; owner withdraw can remove all reserves. TENIO Fragment source-to-chain PR #3 proves matching executable bytes, not full metadata. Historic deployments are NOT strict ERC-8060.
3. **Separate Umbral V2 in frontend:** contracts/UmbralFragmentV2_flat.sol contains a different legacy asset at 0.012 mint, 0.010 burn, 1000 cap. This V2 includes Ownable, owner withdrawal of computed surplus, and owner setBaseURI; it does NOT implement valueOf or strict ERC8060 ID. contracts/UmbralFragmentV2.sol is empty. The two frontend .env contract addresses are distinct from known TENIO-Fragment addresses. Frontend audit PR #2 has now verified both via two public RPCs: Mainnet 0x841c6a8e1858fd7daf25824e4d305ff06bd7a525 (7 live NFTs, 0.086 ETH held against 0.070 ETH reported reserve); Sepolia 0x47C049d0441dae4D06fd7E8d512e4E91B7E92e77 (7 live NFTs, 0.076 test ETH held against 0.070 reported test ETH reserve). Both share runtime hash 0x4ea55e352e81d0a52669ec97cc6d7ab871315cf54c0060ba615b30e932d0f74f and return false for strict ERC-8060 ID. These are observed snapshots, NOT yet compiler-source identity proof.
4. **Frontend ABI mismatch and permissive read fallbacks:** App.jsx imports ABI.json and shows an owner withdrawal panel; the connection module imports UmbralFragment.json with extra nextId/mintedEver. getOwnedFragments uses tokenOfOwnerByIndex, unsupported by the new plain ERC721 reference. Some missing getter errors become displayed zeros: do not present failed reads as solvent/no liability.
5. **Reservable cannot be sold as a right to repayment by itself:** reserveAllowance is permission to create locks, not locked or collected ETH; releaseValue allows the controller to release its own lock. Only authenticated, separately funded and enforceable app settlement can justify a creditor claim.
6. **OECL provenance failure under forged trust roots:** PR #16 demonstrates exact-runtime NFT and factory bytecode with attacker-chosen constructor storage. ERC165, codehash, self-declared isSolvent and lockedBy can all be misleading without deploy and state history authentication. PASS in a negative attack demonstration does not mean production-safe.
7. **Agent-composition mock is not an ETH vault:** contracts/ERC8060ReservableMock.sol lets a token owner call mintValue with arbitrary amount **without any payable ETH deposit**, and mock transfer permission clearing is deliberately unimplemented. CompositionAccountingDemo.sol has purely numerical reserves without real funds. MUST remain labeled local simulations; never onboard them as solvency evidence in OECL.
8. **ERC-8098 is a separate ERC20 behavioral standard:** no new ERC20 ABI; token supply must never increase post-deployment, and burns cannot be reversed. ERC-721 cap examples are similar in spirit but are NOT ERC-8098 conformance. No dedicated 8098 verified production reference was located.

## Next work order

1. **Safety gate first:** onchain identify the two addresses actually used by frontend; compare their ABI and deployed runtime with the flattened Umbral V2 source; block automatic migration and do not send any ETH.
2. **Consolidate strict ERC-8060:** reconcile PR #1 vs #5, use no-admin fee-free reference as target and move/copy every valuable test from the creator-fee PR #4 to TEN.IO if distinct. Keep the interface ONLY valueOf and burn.
3. **Keep history visible:** label TENIO-Origin and TENIO-Fragment historical with explicit warnings, correct any misleading reversible/fully backed claims. Do not overwrite source used for deployed-runtime attestations.
4. **Promote only authenticated financial tests:** integrate v6 Reservable and agent-composition research into OECL as version-pinned evidence, with explicit negative outcomes and UNKNOWN judgments; do not import mocks as backed assets.
5. **Set product contracts separately:** TEN-IO PR #1 defines 0.010 ETH backing + 0.002 fee = 0.012 ETH Umbral; larger collection 0.10 + 0.02 = 0.12 ETH. Keep wallet/CID/max supply as deployment-time values subject to review.
6. **Archive obsolete repos as GitHub repository metadata** after confirming no live deployment/CI dependency; do not delete historical evidence. No repository archive/delete connector operation is available in this review, so these remain proposals, not completed archival actions.

## What must NOT be inferred

- Passing 63, 19, 69 or 213 tests does not certify all contracts or combinations. Some tests intentionally demonstrate unsafe behavior.
- A source repo does not update any contract already deployed to Mainnet or Sepolia.
- Every branch has not yet been independently fuzzed/formally verified; this audit is triage and source-boundary review, not production authorization.
- A fee-wallet being historically the owner of one legacy contract is not an appropriate universal default for any third-party ERC-8060 deployment.

## Key evidence links

- [Strict ERC-8060 PR #5](https://github.com/ten-io-meta/erc8060-native-eth-value/pull/5)
- [Strict ABI alignment PR #1](https://github.com/ten-io-meta/erc8060-native-eth-value/pull/1)
- [Creator fee alternative PR #4](https://github.com/ten-io-meta/erc8060-native-eth-value/pull/4)
- [TEN.IO product collections PR #1](https://github.com/ten-io-meta/TEN-IO/pull/1)
- [Historical Fragment executable audit PR #3](https://github.com/ten-io-meta/TENIO-Fragment/pull/3)
- [OECL forged provenance counterexamples PR #16](https://github.com/ten-io-meta/erc8060-reservable/pull/16)
- [Frontend adapter/chain read-only audit PR #2](https://github.com/ten-io-meta/tenio-frontend-nuevo/pull/2)
