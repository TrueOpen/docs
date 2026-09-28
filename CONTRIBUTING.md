# Contributing to TrueOpen documentation

This repository is the single source for TrueOpen documentation published through GitBook.

## Content rules

- Keep the main navigation in this order: Overview, Providers, Developers, Network Operators, Protocol, Reference. Each section links directly to its README; do not add a redundant Overview child.
- Place model integration under Providers and Task lifecycle walkthroughs under the applicable protocol version.
- Use lowercase English `kebab-case` paths so public URLs remain stable.
- Keep protocol definitions in one authoritative page and link to them elsewhere.
- State the applicable protocol version and network when behavior differs.
- Add a page to `content/SUMMARY.md` only when it contains useful reviewed content.
- Do not treat omission from `SUMMARY.md` as an access-control mechanism. Everything committed here is public.

## Do not publish

- Open-question registers or implementation blockers
- Internal ADR review material and rejected alternatives
- Unannounced roadmap items
- Internal service topology, credentials, private endpoints, or security-sensitive operations
- Acceptance plans, incident exercises, audits, and archived design drafts
- Unreviewed parameters or behavior that is not yet part of a released protocol

## Source of truth

All published explanations, guides, references, and protocol pages must be maintained in this repository. Pages must not include links or build-time dependencies that require documentation from another repository.

Within this repository, versioned protocol rules are authoritative for protocol behavior. Design explanations and stage walkthroughs provide context and must link to the governing rules instead of defining competing requirements.
