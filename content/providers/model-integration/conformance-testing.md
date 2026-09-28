---
title: Conformance testing
description: Validate adapter bindings, deterministic material, failures, and security boundaries before production use.
---

# Conformance testing

An adapter should pass conformance tests for every advertised Profile and capability before a provider declares support.

## Contract tests

Test that the adapter:

- Reports exact Profile and runtime-capability bindings
- Rejects unknown or incompatible Profile versions
- Returns all required canonical output, metric, and evidence material
- Preserves Task, order, duty, and verification-round bindings
- Never substitutes another model, tokenizer, precision, or runtime silently
- Produces recomputable digests from returned material

## Repeatability tests

For identical completed Task bindings, verify that committed material is not affected by local paths, retry counters, process identifiers, logging configuration, or wall-clock timestamps. Where a Profile permits model-level variation, its commitment and evidence rules remain authoritative.

## Failure tests

Exercise unavailable artifacts, capacity exhaustion, malformed input, deadline cancellation, partial output, runtime crashes, adapter restarts, and storage failures. Each case should fail explicitly without returning signable partial material.

## Security tests

Confirm that the adapter cannot read provider private keys, submit chain transactions, contact Nexus as Cortex, or leak Task bodies into ordinary logs and metrics. Authenticate remote adapter connections and reject callers outside the provider-controlled boundary.

## Operator acceptance

Give the compute provider the supported Profile list, artifact and hardware requirements, runtime digest, expected resource use, known failure modes, and a repeatable readiness procedure. Passing local tests does not itself declare or activate support on-chain.
