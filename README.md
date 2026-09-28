# TrueOpen Documentation

This repository contains the TrueOpen documentation published through GitBook.

All documentation content lives in [`content/`](content/README.md). GitBook reads directly from that directory; no page depends on content from another repository.

## Articles

Launch notes and longer posts about TrueOpen are in [`articles/`](articles/README.md).

## Repository structure

```text
content/
├── overview/       Product introduction and system architecture
├── providers/      Cortex operations and model integration
├── developers/     Application integration
├── operators/      Validator and Builder operations
├── protocol/       Design, mechanisms, Task lifecycle, and versioned rules
├── reference/      Terminology and lookup material
└── resources/      Supporting pages linked from Reference

articles/           Launch notes and longer posts (not part of GitBook)
gitbook-docs.yaml  GitBook configuration used by the repository integration
.gitbook.yaml       Default GitBook configuration for local compatibility
```

See [CONTRIBUTING.md](CONTRIBUTING.md) before adding or changing public documentation.
