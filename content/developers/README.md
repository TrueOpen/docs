---
title: Developers
description: Build applications that submit and track AI Tasks on TrueOpen.
---

# Developers

This section is for application developers who consume compute through TrueOpen. It follows the application journey rather than the implementation of Cortex or the chain.

An application integration will normally:

1. Create or load a user account.
2. Discover a suitable model Profile.
3. Create a session and fund a Task order.
4. Submit input data and a signed order.
5. Track Worker selection, inference, and verification.
6. Retrieve and validate the result.
7. Open a challenge when the accepted result does not satisfy the Profile rules.

## Public interfaces

The application guides will document:

- SDK installation and supported environments
- Account creation and signing
- Profile discovery
- Session and Task submission
- Result retrieval and status tracking
- Challenge submission
- Public chain and Nexus APIs
- Error handling, retries, and idempotency

Concrete API quickstarts will be published with the corresponding SDK packages, endpoints, network configuration, and compatibility guarantees. Start with [Application integration](application-integration.md) for the application responsibilities and [Task lifecycle](../protocol/v1/tasks/README.md) for the interaction sequence.

If you want to supply inference or verification capacity, start with [Providers](../providers/README.md). If you are implementing the service behind Cortex, use [Model integration](../providers/model-integration/README.md).
