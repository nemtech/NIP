# NIP 2 - Transaction URI Scheme

```
    NIP: 2
    Title: URI Scheme
    Author: David Garcia <dgarcia360@outlook.com>
    Discussions-To: #sig-client
    Comments-URI: https://github.com/nemtech/NIP/issues/6
    Status: Draft
    Type: Standards Track
    Layer: Library
    Created: 2018-12-18
    License: Apache 2.0
    License-Code: Apache-2.0
```

## Table of contents

- [Introduction](#introduction)
- [Specification](#specification)
  * [Transaction URI scheme](#transaction-uri-scheme)
  * [Webhook payload](#webhook-payload)
  * [Integration sequence diagram](#integration-sequence-diagram)
- [Motivation](#motivation)
- [Design Decisions](#design-decisions)
  * [Standard Protocol](#standard-protocol)
  * [Lightweight library](#lightweight-library)
  * [WebHooks](#webhooks)
- [Implementation](#implementation)
- [Backwards compatibility](#backwards-compatibility)
- [Contributors](#contributors)
- [History](#history)

## Introduction

The signature and announcement of transactions should always occur on the client-side without sharing private keys with third-party applications.
NIP-0002 defines a URI scheme to serve transactions ready to be signed. 

## Motivation

Applications using Symbol will expect users to announce transactions to the network.  Imagine that Alice is purchasing a ticket for a concert. She has selected a ticket on the vendor's website, and at this time she is ready to pay. The website uses Symbol in the background, being the payment a regular transfer transaction from Alice's account. The experience shows from apps built on NIS1 that one of the following solutions would be used to accept the payment.

**A) The ticket vendor offers a client-side app**

Alice downloads the ticket vendor open-source app in local to sign a transaction. To make the process secure, Alice should inspect the downloaded code and check that:
The transaction is being constructed and serialized as expected.
The private key used is not being copied. 
From the UX point of view, having to inspect the code to see what the app does is far from ideal and not secure, since private keys should never be shared.

**B) The customer sends a transaction to a determined address**

In this scenario, Alice has to define the transaction manually in the NEM wallet. This approach looks safer than A), but introduces the possibility of making typing mistakes when defining the address, the message, or even choosing the transaction type. Besides, the customer spends additional time during the process as it has to set the transaction manually.

**C) The customer scans a QR code using a phone wallet**
 
This approach looks more usable and less error-prone, but it is not complete. Alice must use two different devices to announce transactions, one of them being necessarily a mobile phone.

Furthermore, Symbol comes with different types of transactions, and the [current QR standard](https://github.com/NemProject/nem-library-ts/blob/master/src/services/QRService.ts#L56) only handles transfer transactions.

The aforementioned downsides encourage looking for other alternatives. Defining a [standard URI scheme](https://logbooksocial.github.io/blog/development/2018/11/16/ux-i.html) and supporting it in trusted environments such as the official wallets would allow users to sign transactions from applications without having to define them manually, own the second device, nor inspect the source code.

## Specification

### Transaction URI scheme

``web+symbol://transaction?data=<data>&generationHash=<generationHash>&nodeUrl=<endpoint>&webhookUrl=<webhook>``

|**Parameter**      | **Description** | **Example**|
| ----------------- | ------------- | ------------- |
| data*   | The transaction payload [serialized in hexadecimal](https://nemtech.github.io/api.html#serialization) form.| A700...4000000 |
| generationHash | The [network generation hash seed](https://github.com/nemtech/catapult-server/blob/master/resources/config-network.properties). Identifies a network uniquely. | 57F7DA205008026C776CB6AED843393F04CD458E0AA2D9F1D5F31A402072B2D6 |
| nodeUrl | The preferred Rest Gateway URL to announce the transaction. The application could have another strategy to select the endpoint, omitting this field. | http://localhost:3000 |
| webhookUrl | The application can provide a URL that identifies the action uniquely. When the transaction is announced from the secure environment, this will send an HTTP POST [payload](#webhook-payload) to the URL provided. | https://myapp.extension/webhook/10758F6

### Webhook payload

**HTTP Method**: POST

|**Parameter**          | **Description** | **Example**|
| ----------------------| ------------------ | ------------- |
| action*               | The event being tracked. | AnnounceTransaction |
| data.hash*            | The hash of the transaction announced. | 1F05...7597451|
| data.signerPublicKey* | The public key of the transaction signer. | EFF9...227CE85|

**Example**
```
{
  "action": "AnnounceTransaction",
  "data": {
      "hash": "1F05E54DB40DC7C12262F3250F3A428EE6FEC7150DFACB67566B6DD607597451", 
      "signerPublicKey":"EFF9BC7472263D03EF6362B1F200FD3061BCD1BABE78F82119FB88811227CE85"
  }
}
```
*required field.

### Integration sequence diagram

<img src=./nip-0002/process.png>


## Design Decisions

### Standard Protocol

A URI scheme enables the communication between external applications and Symbol wallets. URIs can be recognized by desktop and [mobile wallets](https://developer.apple.com/documentation/uikit/core_app/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app), launching the wallet app with the transaction ready to be signed. 

The protocol adds ``web+`` add the beginning of the scheme due to a [security requirement for Firefox](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/registerProtocolHandler).

### Lightweight library

Creating a URI scheme library that handles custom transaction serialization is expensive because of the possible permutations of maintaining a library per language and the chance of having new transaction types in the future.

A convenient solution partially exists, making available the internal SDK classes to serialize and deserialize transactions. A lightweight library can be created instead to parse the Transaction to URI format and vice versa. This library should not be aware of how transactions are serialized/deserialized, but only how the URI string is formatted from a ``Transaction`` object.

Using the internal Symbol SDK functions to serialize transactions, we achieve the following properties:

* The scheme definition will not change if there is the need to add new types of transactions. 
* Multiple transactions can be announced together using aggregate transactions.

### Webhooks

A wallet app triggered by the URI scheme has to notify back the application after the user confirms announcing the transaction.
The wallet notifies the application sending a **HTTP POST** request to the URL specified in the ``webhook`` parameter with the following [payload](#webhook-payload).

The application is responsible for monitoring the blockchain to check if the transaction announced has been confirmed.

## Implementation

- [x] Changes required in the SDK: [Expose serialization methods](https://github.com/nemtech/symbol-sdk-typescript-javascript/issues/56)

- [x] Implementation: [symbol-uri-scheme](https://github.com/nemfoundation/symbol-uri-scheme)

- [x] Integration: [symbol-cli](https://github.com/nemtech/symbol-cli)

- [ ] Integration: [symbol-desktop-wallet](https://github.com/nemgroup/symbol-desktop-wallet)

- [ ] Integration: symbol-mboile-wallet

## Backwards compatibility

NIS1 does not have a known standard URI scheme.

## Contributors

Special thanks to [@aleixmorgadas](https://github.com/aleixmorgadas), [@dexterslabor](https://github.com/dexterslabor), [@9zero](https://github.com/9zero), [@jontey](https://github.com/jontey), [@rg911](https://github.com/rg911), [@decentraliser](https://github.com/decentraliser) for contributing actively to improve this NIP.

## History

| **Date**          | **Version**   |
| ----------------- | ------------- |
| December 18 2018  | Initial Draft |
| March    24 2020  | 0.4.3         |
