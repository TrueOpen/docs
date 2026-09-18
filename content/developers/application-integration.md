---
title: Application integration
description: Application responsibilities when submitting, tracking, and consuming TrueOpen Tasks.
---

# Application integration

An application consumes TrueOpen through user-authorized orders, off-chain data transfer, and accepted chain state. This guide describes the integration boundaries; concrete SDK calls depend on the public SDK release.

## Prepare a Task

Select an exact Model and Profile version. Check its input schema, generation limits, verification behavior, and budget requirements. Create the required on-chain Session before submitting an offline signed order. Keep transaction signing and order signing in their separate authorization domains.

See [Accounts and signatures](../protocol/v1/foundations/accounts-and-signatures.md) and [Orders and Task identity](../protocol/v1/tasks/orders-and-identity.md).

## Submit and track

Submit the signed order and input through the Task Builder path. Persist the Task identity and order binding so retries can be reconciled with accepted chain state. A transport acknowledgement does not prove admission or assignment.

Track the accepted Task stage and deadlines. Output availability, a verification verdict, and final settlement are distinct states and should be represented separately in the application.

## Consume results

Validate returned data against the expected Task context and commitments. Present provisional output as provisional until the applicable verification and challenge process closes.

If opening a challenge, follow its eligibility, deadline, and funding rules. At finality, reconcile the final outcome and refund or payment state. See [Task lifecycle](../protocol/v1/tasks/README.md) for the full sequence and its failure paths.
