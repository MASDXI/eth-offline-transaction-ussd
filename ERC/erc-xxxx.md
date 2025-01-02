---
eip: XXXX
title: Pay with USSD
description: Offline payment transactions via USSD.
author: sirawt (@MASDXI)
discussions-to: https://ethereum-magicians.org/t/eip-xxxx/
status: Draft
type: Standards Track
category: ERC
created: yyyy-mm-dd
requires: xxx
---

<!-- 
# requires: 155, 137, 191, 681, 712 assuming
something similar to the ERC-7798: Tap to pay?
-->

## Motivation

> TODO

Use cases offline payment

- Credit
- e-Money
- Insurance
- Loyalty program
- Retail Central Bank Digital Currency (rCBDC)

## Specification

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “NOT RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119 and RFC 8174.

<!-- 
**MUST** support to pay with `address` *OPTIONAL* `ens`,`phone number`, `email`, `username` or `unique Id`
not covering transaction to smart contract with USSD cause application **MAY** update the data frequently
mapped phone number to public address see: https://github.com/camaraproject/BlockchainPublicAddress 
-->

### Partial-sync approach

Partially synchronizing with the blockchain network to ensure the client device maintains the latest `nonce`. Upon successfully processing a transaction, the system will return the updated `nonce` and `balance` to the user, allowing for continued offline operations with reliable state information.

### Sync-less approach

Explores sending signed transactions to a forwarder without requiring prior synchronization of the `nonce`, while ensuring resistance to replay attacks even in the absence of direct synchronization with the blockchain network.

<!-- NOTE: For both partial-sync and sync-less approach with custodian wallet can use ERC-681 -->

## Rationale

> TODO

## Backwards Compatibility

> TODO

## Reference Implementation

> TODO example implementation source code

## Security Considerations

### USSD Weak Cryptography (Quantum Resistance)

> TODO short explain

### USSD Replay Attacks

> TODO short explain

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).