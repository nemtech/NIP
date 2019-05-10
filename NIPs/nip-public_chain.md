# NIP-? - Catapult technology release for Public Network

## Summary

```
    NIP: 000?
    Layer: Core
    Title: Catapult technology release for Public Network
    Author: Gregory Saive <greg@nem.foundation>
    Discussions-To: TBD
    Comments-URI: TBD
    Status: Draft
    Type: Process
    Created: 2019-05-10
    License: Apache-2.0
    License-Code: ASL v2
```

## Introduction

This document aims to provide with a decision making process about upgrading the current public blockchain network NEM (hereafter "**NIS1**") with the newly available Catapult Technology (hereafter "**Catapult**", each of which represent a "_Project_" and both "_Projects_").

Following projects are target of this documentation:

- [`NIS1`: NemProject/nem.core](https://github.com/NemProject/nem.core)
- [`Catapult`: nemtech/catapult-server](https://github.com/nemtech/catapult-server)

Discussions have been made about migration of NIS1 data sets to Catapult but several points remain open for discussion and unresolved.

## Specification

This section describes the process that will be followed when Catapult releases to a Public Network. 

### Possible Outcomes

Possible outcomes include, and are limited to:

- 1) **Catapult** technology **upgrades** NIS1, resulting in **one chain** and network.
- 2) **Catapult** technology is **released alongside** of NIS1, resulting in **two chains** and network.

Hereafter, these two outcomes will be referred to as the `one chain approach` (as in Point 1) and the `two chains approach`  (as in Point 2) respectively.

**Issue Resolution**: <span style="color: #f00;">One Chain Approach</span> OR <span style="color: #f00;">Two Chains Approach</span>

### Migrated Modules / Datasets / Integrations

Following list includes all the migrated modules that are currently available with NIS1 and datasets or _integrations_ (exchanges/clients) that must be taken into account when **migrating** to the Catapult technology:

