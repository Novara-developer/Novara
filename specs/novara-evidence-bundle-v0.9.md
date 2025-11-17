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



## 1. File layout
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



## 2.meta.json 
{
  "format": "novara-evidence-bundle",
  "version": "0.9",
  "bundle_id": "urn:uuid:...",
  "created_at": "2025-11-17T00:00:00Z",
  "producer": {
    "name": "Example AI Service",
    "jurisdiction": "TW",
    "contact": "compliance@example.com"
  },
  "subject_type": "human",           // or "org", "mixed"
  "scope": ["insurance_pricing"],    // free-form tags
  "hash_algorithm": "SHA3-256"
}



## 3.aal/chain.ndjson 
{
  "seq": 1,
  "prev_hash": null,
  "this_hash": "hex...",
  "ts": "2025-11-17T00:00:00Z",
  "role": "ingest",                  // "inference", "policy_eval", ...
  "actor": "client:web",
  "input_ref": "sha3-256:...",
  "output_ref": null,
  "policy_version": "demo-v1",
  "signature": {
    "eddsa": "base64...",
    "pqc_dilithium2": "base64..."
  }
}



## 4.independence.json 
{
  "version": "0.9",
  "operators": [
    {
      "name": "Novara Labs (demo)",
      "jurisdiction": "TW",
      "role": "service_operator"
    }
  ],
  "infrastructure": [
    {
      "provider": "cloud:example",
      "region": "ap-east-1",
      "trust_anchors": ["TPM2.0", "TEE:TDX"],
      "notes": "demo only"
    }
  ],
  "independence_index_hint": 0.82
}

