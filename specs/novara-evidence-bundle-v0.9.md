# Novara Evidence Bundle v0.9 (draft)

## 0. Purpose

A **Novara Evidence Bundle** is a ZIP file that contains everything a
third-party needs to verify an AI-related decision *offline*, in a few minutes.

Goals:

- deterministic, implementation-agnostic structure  
- tamper-evident link between events and anchors  
- friendly to later ZK / external verifiers

This is **not** tied to any specific model, cloud, or country.

---

## 1. File layout (high level)

A bundle is a ZIP with this layout:

```text
bundle.zip
├── meta.json
├── independence.json
├── aal/
│   └── chain.ndjson
├── anchors/
│   └── anchors.json
├── policy/
│   └── policy.json
├── refusal/
│   └── refusals.ndjson
└── cost/
    └── cost.json