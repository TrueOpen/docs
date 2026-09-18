---
title: Validators
description: Consensus, governance, and security responsibilities of a TrueOpen Validator.
---

# Validators

Validators operate the chain's consensus and deterministic application state machine. Their role makes accepted protocol state available to Users, Builders, and Cortex Nodes.

## Responsibilities

- Validate transactions and execute the versioned state-transition rules consistently.
- Verify the required proposer VRF beacon and maintain the separately registered VRF key.
- Maintain consensus-key custody and distinguish it from account, service, VRF, and bridge-signing keys.
- Participate in the governed Validator-set and upgrade processes.
- Follow bridge signer coordination and freeze controls when membership changes affect the canonical asset route.

Consensus stake and service liability are separate. Running a Validator does not automatically provide inference or verification capacity, and ordinary service faults do not debit consensus stake.

## Operating boundaries

Operators need synchronized chain state, durable node storage, protected signing infrastructure, and an upgrade process compatible with the active network version. Public installation commands, genesis values, and network endpoints will be documented with supported releases.

Read [Randomness](../protocol/v1/foundations/randomness.md), [Governance](../protocol/v1/governance.md), and [Cross-chain assets](../protocol/v1/cross-chain-assets.md) before operating the corresponding duties.
