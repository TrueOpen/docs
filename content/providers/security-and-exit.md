---
title: Security and exit
description: Protect provider keys and data, rotate authorization, drain duties, and withdraw safely.
---

# Security and exit

A compute provider signs financially accountable material and handles potentially sensitive Task data. Key custody, data handling, and exit procedures are part of correct operation.

## Isolate keys

- Keep the operator key offline or behind a restricted signing process.
- Give the online Cortex process access only to the current service key.
- Never provide private keys to the adapter or model runtime.
- Give the signer canonical digests rather than prompts, outputs, or evidence bodies.
- Do not reuse Validator consensus, operator, service, or bridge-signing keys.

A compromised service key exposes online Task actions but must not permit direct ServiceBond withdrawal or reward claims.

## Protect transport and Task data

Authenticate and encrypt every non-local connection to chain endpoints, Nexus, and the model adapter. Validate Builder descriptors and endpoint identity before transferring Task data. Secure transport does not prove that a message is current or correctly bound to a Task.

V1 Task data is not end-to-end encrypted from Task Builders. Restrict filesystem and process access, omit sensitive content from normal logs, store evidence under explicit retention controls, sanitize diagnostic exports, and delete Task data only after chain cleanup conditions are satisfied.

## Rotate the service key

1. Stop new handraises.
2. Drain or finish accepted duties.
3. Confirm no required signed submission remains pending.
4. Preserve continuing evidence obligations.
5. Use the operator account to authorize the new key with proof of possession.
6. Confirm the new binding on-chain before restarting work.

The replacement is atomic. The old service key cannot remain as a fallback submission key.

## Exit the network

Exiting is not an immediate withdrawal:

1. Stop new Profile support and handraises.
2. Drain Profiles without abandoning accepted Tasks.
3. Start unbonding.
4. Continue monitoring Tasks, challenges, penalties, and evidence retention.
5. Wait for liability and the unbonding period to close.
6. Withdraw the remaining releasable ServiceBond.

The provider remains accountable during unbonding. Existing slashable responsibility is applied before withdrawal. See the [Cortex Node lifecycle](node-lifecycle.md) and [Staking and penalties](../protocol/v1/service-participation/staking-and-penalties.md).
