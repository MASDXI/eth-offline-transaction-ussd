---
eip: XXXX
title: Pay with USSD
description: Offline payment transactions via USSD.
author: sirawt (@MASDXI), Paramet Kongjaroen (@parametprame), et al.
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
In scenarios with limited or unreliable internet access, traditional digital payment methods may not be feasible. Unstructured Supplementary Service Data (USSD) provides a vital solution by enabling offline transactions like payments, transfers, and balance inquiries without requiring internet connectivity. Its simplicity and broad compatibility with basic mobile devices and Electronic Draft Capture (EDC) device make USSD an essential tool for mobile payments, particularly in underserved areas, supporting financial inclusion and broader access to digital financial services.

Use cases for offline payments including
- Credit
- e-Money
- Insurance
- Loyalty program
- Retail Central Bank Digital Currency (rCBDC)

## Specification

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “NOT RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119 and RFC 8174.


> **MUST** support to pay with `address` **OPTIONAL** `ens`,`phone number`, `email`, `username` or `unique Id`  
not covering transaction to smart contract with USSD cause application **MAY** update the data frequently.  
mapped phone number to public address see: https://github.com/camaraproject/BlockchainPublicAddress  


### Partial-sync approach

Partially synchronizing with the blockchain network to ensure the client device maintains the latest `nonce`. Upon successfully processing a transaction, the system will return the updated `nonce` and `balance` to the user, allowing for continued offline operations with reliable state information.

### Sync-less approach

Explores sending signed transactions to a forwarder without requiring prior synchronization of the `nonce`, while ensuring resistance to replay attacks even in the absence of direct synchronization with the blockchain network.

> NOTE: For both partial-sync and sync-less approach with custodian wallet can use ERC-681 -->

### USSD structure

>TODO

## Rationale

> TODO

## Backwards Compatibility

No backward compatibility issues found.

## Reference Implementation

> TODO example implementation source code  
> some useful source see:   
> https://github.com/krypt007/kotanipay-USSD.git
> https://docs.oracle.com/communications/F83448_01/doc.1500/ccc_ussd_gw_tg.pdf  
> https://help.webexconnect.io/docs/sending-and-receiving-sms-using-sandbox  
> https://github.com/SedemQuame/fido-ussd-app  

## Security Considerations

### USSD Weak Cryptography (Quantum Resistance)

> TODO short explain  
> potential solution see: https://www.itu.int/dms_pub/itu-t/opb/tut/T-TUT-PROTO-2021-PDF-E.pdf


### USSD Replay Attacks

> TODO short explain

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).