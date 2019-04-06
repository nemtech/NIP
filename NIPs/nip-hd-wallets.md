# NIP-? - Multi-Account Hierarchy for Deterministic Wallets

```
    NIP: ?
    Layer: Applications
    Title: Multi-Account Hierarchy for Deterministic Wallets
    Author: Grégory Saive <greg@nem.foundation>
    Status: Draft
    Type: Standards Track
    Created: 2019-04-09
    License: MIT
```

## Table of contents

- [Abstract](#abstract)
- [Motivation](#motivation)
- [Specification: Conversion functions](#specification-conversion-functions)
- [Specification: Extended keys](#specification-extended-keys)
  - [Key trees](#key-trees)
  - [Compatibility](#compatibility)
  - [Security implications](#security-implications)
- [Specification: Wallet structure](#specification-wallet-structure)
- [Specification: Mnemonic seeds](#specification-mnemonic-seeds)
- [Specification: A logical hierarchy with BIP44](#specification-a-logical-hierarchy-with-bip44)

## Abstract

This document describes hierarchical deterministic wallets for NEM.

This document uses Bitcoin's [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki), [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki), [BIP43](https://github.com/bitcoin/bips/blob/master/bip-0043.mediawiki) and [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) as sources of documentation.

A standard for deterministic wallets creation is needed to improve handling of NEM wallets within client applications.

This standard will set the rules for generating _extended keys_ as defined in [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki), for generating _mnemonic pass phrases_ as defined in [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) and for _defining a logical hierarchy for deterministic wallets_.

Extracts from the Bitcoin documents will be added in quotes and detailed _extensions_  or _updates_ will be annotated for the NEM platform.

## Motivation

Previous versions of NEM clients (wallets) used a _user password_ to encrypt private keys, resulting in the need of creating backups every time when a new private key is generated.

Deterministic wallets do not require frequent backups as they will permit the generation of multiple public keys (addresses) without revealing the _spending private key_, with the use of elliptic curve mathematics.

This multi-account hierarchy will support _several chains of keypairs_ (multiple trees) as to allow selective sharing of wallet public keys. 

Additionally, we will be defining Mnemonic code for generating deterministic keys using the definition in [Bitcoin BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki).

Furthermore, using [Bitcoin BIP44], we will define a scheme to build logical hierarchies for deterministic wallets. This will represent the recommended method to work with NEM CATAPULT wallets and keys.

## Specification: Conversion functions

From the Bitcoin standard, as **standard conversion functions**, we assume:

- `point(p)`: returns the coordinate pair resulting from EC point multiplication (repeated application of the EC group operation) of the **ED25519** base point with the integer p.
- `ser32(i)`: serialize a 32-bit unsigned integer `i` as a 4-byte sequence, most significant byte first.
- `ser256(p)`: serializes the integer `p` as a 32-byte sequence, most significant byte first.
- `serP(P)`: serializes the coordinate pair `P = (x,y)` as a byte sequence using [SEC1](https://www.secg.org/sec1-v2.pdf)'s compressed form: (0x02 or 0x03) || ser256(x), where the header byte depends on the parity of the omitted y coordinate.
- `parse256(p)`: interprets a 32-byte sequence as a 256-bit number, most significant byte first.

## Specification: Extended keys

The [Bitcoin BIP32 document](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) describes extended keys in detail. With the following extracts:

> We represent an extended private key as (k, c), with k the normal private key, and c the chain code. An extended public key is represented as (K, c), with K = point(k) and c the chain code.

> Each extended key has 2^31 normal child keys, and 2^31 hardened child keys. Each of these child keys has an index. The normal child keys use indices 0 through 2^31-1. The hardened child keys use indices 2^31 through 2^32-1. To ease notation for hardened key indices, a number iH represents i+2^31.

Multiple *child key derivation* functions (CKDs) are proposed in [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) as well, with the following references :

- [**Private** parent key --> **Private** child key: `CKDpriv((kpar, cpar), i) → (ki, ci)`](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#private-parent-key--private-child-key)
- [**Public** parent key --> **Public** child key: `CKDpub((Kpar, cpar), i) → (Ki, ci)`](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#public-parent-key--public-child-key)
- [**Private** parent key --> **Public** child key: `N((k, c)) → (K, c)`](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#private-parent-key--public-child-key)
- It is not possible to derive a **private** child key from a **public** parent key.

### Key trees

In the [source document](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki), a key tree is defined that will make use of the CKDs defined above. The child key derivation functions are cascaded several times to build a tree of keys.

Leaf nodes of that tree each define one key (private or public). A detailed explanation of the created key tree can be found [here](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#the-key-tree).

### Compatibility

From the Bitcoin BIP32 standard document: 

> To comply with this standard, a client must at least be able to import an extended public or private key, to give access to its direct descendants as wallet keys. The wallet structure (master/account/chain/subchain) presented in the second part of the specification is advisory only, but is suggested as a minimal structure for easy compatibility - even when no separate accounts or distinction between internal and external chains is made. However, implementations may deviate from it for specific needs; more complex applications may call for a more complex tree structure.

### Security implications

Security properties of the Extended Keys proposals can be found [here](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#security).

From the Bitcoin BIP32 description: 

> Private and public keys must be kept safe as usual. Leaking a private key means access to coins - leaking a public key can mean loss of privacy.

> Somewhat more care must be taken regarding extended keys, as these correspond to an entire (sub)tree of keys.

> One weakness that may not be immediately obvious, is that knowledge of a parent extended public key plus any non-hardened private key descending from it is equivalent to knowing the parent extended private key (and thus every private and public key descending from it). This means that extended public keys must be treated more carefully than regular public keys. It is also the reason for the existence of hardened keys, and why they are used for the account level in the tree. This way, a leak of account-specific (or below) private key never risks compromising the master or other accounts.

## Specification: Wallet structure

The previous sections specified key trees and their nodes as defined by the Bitcoin BIP32 source document. Next we are imposing a wallet structure that leverages this tree of keys. 

From the Bitcoin BIP32 standard - [The default wallet layout](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#the-default-wallet-layout):

> The layout defined in this section is a default only, though clients are encouraged to mimic it for compatibility, even if not all features are supported.

> An hyper deterministic wallet is organized as several `accounts`. Accounts are numbered, the default account ("") being number 0. Clients are not required to support more than one account - if not, they only use the default account.

> Each account is composed of two keypair chains: an **internal** and an **external** one. The _external_ keychain is used to _generate new public addresses_, while the _internal_ keychain is used for _all other operations_.

We will detail the logical hierarchy more in detail in the section [BIP44: A logical hierarchy for deterministic wallets](#specification-bip44-a-logical-hierarchy-for-deterministic-wallets).

## Specification: Mnemonic seeds

Mnemonic seeds are sentences with words matching a [Wordlists](https://github.com/bitcoin/bips/blob/master/bip-0039/bip-0039-wordlists.md) as well as holding a checksum as defined in [BIP39's `Generating the mnemonic`](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki#generating-the-mnemonic).

Mnemonic seeds are created from the available [Wordlists](https://github.com/bitcoin/bips/blob/master/bip-0039/bip-0039-wordlists.md) in the BIP39 annex.

Following references will be used during reference implementation: 

- [Generating the mnemonic](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki#generating-the-mnemonic)
- [From mnemonic to seed](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki#from-mnemonic-to-seed)

## Specification: A logical hierarchy with BIP44

Because we want to comply to the BIP44 standard we will define path levels as recommended in BIP44. This gives us the following path levels: 

```
m / purpose' / coin_type' / account' / change / address_index
```

- Our `purpose` level will be `44'` as we are building a logical hierarchy following the BIP44 standard. 
- Our `coin_type` is `43'` as this corresponds to `NEM` in [SLIP-44 annexed to the source document](https://github.com/satoshilabs/slips/blob/master/slip-0044.md).
- The next level corresponds to the _index_ of the `account` that we want to use, starting at `0` for the **first** account.
- The `change` path level is used to _define which keychain must be used_. Set to `0`, the keychain used is said to be `external`, while any other `change` path level will result in using the `internal` keychain.
- The `address_index` path level corresponds to the _index_ of the `address` that we want to use, starting at `0` for the **first** address.

The appended apostrophe (`'`) in path levels is used to mark **hardened key levels**. As defined in Bitcoin BIP32 and in this document's [Wallet structure](#specification-wallet-structure), the BIP32 algorithm permits derivation of two entirely independent keyspaces. Those are usually called **the hardened key space** and **the non-hardened key space**. 

For NEM, we can define a _base logical hierarchy_ of `m/44'/43'`. It is recommended for client implementations to follow this standard in order to achieve better cross-client compatibility.

For client implementations which _do not wish_ to implement the full capabilities of multi-account hierarchy for deterministic wallets, it is **recommended** to use only the following _default address path_: `m/44'/43'/0'/0/0`.

### Examples

| account | keychain | address | path |
|---|---|---|---|
| **first** | **external** | **first** | `m/44'/43'/0'/0/0` |
| **first** | **external** | **second** | `m/44'/43'/0'/0/1` |
| **first** | **external** | **third** | `m/44'/43'/0'/0/2` |
| **first** | **internal** | **first** | `m/44'/43'/0'/1/0` |
| **first** | **internal** | **second** | `m/44'/43'/0'/1/1` |
| **first** | **internal** | **third** | `m/44'/43'/0'/1/2` |
| **second** | **external** | **first** | `m/44'/43'/1'/0/0` |
| **second** | **external** | **second** | `m/44'/43'/1'/0/1` |
| **second** | **external** | **third** | `m/44'/43'/1'/0/2` |
| **second** | **internal** | **first** | `m/44'/43'/1'/1/0` |
| **second** | **internal** | **second** | `m/44'/43'/1'/1/1` |
| **second** | **internal** | **third** | `m/44'/43'/1'/1/2` |

## References

- [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki)
- [BIP32 - Extended Keys](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#extended-keys)
- [BIP32 - Child Key Derivation Functions](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#child-key-derivation-ckd-functions)
- [BIP32 - The key tree](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#the-key-tree)
- [BIP32 - Master key generation](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#master-key-generation) 
- [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki)
- [BIP39 - Generating the mnemonic](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki#generating-the-mnemonic)
- [BIP39 - Rules about wordlist](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki#wordlist)
- [BIP39 - From mnemonic to seed](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki#from-mnemonic-to-seed)
- [BIP39 - Wordlists](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki#wordlists)
- [BIP43](https://github.com/bitcoin/bips/blob/master/bip-0043.mediawiki) 
- [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki)
- [BIP44 - Path levels](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#path-levels)
- [SLIP44 - Registered coin types](https://github.com/satoshilabs/slips/blob/master/slip-0044.md)

## History

| **Date**      | **Version**   |
| ------------- | ------------- |
| Apr 6 2019    | Initial Draft |
