---
title: Profile and capability manifest
description: Bind an adapter implementation to exact model Profiles, capabilities, artifacts, and runtime semantics.
---

# Profile and capability manifest

A capability manifest tells Cortex exactly what the adapter can execute. It is a technical claim about a concrete runtime, not a provider's price or willingness to accept work.

## Required identity

Each advertised entry binds:

- Model identifier and Profile version
- Profile manifest digest
- Runtime-capability digest
- Inference, verification, or both capabilities
- Required model, tokenizer, precision, and evidence artifacts
- Runtime implementation and compatibility version

The pair `(model_id, profile_version)` must be unique in one adapter view. Never treat a model name without its Profile version as sufficient identity.

## Capability semantics

Inference support means the adapter can produce canonical output and every evidence object required by the Profile. Verification support means it can evaluate all committed generated positions and produce the required metric material. Advertising both means satisfying both contracts independently.

Provider capacity, queue state, and minimum price are local operating policy and do not belong in the compatibility manifest.

## Readiness

`ReadinessCheck` should verify artifacts, digests, runtime support, storage access, and a lightweight execution path for the exact Profile and capability. It must fail closed on missing or mismatched artifacts.

A readiness response must identify what was checked and return the exact bindings expected by Cortex. Generic backend health is not Profile readiness.

## Version changes

Any change that alters inference output semantics, verification metrics, evidence construction, or runtime compatibility requires the appropriate new Profile or capability digest. An in-place local change must not alter work already bound to an existing Task lease.

Compute providers use these manifest results when they [configure Profiles and capabilities](../profiles-and-capabilities.md).
