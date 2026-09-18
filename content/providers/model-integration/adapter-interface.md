---
title: Model adapter interface
description: Implement the stable capability boundary between Cortex and model compute.
---

# Model adapter interface

Cortex talks to model compute through an adapter with six stable capabilities. The adapter may be in-process, local, or remote, but Cortex remains the only component allowed to sign protocol material.

## Operations

| Capability | Purpose | Task-bound |
|---|---|---|
| `Health` | Report lightweight backend health | No |
| `ListCapabilities` | Enumerate supported Profiles and inference or verification capabilities | No |
| `ReadinessCheck` | Validate a Profile before support declaration | No |
| `Estimate` | Provide best-effort load and completion estimates for local policy | Yes |
| `Infer` | Produce canonical Worker output and required evidence | Yes |
| `Verify` | Produce full-output verification metrics and evidence | Yes |

## Bind every Task operation

Task-bound calls carry the exact context supplied by Cortex, including Task identity, order commitment, Profile version, assigned duty, verification round where applicable, and runtime-capability digest.

The adapter returns those bindings with recomputable result digests. Cortex rejects a result when any binding differs from its persisted Task lease. The adapter must never silently fall back to another Profile version or runtime.

## Implement `Infer`

`Infer` is invoked only after Cortex confirms Worker assignment and persists the Task lease. Return:

- Canonical output bytes or frames
- Material needed to calculate the output commitment
- Generated-work measurement material
- Evidence artifacts required by the Profile
- Diagnostic digests suitable for local troubleshooting

Do not return a final verdict, payout, penalty, or claimed chain state.

## Implement `Verify`

`Verify` is invoked after Cortex confirms formal Verifier assignment and validates the downloaded Task material. Return raw per-position measurement material, metric summary and root, evidence artifacts, and the candidate result. Cortex recomputes and validates them against the frozen Profile before commit or reveal.

Challenge verification uses the same boundary with an independent round identifier.

## Treat estimates as advisory

`Estimate` may be stale or unknown. It helps provider scheduling before a handraise, but must never become a signed protocol fact, candidate weight, or justification for missing an accepted duty.

## Errors and cancellation

Distinguish at least capacity exhaustion, capability mismatch, invalid Task material, backend failure, cancellation, and protocol-risk errors. Return complete material or fail; Cortex cannot sign partial output from a timed-out call.

Cancellation stops local computation. It does not cancel responsibility already accepted on-chain, so Cortex may retry, invoke fallback, or enter a deterministic failure path.

## Preserve the security boundary

The adapter and runtime must never receive operator or service private keys or connect directly to the chain or Nexus. Keep prompts, outputs, logits, and checkpoints in controlled Task and evidence stores rather than ordinary logs.
