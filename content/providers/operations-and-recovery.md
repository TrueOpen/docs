---
title: Operations and recovery
description: Monitor a Cortex Node, recover state, handle deadlines, and protect evidence.
---

# Operations and recovery

Reliable operation depends on distinguishing local progress from accepted protocol progress.

## Monitor the node

Monitor at least:

- Chain synchronization lag, query failures, and event cursor progress
- Nexus connectivity, acknowledgement failures, and Builder endpoint changes
- Signed material that remains unaccepted near a deadline
- Self-rescue state and transaction failures
- Per-Profile readiness, queue depth, capacity, and support freshness
- Evidence-store capacity, write failures, and cleanup backlog
- Local Task leases that remain open after expected finality

Do not expose prompts, outputs, private keys, transport credentials, checkpoints, or sensitive evidence in ordinary logs and metrics.

## Persist before sending

Persist signed handraises, receipts, commitments, and reveals with their Task binding before transmission. A crash after sending must be recoverable without signing different bytes for the same responsibility.

Write evidence to a staging location, validate it, and publish it atomically before its index reports availability.

## Restart safely

On startup, Cortex should not immediately offer new capacity. It first:

1. Loads Profiles and validates signer and storage access.
2. Restores Task leases, signed material, evidence indexes, and deduplication records.
3. Queries the chain from the last safe cursor.
4. Reconciles every non-terminal local Task with chain state.
5. Rebuilds missing responsibility state from queries rather than waiting for old events.
6. Resumes valid retry or self-rescue work.
7. Enables new handraises only after reconciliation completes.

Duplicate events may trigger a query but must not create a second signature, evidence object, or different submission.

## Resolve state conflicts

If local signed material conflicts with a chain query:

- Stop signing new material for the affected Task.
- Preserve local material and diagnostics.
- Treat the chain as authoritative.
- Rebuild Task state from chain facts.
- Require operator attention if stale or replayed transport input does not explain the conflict.

Never resolve a conflict by trusting the newest Nexus message or local timestamp.

## Back up and recover evidence

Backups should cover signed material, Task leases, evidence indexes, deduplication state, and evidence objects. After restoring a backup, reconcile chain responsibility again; cached assignment and finality fields are not authoritative.

If required evidence cannot be recovered, stop accepting new responsibility and surface the affected Tasks. Do not generate different evidence merely to replace a missing object.

## Planned maintenance

Before shutdown or upgrade:

1. Stop new handraises.
2. Identify open Worker, Verifier, and evidence-retention duties.
3. Persist pending signed material and the current chain cursor.
4. Complete duties or preserve a tested recovery path.
5. Restart and reconcile before offering new capacity.

A single Profile can be drained without stopping unrelated Profiles.
