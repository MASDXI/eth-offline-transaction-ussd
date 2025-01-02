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
---

<!-- 
requires: 155, 137, 191, 681, 712 assuming
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

## Partial-sync approach

Partially synchronizing with the blockchain network to ensure the client device maintains the latest `nonce`, `gasPrice`, and other. Upon successfully processing a transaction, the system will return the updated `nonce`, `balance`, and other to the user, allowing for continued offline operations with reliable state information.

### Schema

- sendTransaction

``` json
"payload": {
    "chainId": "<HEX_VALUE>",
    "recipient": "<STRING>",
    "value": "<HEX_VALUE>",
    "currency": "<STRING>",
    "signedTransaction": "<HEX_VALUE>"
}
```

``` json
"response": {
    "nonce": "<HEX_VALUE>",
    "balance": "<HEX_VALUE>",
    "currency": "<STRING>",
    "transactionHash": "<HEX_STRING>"
}
```

When transferring native token the `currency` key **MUST** be `0x000...000` or `null`.  
The callback **MUST** return be returns the latest `nonce`, `balance` of `currency` and a `transactionHash` 
back to the `sender` if transaction successfully otherwise response `error` message.

- getBalance
  
``` json
"payload": {
    "chainId": "<HEX_VALUE>",
    "currency": "<STRING>",
}
```

``` json
"response": {
    "balance": "<HEX_VALUE>",
    "currency": "<STRING>",
}
```

When get balance of native token the `currency` key **MUST** be `0x000...000` or `null`.
The callback **MUST** return be return the latest `balance` of given `currency`.
The currency **SHOULD** be the token contract `address` or token `symbol`.

> **MUST** support to pay with `address` **OPTIONAL** `ens`,`phone number`, `email`, `username` or `unique Id`  
not covering transaction to smart contract with USSD cause application **MAY** update the data frequently.  

- getBlockchainState

``` json
"payload": {
    "chainId": "<HEX_VALUE>",
}
```

``` json
"response": {
    "nonce": "<HEX_VALUE>",
    "gasPrice": "<STRING>",
    // other e.g.; EIP-1559
}
```

- getTransactionByHash
  
``` json
"payload": {
    "chainId": "<HEX_VALUE>",
    "transactionHash": "<HEX_VALUE>"
}
```

``` json
"response": {
    // transaction information see eth_getTransactionByHash and eth_getTransactionReceipt
}
```

### Sync-less approach

Explores sending signed transactions to a forwarder without requiring prior synchronization of the `nonce`, and other, while ensuring resistance to replay attacks even in the absence of direct synchronization with the blockchain network.

<!--  Custodian: ERC-681 URL as payload? -->
<!--  Non-Custodian: Account-Abstraction potentially solve? -->

## Rationale

<!-- TODO -->

## Backwards Compatibility

No backward compatibility issues found.

## Reference Implementation

<!-- TODO -->
<!-- TODO example implementation source code   -->
<!-- some useful source see:    -->
<!-- https://github.com/krypt007/kotanipay-USSD.git -->
<!-- https://docs.oracle.com/communications/F83448_01/doc.1500/ccc_ussd_gw_tg.pdf   -->
<!-- https://help.webexconnect.io/docs/sending-and-receiving-sms-using-sandbox   -->
<!-- https://github.com/SedemQuame/fido-ussd-app   -->
<!-- Mapped phone number to public address see: https://github.com/camaraproject/BlockchainPublicAddress   -->
<!-- ERC-7798 see: https://hackmd.io/VyxIMlk1SvCOpBpS6a_2uA?both   -->

## Security Considerations

### USSD Weak Cryptography

<!-- TODO  -->
<!-- potential quantum resistance solution see: https://www.itu.int/dms_pub/itu-t/opb/tut/T-TUT-PROTO-2021-PDF-E.pdf -->


### USSD Replay Attacks

<!-- TODO -->

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).