# TEN.IO: product collections built on the ERC-8060 draft

**Application repository. Not the ERC-8060 specification or its canonical security reference.** The normative strict draft interface lives in `ten-io-meta/ERCs/ERCS/erc-8060.md`. The generic ETH-backed research reference lives in `ten-io-meta/erc8060-native-eth-value`.

The product implementation `contracts/TENIOImmutableCollection.sol` implements the **strict two-function ERC-8060 draft**:
- `valueOf(tokenId)`: ETH recoverable by the existing owner.
- `burn(tokenId)`: exact ETH returned to the existing owner or atomic revert.

The product application additionally configures **fees, a fixed fee destination, a maximum number of ever-minted NFTs and immutable metadata paths**. None of those product features are requirements for all ERC-8060 NFTs, and they must not be added to the minimal `IERC721Value` interface.

## Collection parameters: planning only

See `config/erc8060-collections.json`. These values are **per-collection**:

| Collection | ETH backing per NFT | Mint fee | Total paid |
| --- | ---: | ---: | ---: |
| Umbral | **0.010 ETH** | **0.002 ETH** | **0.012 ETH** |
| Later collection | **0.10 ETH** | **0.02 ETH** | **0.12 ETH** |
| Future denomination | **1 ETH** | **not decided** | not decided |
| Future denomination | **10 ETH** | **not decided** | not decided |

The 0.012 ETH Umbral figure is the **total issue price**, not its backing. Do not report the backing as 0.012 ETH.

The real fee recipient wallet, `maxMinted`, metadata CID, final symbols and future higher-denomination fees **must be independently validated before deployment**. They are deliberately `null` in the planning file. Do not substitute the historical TENIO Fragment deployer/owner address, an outside project's address or any address from tests. The deploy-time fee recipient has zero authority to change the smart contract or withdraw the backing.

## Immutable economic design

- Each NFT has an exact fixed ETH backing for its particular collection. One deployment = one collection.
- Successful mint requires `backingPerToken + mintFee`, retains the backing and forwards the **fee** atomically to the immutable beneficiary address. If the beneficiary refuses the transfer, the whole mint reverts.
- Only the actual NFT owner may burn to redeem ETH. A revert of the ETH transfer restores the NFT and accounting.
- No `Ownable`, privileged burn, owner withdrawal, setters, upgrade or proxy paths.
- Total issued NFT count has a hard immutable ceiling; burned IDs are not reused. **This is a product-level NFT scarcity choice, not implementation of ERC-8098** (the latter is an ERC-20 profile).
- No rescue of forced ETH accidentally sent to the contract. This is an explicit disadvantage of an ownerless, no-surplus-withdrawal design.
- Mint is permissionless upon deployment (first ready transaction can mint). No artist reserved editions or allowlist is implemented; distribution controls require separately reviewed product extensions.
- The IPFS base URI must be static and content-addressed before deploying the contract.

## Tests and deployment policy

```bash
npm ci
npm run compile
npm test
```

`test/TENIOImmutableCollection.test.js` covers fee accounting, strict ERC-165 detection, mint caps and token-ID non-reuse, authorized redemption, failed fee forwarding, failed owner payouts and reentrancy attempts. **Test examples of future 1 and 10 ETH backing include arbitrary test-only fees; those fees are NOT agreed product terms.**

No deployment script is provided. Do not deploy automatically. Do not insert a real wallet secret into the repository. Before any Mainnet ETH is involved, a professional external security audit, property-based invariants, proven metadata integrity and explicit production approval are necessary.

No historical TENIO Fragment or TEN.IO Origin contract is modified by these source files. Any existing onchain contract remains immutable. No changes to ERC-8098, Reservable or OECL are made here. OECL can eventually assess the implementation only after independently authenticated provenance; simply implementing `valueOf` and `burn` does not constitute OECL approval.
