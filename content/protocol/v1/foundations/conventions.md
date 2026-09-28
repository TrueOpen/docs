---
title: Protocol conventions
description: Normative language, sources of authority, versioning, and failure behavior in TrueOpen V1.
---

# Protocol conventions

This documentation describes consensus and participant behavior for TrueOpen V1. Versioned rule pages are authoritative. Design explanations, operator guides, and the numbered Task stage walkthroughs illustrate those rules; their location within a protocol version does not make them separate sources of requirements. If a walkthrough differs from its linked governing rules, the rules take precedence.

## Normative language

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHOULD**, **SHOULD NOT**, and **MAY** indicate requirement strength when written in uppercase:

- **MUST**, **MUST NOT**, and **REQUIRED** define behavior necessary for protocol compatibility or safety.
- **SHOULD** and **SHOULD NOT** describe the expected behavior unless a documented reason justifies a different implementation choice.
- **MAY** identifies optional behavior that must not change consensus results or another participant's obligations.

Descriptive present-tense statements in the governing rule pages define V1 behavior even when those keywords are not repeated in every sentence.

## Sources of authority

Accepted on-chain state is authoritative for identity, assignment, deadlines, commitments, balances, settlement, and finality. Chain events are notifications that trigger a query; an event alone is not a substitute for current state.

Builder, Nexus, Cortex, adapter, indexer, and user-interface observations are off-chain information. They can transport data or initiate a protocol action, but cannot independently create an assignment, verdict, payment, or penalty.

## Determinism

All validators must derive the same result from the same accepted state and transaction. Consensus behavior must not depend on local time, floating-point arithmetic, map iteration order, network arrival order, private scoring, external API results, or implementation-specific defaults.

Canonical encodings, hashes, integer arithmetic, domain separators, and frozen version selectors are part of the protocol input where specified.

## Versioning and snapshots

An accepted Task keeps the Profile, order, candidate, parameter, encoding, and rule versions frozen for it. Later configuration or governance changes affect only the explicitly defined future boundary and do not reinterpret historical signatures or state.

An implementation that does not support a required version must reject the action or stop processing that path. It must not silently interpret the material under a newer or older version.

## Fail closed

Unknown versions, invalid signatures, inconsistent commitments, missing required randomness, arithmetic overflow, and violated invariants fail closed. A failure path may produce a defined timeout, refund, or unavailable-data outcome; it must not invent missing protocol facts.
