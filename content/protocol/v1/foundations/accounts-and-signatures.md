---
title: Accounts and signatures
description: Account identity, address representation, and authorization rules in TrueOpen V1.
---

# Accounts and signatures

TrueOpen V1 uses one account family for users, operators, service keys, and Builders. A role does not create a separate address space.

## Account identity

V1 account keys use the secp256k1 curve with Ethereum-compatible address derivation. An address is the last 20 bytes of `keccak256(X || Y)`, where `X || Y` is the 64-byte uncompressed public key without the `0x04` prefix.

The standard wallet derivation path begins at:

```text
m/44'/60'/0'/0/0
```

Additional account indexes may be derived, but the chain only observes the resulting 20-byte address. The account public key is stored as a compressed 33-byte secp256k1 point.

## Address forms

TrueOpen account inputs use canonical lowercase Bech32:

| Use | Prefix |
|---|---|
| Account, User, operator, service key, Builder | `trueopen` |
| Validator operator | `trueopenvaloper` |
| Validator consensus identity | `trueopenvalcons` |

An account address and its validator-operator representation may encode the same 20 bytes with different prefixes. Validator consensus addresses are derived separately from consensus keys.

Public messages, queries, and genesis records must not accept `0x` account input. Wallets may display or convert an equivalent EVM address, but conversion belongs at the client boundary. The chain rejects non-canonical Bech32, mixed case, unexpected prefixes, and decoded lengths other than 20 bytes.

## Transaction authorization

V1 supports two transaction-signing paths:

1. **SDK direct signing** signs a deterministic protobuf `SignDoc` digest and carries a canonical 64-byte `R || S` signature.
2. **Web3 EIP-712 signing** signs the registered transaction domain and carries a recoverable 65-byte `R || S || V` signature.

The transaction extension option selects the path. Validators must not infer the path from the message type, key type, memo, local configuration, or signature length. Unsupported, repeated, or mixed extension options are rejected.

Both paths bind the transaction body, authorization information, chain identity, account number, and sequence. Signatures must be canonical and low-S. A signer cannot use transaction encoding ambiguity to authorize different actions on different nodes.

## Orders are a separate signing domain

A signed Task order is not a Cosmos transaction. It uses a distinct EIP-712 order domain so a transaction signature cannot be replayed as an order or vice versa.

Before submitting an offline signed order, a User must have successfully created a Session using an on-chain transaction. This ensures the account and its public key already exist. Order validation must fail if the account is missing, has no public key, uses an unsupported key type, or the recovered signer differs from the order's User address.

Recovered keys are used for comparison only. Validation must never create or modify an account from a recovered signature.

## Key separation

An operator address is the stable economic identity for a Builder or Cortex Node. A service key is a replaceable online authorization key. Bonds, earnings, penalties, Task ownership, and claims remain attached to the operator when its service key changes.

Validator consensus keys and bridge-signing keys have separate security purposes and must not be reused as account or service keys.