- [Account data (balance(s), importance, multisig relationships)](#dataset-migration-account-data)
- [Transaction history](#dataset-migration-transaction-history)
- [Namespaces](#dataset-migration-namespaces)
- [Mosaics](#dataset-migration-mosaics)
- [Second Layer Integrations](#dataset-migration-second-layer-integrations)
- [Exchanges Integrations](#dataset-migration-exchanges-integrations)

Each of these migrated modules and datasets will be described more in detail in sub-sections of this document under the section [Dataset Migrations](#dataset-migrations).

### Process Implications

Several points have to be taken into account about implications of the migration in both **legal** and **technical** domains. Each of these implications that are open for resolution will be described in a sub-section of the current section.

#### Legal implications

The proposed approaches for migration imply the creation of a potential taxable event. It is important to clear this point before migration can be planned correctly.

- Do we want our end-users to be affected with a taxable event ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
- Can/Should we avoid the creation of a taxable event ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
- Is the creation of a taxable event a **blocking** Point for migration ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>

Other reference documentation available here: [Tax Considerations for ICOs](https://nem2.slack.com/files/U9G1B8BAT/FJKB78FJA/tax-considerations-for-icos.pdf)

**Issue Resolution**: <span style="color: #f00;">Resolution to be described here.</span>

#### Technical implications / Release Technical Debt

During the process of migration, it is preferred that end-users **know exactly what they have to do** in order for the Catapult migration/release to be successful. For this, we should be defining important documentation and article references in this section, that will give end-users an overview of how the necessary steps for the upgrade can/should be taken.

Additionally, we will be providing an overview of the technical debt that accompanies the _Catapult release on Public Network_ grouped in the different Special Interest Groups as described in [nemtech/community](https://github.com/nemtech/community).

Following list may be re-defined over time, when decisions have been made on subsequent topics. Below is the list of **important tools and documentation for the Catapult Release on Public Network**.

- `catapult-service-bootstrap`: [Guide: Docker containers for Public Network Nodes](https://github.com/nemtech/catapult-service-bootstrap)
- `catapult-server`: [Building Instructions for Public Network Nodes](https://github.com/nemtech/catapult-server/blob/master/BUILDING.md)
- `catapult-rest`: [Guide: Run your own REST gateway for Public Network Nodes](https://github.com/nemtech/catapult-rest)
- `nem2-sdk-*`: [Guide: NEM2 TS/JS for Public Network Integrations](https://github.com/nemtech/nem2-sdk-typescript-javascript)
- `nem2-cli`: [Guide: NEM2 CLI for Public Network Integrations](https://github.com/nemtech/nem2-cli)
- `nem2-docs`: [Section: Catapult Public Network Integration](https://github.com/nemtech/nem2-docs)
- `nem2-e2e-tests`: [Testing: Usage with Public Network Nodes](https://github.com/nemtech/nem2-e2e-tests)
- `all-projects`: [Testing Clients/SDK/Docs: Usage with Public Network Nodes](https://github.com/nemtech)

Some of the listed **tools and documentation** may change due to decisions taken on subsequent topics. Also, some of the tools will require work assignment to permit usage with Public Network Nodes.

Below is the list of **technical debt for the Catapult Release on Public Network**.

- **#sig-api**: Permit Keccak hashing/derivation in _public key derivation_ and _signature creation algorithms_.
- **#sig-docs**: Needed resolution on [Possible Outcomes](#possible-outcomes) to publish list of _Guides for Migration_.
- **#sig-testing**: end-to-end testing must be available for Catapult releases to improve quality in release flow.

**Issue Resolution**: <span style="color: #0f0;">Integrations / Implementations to be finished by start of Q3 2019.</span>

### Dataset Migrations

This section describes the different datasets that have to be taken into account when migrating to Catapult technology. Each of the datasets available will be reviewed by asking the following questions:

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1?
2. will _not migrating dataset_ irreparably harm nem/catapult reputation?
3. will dataset be migrated ? (**Issue Resolution**)
4. will there be any legal implication to the migration of this dataset ?
5. will there be any technical debt introduction with the migration of this dataset ?

#### Dataset Migration: Account Data

Account data represents those datasets that are linked to **Accounts on the NEM blockchain Public Network** (MAIN_NET).

Following sub-sections identify datasets that are linked to an **Account** on the _NIS1_ network.

##### Multi-Signature Conversions

Siblings:
- [Multi-Signature Information](#multi-signature-information)
- [Modify Multisig Transaction](#modify-multisig-transaction)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
3. will _not migrating dataset_ feature irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Importance Delegation

Siblings:
- [Importance Transfer Transaction](#importance-transfer-transaction)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Multi-Signature Information

Siblings:
- [Multi-Signature Conversions](#multi-signature-conversions)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### XEM Balances

Siblings:
- [Dataset Migration: Namespaces](#dataset-migration-namespaces)
- [Dataset Migration: Mosaics](#dataset-migration-mosaics)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1?  <span style="color: #f00;">YES: people will prefer previous balances.</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Mosaic Balances

Siblings:
- [Dataset Migration: Namespaces](#dataset-migration-namespaces)
- [Dataset Migration: Mosaics](#dataset-migration-mosaics)
- [Register Namespace Transaction](#register-namespace-transaction)
- [Mosaic Definition Transaction](#mosaic-definition-transaction)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1?  <span style="color: #f00;">YES: people will prefer previous balances.</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Account Importance

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

#### Dataset Migration: Transaction History

The transaction history of the _NIS1_ network represents those datasets that are said to be **Transactions on the NEM blockchain Public Network**. Several types of transactions are available and some of them may require a migration.

Following sub-sections identify datasets that are linked to a **Transaction History** on the _NIS1_ network.

##### Transfer Transaction

Siblings:
- [Distribution (Transfers)](#distribution-transfers)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Modify Multisig Transaction

Siblings:
- [Multi-Signature Information](#multi-signature-information)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Importance Transfer Transaction

Siblings:
- [Account importance](#account-importance)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Register Namespace Transaction

Siblings:
- [Dataset Migration: Namespaces](#dataset-migration-namespaces)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Mosaic Definition Transaction

Siblings:
- [Dataset Migration: Mosaics](#dataset-migration-mosaics)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #f00;">YES, people may want to see previous balances.</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

#### Dataset Migration: Namespaces

The namespaces of the _NIS1_ network represents those datasets that are identified as **expirable Namespace registrations on the NEM blockchain Public Network**.

Following sub-sections identify datasets that are linked to a **Namespace** on the _NIS1_ network.

##### Root Namespaces

Siblings:
- [Register Namespace Transaction](#register-namespace-transaction)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Sub Namespaces

Siblings:
- [Register Namespace Transaction](#register-namespace-transaction)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Mosaics

Siblings:
- [Mosaic Definition Transaction](#mosaic-definition-transaction)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

#### Dataset Migration: Mosaics

The mosaics of the _NIS1_ network represents those datasets that are identified as **custom mosaics created on the NEM blockchain Public Network**.

Following sub-sections identify datasets that are linked to a **Mosaic** on the _NIS1_ network.

##### Balances

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Distribution (Transfers)

Siblings:
- [Transfer Transaction](#transfer-transaction)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Namespaces

Siblings:
- [Mosaic Definition Transaction](#mosaic-definition-transaction)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

#### Dataset Migration: Second Layer Integrations

The second layer integrations of the _NIS1_ network represents those datasets that are related to **data stored on the NEM blockchain Public Network**, including but not limited to: **Apostille configurations**, **Voting / Poll data**.

Following sub-sections identify datasets that are linked to **Second Layer Integrations** on the _NIS1_ network.

##### Apostille

Siblings:
- [Transfer Transaction](#transfer-transaction)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

##### Voting Data

Siblings:
- [Transfer Transaction](#transfer-transaction)

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #f00;">YES</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

#### Dataset Migration: Exchanges Integrations

The exchanges integrations of the _NIS1_ network represents those datasets that are related to **exchanges integrations of XEM or custom Mosaics on the NEM blockchain Public Network**.

Following sub-sections identify datasets that are linked to **Exchanges Integrations** on the _NIS1_ network.

##### XEM Buy / Sell Integrations

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #f00;">YES</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #f00;">YES</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

:warning: **Each exchange integration for XEM mosaics must be contacted for a clear resolution on whether _migration_ will be supported by work on their side or not**.

List of available XEM Buy / Sell Integrations:

- <span style="color: #f00;">Exchanges list to be determined.</span>

##### Custom Mosaics Buy / Sell Integrations

1. will _not migrating dataset_ make majority of users unhappy and/or prefer NIS1? <span style="color: #0f0;">NO</span>
2. will _not migrating dataset_ irreparably harm nem/catapult reputation? <span style="color: #0f0;">NO</span>
3. will dataset be migrated ? **Issue Resolution**: <span style="color: #f00;">NO</span>
4. will there be any legal implication to the migration of this dataset ? <span style="color: #0f0;">YES</span> / <span style="color: #f00;">NO</span>
5. will there be any technical debt introduction with the migration of this dataset ? <span style="color: #f00;">YES</span> / <span style="color: #0f0;">NO</span>

:warning: **Businesses who have issued custom mosaics on the NEM blockchain Public Network must be contacted in order to find a clear resolution on their future with the Catapult technology**.

### Technical Debt Introduction

During the process of decision making on the _Catapult release on Public Network_, it is possible that technical debt is introduced through any of the decisions/resolutions taken. In order to favoritize a smooth release, it is best that the introduced technical debt is planned/organized/described in this document accordingly.

As such, special interest groups will be listed with their **introduced technical debt** in the following table:

| SIG | Technical Debt Topic | Assigned ? | Blocking Topic ? |
| -:- | -:- | -:- | -:- |
| #sig-api | SDK TS/JS Keccak Implementation | :white_check_mark: | <span style="color: #0f0;">NO</span> |
| #sig-api | SDK Java Keccak Implementation | :stop_sign: | <span style="color: #0f0;">NO</span> |
| #sig-api | Docker instructions for Public Network Nodes | :stop_sign: | <span style="color: #0f0;">NO</span> |
| #sig-client | Migration tools | :stop_sign: | <span style="color: #0f0;">YES, need resolution [Possible Outcomes](#possible-outcomes)</span>
| #sig-docs | Guide for Public Network | :white_check_mark: | <span style="color: #f00;">YES, need resolution [Possible Outcomes](#possible-outcomes)</span>
| #sig-testing | End-to-end test suite | :white_check_mark: | <span style="color: #0f0;">NO</span> |
| catapult-server | Build instructions for Public Network Nodes | :stop_sign: | <span style="color: #0f0;">NO</span> |

## Backwards compatibility

As the Catapult software is a rewrite in a different software development language, it is not possible to provide with a simple update process. Backwards compatibility is being reviewed and researched and should be discussed in this document.

All backwards incompatible modules and features of the Catapult technology are being evaluated in order find clear resolutions on the topics _before migration can happen_.

:warning: **More information will be described in this section when issues have been resolved.**

## References

- [`NIS1`: NemProject/nem.core](https://github.com/NemProject/nem.core)
- [`Catapult`: nemtech/catapult-server](https://github.com/nemtech/catapult-server)
- [catapult-service-bootstrap](https://github.com/nemtech/catapult-service-bootstrap)
- [catapult-server](https://github.com/nemtech/catapult-server/blob/master/BUILDING.md)
- [catapult-rest](https://github.com/nemtech/catapult-rest)
- [nem2-sdk-typescript-javascript](https://github.com/nemtech/nem2-sdk-typescript-javascript)
- [nem2-cli](https://github.com/nemtech/nem2-cli)
- [nem2-docs](https://github.com/nemtech/nem2-docs)
- [nem2-e2e-tests](https://github.com/nemtech/nem2-e2e-tests)
- [@nemtech](https://github.com/nemtech)
- [nemtech/community](https://github.com/nemtech/community)
- [Tax Considerations for ICOs](https://nem2.slack.com/files/U9G1B8BAT/FJKB78FJA/tax-considerations-for-icos.pdf)

## History

| **Date**     | **Version**   |
| ------------ | ------------- |
| May 10 2019 | Initial Draft |
