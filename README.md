# TEN.IO — Audiovisual archive and Ethereum application

TEN.IO is an audiovisual project combining music, IPFS metadata, ENS and optional Ethereum collectibles. The project-level NFT collection, publication economics and creative assets are separate from the general-purpose ERC-8060 draft standard.

**Status:** cultural archive and experimental application engineering; no new production contract is certified by the research PRs below. Source-code changes do not update previously deployed contracts.

## Important separation

| Layer | Repository | Purpose |
| --- | --- | --- |
| ERC-8060 draft | [ERCs fork](https://github.com/ten-io-meta/ERCs) | Public ERC proposal: valueOf and burn, ETH-redemption semantics |
| Strict ERC-8060 reference | [erc8060-native-eth-value](https://github.com/ten-io-meta/erc8060-native-eth-value) | **PR #6 only**: one no-admin, no-fee research implementation; 20/20 local tests |
| Reservable research | [erc8060-reservable](https://github.com/ten-io-meta/erc8060-reservable) | Optional conditional reserve accounting; not automatic creditor rights |
| Composition evidence | [OECL](https://github.com/ten-io-meta/open-erc-composition-laboratory) | Independently bounded evidence for cross-protocol claims |
| TEN.IO product | [this repository](https://github.com/ten-io-meta/TEN-IO) | Collection fees, supply caps, videos, metadata and brand settings |
| Live/historical interface | [tenio-frontend-nuevo](https://github.com/ten-io-meta/tenio-frontend-nuevo) | Preserve live Umbral V2 NFT rights; [source and owner evidence PR #3](https://github.com/ten-io-meta/tenio-frontend-nuevo/pull/3) |

## Collections: design, not current deployment

Umbral **planned** economic terms: 0.010 ETH recoverable backing + 0.002 ETH mint fee = **0.012 ETH total**. A higher denomination uses 0.10 ETH backing + 0.02 fee = 0.12 ETH total. Future 1 ETH and 10 ETH backing collections have **no confirmed fee parameters**. The independent product Solidity implementation is in [TEN.IO application PR #1](https://github.com/ten-io-meta/TEN-IO/pull/1), currently a research draft, not deployed.

Critical deployment inputs (fee beneficiary, minted cap, permanent metadata CID) must be verified before authorizing any real ETH.

## Historical contracts — NOT the strict ERC-8060 reference

- [TENIO-Origin](https://github.com/ten-io-meta/TENIO-Origin): genesis-era Mainnet record; see historical deployment `0x8Cfc6b16B01604c83bef1e315d6693d2e7dA43Ad`.
- [TENIO-Fragment](https://github.com/ten-io-meta/TENIO-Fragment): Mainnet `0x7c88fabe05fd373d56a728f9896f87ede10db789`; historical burn/withdraw design does not meet strict ERC-8060 economic guarantees. [Security audit PR #3](https://github.com/ten-io-meta/TENIO-Fragment/pull/3).
- [Umbral V2 in frontend source](https://github.com/ten-io-meta/tenio-frontend-nuevo/blob/main/contracts/UmbralFragmentV2_flat.sol): legacy 1,000 NFT cap and 0.012 ETH mint/0.010 ETH refund, with owner controlled surplus; deployed on Mainnet at `0x841c6a8e1858fd7daf25824e4d305ff06bd7a525` and Sepolia at `0x47C049d0441dae4D06fd7E8d512e4E91B7E92e77`. [Frontend inventory PR #2](https://github.com/ten-io-meta/tenio-frontend-nuevo/pull/2) and [provenance/owner PR #3](https://github.com/ten-io-meta/tenio-frontend-nuevo/pull/3) record seven live NFTs on each chain at pinned blocks, and reproduced executable runtime, but full original compiler metadata remains unverified.

These old contracts are already deployed or historical. Editing GitHub cannot retroactively change them. Do not present them as audited strict ERC-8060 deployments.

## Audiovisual archive

- [Season 1 timeline](timeline/genesis.md)
- [Fragment catalog](fragments/001-crack-in-the-silence.md)
- [IPFS archive](ipfs/root-archive.md)
- [Genesis contract notes](contracts/genesis-contract.md)
- [ERC-8060 product notes](contracts/erc-8060.md)
- [ERC-8098 product notes](contracts/erc-8098.md)
- [TEN.IO audiovisual frontend](https://tenio.eth.limo)

## Engineering audit and cleanup

**Current coordination index:** [GitHub portfolio, holder-protection rules and release gates (PR #2)](https://github.com/ten-io-meta/TEN-IO/pull/2). It records all 12 repositories, exact PR status, [single strict ERC-8060 PR #6](https://github.com/ten-io-meta/erc8060-native-eth-value/pull/6), live Umbral V2 provenance, independent Reservable/OECL roles and safe archival candidates. Keep this as the source of truth for engineering status rather than duplicating progress statements across product and standard repositories. DefiLlama-Adapters and unreplied-mvp are considered legacy/unrelated experiments, not active protocol components.

**No farming. No promises. Just fragments of truth.**
