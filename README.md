# Community Token Whitelist

This repository contains entries for native tokens and NFTs which are considered whitelisted for usage in third-party applications such as wallets, explorers etc.


## Structure

The root consists of folders for each different network. Within such folder, there are corresponding `native-tokens` and `nfts` folders which contain
the submitted JSON files.

- Native token JSON files must contain the [IRC30](https://github.com/iotaledger/tips/blob/main/tips/TIP-0030/tip-0030.md) metadata.
  This data must also occur within the immutable metadata field of the foundry output which mints the given token.
  - The filename must adhere to following pattern: `<project/ticker-name>-<foundry-id-hex(0x prefixed)>.json`
- NFT JSON files must contain the [IRC27](https://github.com/iotaledger/tips/blob/main/tips/TIP-0027/tip-0027.md) metadata.
  This data must also occur within the immutable metadata field of the NFT output.
  - The filename must adhere to following pattern: `<project/collection-name>-<nft-id-hex(0x prefixed)>.json`

> Nomenclature: We call NFTs minting other NFTs `Collection NFTs`. 

Note that we consider subsequent NFTs minted by a whitelisted collection NFT as also whitelisted as long as the issuer field within those NFTs is set to correspond to the collection NFT.
Therefore there is no resubmission needed when minting additional NFTs for a collection. 
However, we do not support transitive whitelisting: 
If collection NFT `A` is whitelisted and NFT `B` is created by `A` (`B` is therefore also whitelisted), then another NFT `C` created by `B` is not considered whitelisted.

## How To Contribute

Following steps will get your entries added to the whitelist:
1. Submit a PR which adds the defined JSON file in the right network and type folder. Make sure that the JSON data is valid and adheres to either the IRC27/IRC30 standards (depending on the type).
1. You must supply an Ed25519 signature within the PR description which signs the JSON data together with the corresponding public key (not the Ed25519 address).
  Do not submit multiple JSON files at once, supply a PR for each entry individually. We check the supplied signatures/public keys against the on-chain
  outputs by examining whether the given foundry or NFT was created through the specified public key bearer.
1. A group of reviewers will check the signatures and the IRC27/IRC30 data against the on-chain data and for profanity.
2. Your PR gets merged and our public service will pick up the change to whitelist your tokens/NFTs.

## Violations

We take the right to simply delete any whitelisting entries in case we find that any metadata of a given token/NFT violates the safety of our community by
linking to NSFW media or containing profanity. This means that should it come to our attention that collection NFTs violate these terms, we will simply
delete the collection NFT entry. We will also delete any entry if it comes to our attention that the given tokens/NFTs are part of a scam or compromising the security of our community.