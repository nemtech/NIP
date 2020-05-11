# NIP-13 Annex 1: Reason Codes

In an attempt to make the token holder experience better, the provided `canTransfer` function MUST return a _reason byte code_ on success or failure based on the NIP-13 application-specific status codes specified in below table.

| Code | Reason | Failure |
| --- | --- | --- |
| **`0x0*` Generic Failure Codes** | | |
| `0x00` | Failure | `Failure_Generic` |
| `0x01` | Success | `Success_Generic` | 
| `0x02` | Awaiting Others | `Info_Awaiting_Parties` | 
| `0x03` | Accepted | `Success_Accepted` |
| `0x04` | Lower Limit or Insufficient | `Failure_Lower_Limit` |
| `0x05` | Receiver Action Requested | `Info_Receiver_Action_Requested` |
| `0x06` | Upper Limit | `Failure_Upper_Limit` |
| `0x07` | _Currently unspecified_ | _Currently unspecified_ |
| `0x08` | _Currently unspecified_ | _Currently unspecified_ |
| `0x09` | _Currently unspecified_ | _Currently unspecified_ |
| `0x0A` | _Currently unspecified_ | _Currently unspecified_ |
| `0x0B` | _Currently unspecified_ | _Currently unspecified_ |
| `0x0C` | _Currently unspecified_ | _Currently unspecified_ |
| `0x0D` | _Currently unspecified_ | _Currently unspecified_ |
| `0x0E` | _Currently unspecified_ | _Currently unspecified_ |
| `0x0F` | Informational or Metadata | `Info_Generic` |
| **`0x1*` Permission and Control** | | |
| `0x10` | Disallowed or Stop | `Failure_Disallowed` |
| `0x11` | Allowed or Go | `Success_Allowed` |
| `0x12` | Awaiting Other’s Permission | `Info_Awaiting_Parties_Permission` |
| `0x13` | Permission Requested | `Success_Permission_Requested` |
| `0x14` | Too Open / Insecure | `Failure_Insecure_Action` |
| `0x15` | Needs Your Permission or Request for Continuation | `Failure_Needs_Permission` |
| `0x16` | Revoked or Banned | `Failure_Permission_Revoked` |
| `0x17` | _Currently unspecified_ | _Currently unspecified_ |
| `0x18` | Not Applicable to Current State | `Failure_Permission_Not_Applicable` |
| `0x19` | _Currently unspecified_ | _Currently unspecified_ |
| `0x1A` | _Currently unspecified_ | _Currently unspecified_ |
| `0x1B` | _Currently unspecified_ | _Currently unspecified_ |
| `0x1C` | _Currently unspecified_ | _Currently unspecified_ |
| `0x1D` | _Currently unspecified_ | _Currently unspecified_ |
| `0x1E` | _Currently unspecified_ | _Currently unspecified_ |
| `0x1F` | Permission Details or Control Conditions | `Info_Permission_Details` |
| **| `0x2*` Find, Inequalities and Ranges** | | |
| `0x20` | Not Found, Unequal, or Out of Range | `Failure_Not_Found` |
| `0x21` | Found, Equal or In Range | `Success_Found` |
| `0x22` | Awaiting Match | `Info_Awaiting_Match` |
| `0x23` | Match Request Sent | `Success_Match_Request_Sent` |
| `0x24` | Below Range or Underflow | `Failure_Below_Range` |
| `0x25` | Request for Match | `Info_Request_For_Match` |
| `0x26` | Above Range or Overflow | `Failure_Above_Range` |
| `0x27` | _Currently unspecified_ | _Currently unspecified_ |
| `0x28` | Duplicate, Conflict, or Collision | `Failure_Duplicate_Conflict` |
| `0x29` | _Currently unspecified_ | _Currently unspecified_ |
| `0x2A` | _Currently unspecified_ | _Currently unspecified_ |
| `0x2B` | _Currently unspecified_ | _Currently unspecified_ |
| `0x2C` | _Currently unspecified_ | _Currently unspecified_ |
| `0x2D` | _Currently unspecified_ | _Currently unspecified_ |
| `0x2E` | _Currently unspecified_ | _Currently unspecified_ |
| `0x2F` | Matching Meta or Info | `Info_Matching_Meta` |
| **`0x3*` Negotiation and Governance** | | |
| `0x30` | Sender Disagrees or Nay | `Failure_Sender_Agreement` |
| `0x31` | Sender Agrees or Yea | `Success_Sender_Agreement` |
| `0x32` | Awaiting Ratification | `Info_Awaiting_Ratification` |
| `0x33` | Offer Sent or Voted | `Success_Offer_Sent`<br />`Success_Voted` |
| `0x34` | Quorum Not Reached | `Failure_Quorum_Not_Reached` |
| `0x35` | Receiver’s Ratification Requested | `Info_Receiver_Ratification_Requested` |
| `0x36` | Offer or Vote Limit Reached | `Failure_Offer_Limit_Reached`<br />`Failure_Vote_Limit_Reached` |
| `0x37` | _Currently unspecified_ | _Currently unspecified_ |
| `0x38` | Already Voted | `Failure_Already_Voted` |
| `0x39` | _Currently unspecified_ | _Currently unspecified_ |
| `0x3A` | _Currently unspecified_ | _Currently unspecified_ |
| `0x3B` | _Currently unspecified_ | _Currently unspecified_ |
| `0x3C` | _Currently unspecified_ | _Currently unspecified_ |
| `0x3D` | _Currently unspecified_ | _Currently unspecified_ |
| `0x3E` | _Currently unspecified_ | _Currently unspecified_ |
| `0x3F` | Negotiation Rules or Participation Info | `Info_Negotiation_Rules` |
| **`0x4*` Availability and Time** | | |
| `0x40` | Unavailable | `Failure_Unavailable` |
| `0x41` | Available | `Success_Available` |
| `0x42` | Paused | `Info_Paused` |
| `0x43` | Queued | `Info_Queued` |
| `0x44` | Not Available Yet | `Failure_Not_Available_Yet` |
| `0x45` | Awaiting Your Availability | `Info_Awaiting_Own_Availability` |
| `0x46` | Expired | `Failure_Expired` |
| `0x47` | _Currently unspecified_ | _Currently unspecified_ |
| `0x48` | Already Done | `Failure_Already_Done` |
| `0x49` | _Currently unspecified_ | _Currently unspecified_ |
| `0x4A` | _Currently unspecified_ | _Currently unspecified_ |
| `0x4B` | _Currently unspecified_ | _Currently unspecified_ |
| `0x4C` | _Currently unspecified_ | _Currently unspecified_ |
| `0x4D` | _Currently unspecified_ | _Currently unspecified_ |
| `0x4E` | _Currently unspecified_ | _Currently unspecified_ |
| `0x4F` | Availability Rules or Info (ex. time since or until) | `Info_Availability_Rules` |
| **`0x5*` Tokens, Funds and Finance** | | |
| `0x50` | Transfer Failed | `Failure_Transfer` |
| `0x51` | Transfer Successful | `Success_Transfer` |
| `0x52` | Awaiting Payment From Others | `Info_Awaiting_Parties_Payment` |
| `0x53` | Hold or Escrow | `Info_Hold`<br />`Info_Escrow` |
| `0x54` | Insufficient Funds | `Failure_Insufficient_Funds` |
| `0x55` | Funds Requested | `Success_Funds_Requested` |
| `0x56` | Transfer Volume Exceeded | `Failure_Transfer_Volumn_Exceeded` |
| `0x57` | _Currently unspecified_ | _Currently unspecified_ |
| `0x58` | Funds Not Required | `Failure_Funds_Not_Required` |
| `0x59` | _Currently unspecified_ | _Currently unspecified_ |
| `0x5A` | _Currently unspecified_ | _Currently unspecified_ |
| `0x5B` | _Currently unspecified_ | _Currently unspecified_ |
| `0x5C` | _Currently unspecified_ | _Currently unspecified_ |
| `0x5D` | _Currently unspecified_ | _Currently unspecified_ |
| `0x5E` | _Currently unspecified_ | _Currently unspecified_ |
| `0x5F` | Token or Financial Information | `Info_Token_Information` |
| **`0x6*` Currently unspecified** | | |
| **`0x7*` Currently unspecified** | | |
| **`0x8*` Currently unspecified** | | |
| **`0x9*` Currently unspecified** | | |
| **`0xA*` Application-specific Codes** | | |
| `0xA0` | App-Specific Failure | `Failure_App_Generic` |
| `0xA1` | App-Specific Success | `Success_App_Generic` |
| `0xA2` | App-Specific Awaiting Others | `Info_App_Awaiting_Parties` |
| `0xA3` | App-Specific Acceptance | `Info_App_Acceptance` |
| `0xA4` | App-Specific Below Condition | `Info_App_Conditions` |
| `0xA5` | App-Specific Receiver Action Requested | `Info_App_Received_Action_Requested` |
| `0xA6` | App-Specific Expiry or Limit | `Failure_App_Expiry`<br />`Failure_App_Limit` |
| `0xA7` | _Currently unspecified_ | _Currently unspecified_ |
| `0xA8` | App-Specific Inapplicable Condition | `Failure_App_Inapplicable_Condition` |
| `0xA9` | _Currently unspecified_ | _Currently unspecified_ |
| `0xAA` | _Currently unspecified_ | _Currently unspecified_ |
| `0xAB` | _Currently unspecified_ | _Currently unspecified_ |
| `0xAC` | _Currently unspecified_ | _Currently unspecified_ |
| `0xAD` | _Currently unspecified_ | _Currently unspecified_ |
| `0xAE` | _Currently unspecified_ | _Currently unspecified_ |
| `0xAF` | App-Specific Meta or Info | `Info_App_Generic` |
| **`0xB*` Currently unspecified** | | |
| **`0xC*` Currently unspecified** | | |
| **`0xD*` Currently unspecified** | | |
| **`0xE*` Encryption, Identity and Proofs** | | |
| `0xE0` | Decrypt Failure | `Failure_Decryption` |
| `0xE1` | Decrypt Success | `Success_Decryption` |
| `0xE2` | Awaiting Other Signatures or Keys | `Info_Awaiting_Parties_Signatures` |
| `0xE3` | Signed | `Success_Signed` |
| `0xE4` | Unsigned or Untrusted | `Info_Unsigned_Untrusted` |
| `0xE5` | Signature Required | `Info_Signature_Required` |
| `0xE6` | Known to be Compromised | `Info_Known_To_Be_Compromised` |
| `0xE7` | _Currently unspecified_ | |
| `0xE8` | Already Signed or Not Encrypted | `Failure_Already_Signed` |
| `0xE9` | _Currently unspecified_ | |
| `0xEA` | _Currently unspecified_ | |
| `0xEB` | _Currently unspecified_ | |
| `0xEC` | _Currently unspecified_ | |
| `0xED` | _Currently unspecified_ | |
| `0xEE` | _Currently unspecified_ | |
| `0xEF` | Cryptography, ID, or Proof Metadata | `Info_Cryptography`<br />`Info_Metadata_Proof` |

Source: [EIP#1066 `EIP 1066: Status Codes`][eip-1066]

## Credits

| Name | Github | Role |
| --- | --- | --- |
| Brooklyn Zelenka, Tom Carchrae, Gleb Naumenko | EIP-1066 | EIP-1066 |
| Grégory Saive | @evias | Contributor |

[eip-1066]:https://eips.ethereum.org/EIPS/eip-1066
