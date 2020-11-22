# NIP-16 Annex 1: Components

## symbol-transaction-icon

### Attributes

| Parameter | Possible value(s) |
| --------- | ------------- |
| `type` | `account-link`, `aggregate`, `lock`, `metadata`, `mosaic`, `multisig`, `namespace`, `restriction`, `transfer`, `incoming`, `outgoing` |

### User stories

| Step | Title | Condition(s) | Story |
| ---- | ----- | ------------ | ----- |
| 1 | **User can see a transaction icon** | N/A | Should contain an icon depending on the transaction type. |
| 2 | **User can see an error icon** | N/A | Should contain an error icon. |

### Actions 

- **Given a valid transaction type**
  * An icon specific to said transaction type should be displayed.

- **Given an invalid transaction type**
  * An error icon should be displayed.

## symbol-node-health-icon

### Attributes

| Parameter | Possible value(s) |
| --------- | ------------- |
| `node-url` | `http://localhost:3000` |

### User stories

| Step | Title | Condition(s) | Story |
| ---- | ----- | ------------ | ----- |
| 1 | **User can see a node health icon** | N/A | Should contain an icon depending on the returned health of the network node. |
| 2 | **User can see an error icon** | N/A | Should contain an error icon. |

### Actions 

- **Given a node URL for a network node in good health**
  * An icon that reflects successful connection / health ("green") should be displayed.

- **Given a node URL for a network node in bad health**
  * An icon that reflects erroneous connection / health  ("red") should be displayed.

- **Given an invalid node URL**
  * An error icon should be displayed.

## symbol-signatures-progressbar

### Attributes

| Parameter | Possible value(s) |
| --------- | ------------- |
| `transaction` | `{type: 16724, signature: '...', recipientAddress: '...'}` |
| `graph` | `{multisigAccounts: {0: {cosignatories: ['...', '...'], ...}, ...}}` |

### User stories

| Step | Title | Condition(s) | Story |
| ---- | ----- | ------------ | ----- |
| 1 | **User can see progress of signatures** | N/A | Should contain a progress bar reflecting progress of total needed signatures for a Symbol transaction. |
| 2 | **User can see completion icon** | N/A | Should contain an icon reflecting the completion of signatures for a Symbol transaction. |
| 3 | **User can see an error icon** | N/A | Should contain an error icon. |

### Actions 

- **Given a transaction which requires more than one signature**
  * A progress bar should be displayed which reflects the progressing state of signatures. 

- **Given a transaction which doesn't require more than one signature**
  * An icon should be displayed which reflects the completion of signatures for said transaction.

- **Given an invalid transaction**
  * An error icon should be displayed.

- **Given an invalid multi-signature account graph**
  * An error icon should be displayed.

## symbol-transaction-schema

TBD

## Credits

| Name | Github | Role |
| --- | --- | --- |
| Grégory Saive | @evias | Author |
| Oleh Makarenko | @OlegMakarenko | Contributor |

