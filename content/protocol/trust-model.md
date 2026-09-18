---
title: Trust model
description: Authority, verification boundaries, and security assumptions in TrueOpen.
---

# Trust model

TrueOpen distributes execution, data delivery, verification, and consensus across different roles. This page explains their boundaries. The [V1 protocol](v1/README.md) defines the corresponding acceptance and failure rules.

## Chain and consensus

Accepted chain state is the authority for assignments, deadlines, balances, and finality. This relies on the chain's consensus security assumptions and correct deterministic execution by validators. An event or indexer response is an observation that should be reconciled with accepted state.

## Builders and data availability

Builders coordinate proposals and transport Task material through Nexus. Commitments let recipients check that delivered bytes match the accepted Task context. Commitments alone do not guarantee that data remains available: retention, availability duties, and defined failure paths are also required.

A Builder acknowledgement establishes transport progress, not a final verdict or payment. The [data and evidence rules](v1/tasks/data-and-evidence.md) define the relevant obligations.

## Workers, Verifiers, and Profiles

Workers provide inference results and evidence. Verifiers independently evaluate the material under the selected Profile. Selection, role separation, commit-reveal, and challenges limit specific manipulation opportunities; their protection depends on the verification algorithm and the participating set.

A registered Profile fixes the model, execution, verification, and evidence context. Registration does not itself prove universal model quality or factual correctness.

## Cortex and model runtimes

Cortex controls provider signing and validates the bindings returned by the model adapter. The runtime must not hold the service key or decide chain outcomes. Operators remain responsible for protecting their keys and host. See [Cortex architecture](../providers/model-integration/cortex-architecture.md).

## Governance and assets

Governance operates within versioned constraints and cannot rewrite historical Tasks through an ordinary parameter change. The canonical asset route adds bridge-signature and origin-chain assumptions beyond local chain consensus. A local withdrawal burn and delivery on the origin chain are separate outcomes.

See [Governance](v1/governance.md) and [Cross-chain assets](v1/cross-chain-assets.md) for these boundaries and their failure controls.
