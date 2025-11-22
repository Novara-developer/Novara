# Novara

[![Test](https://github.com/Novara-developer/Novara/workflows/Test/badge.svg)](https://github.com/Novara-developer/Novara/actions)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Evidence-first AI governance stack — starting with a minimal, verifiable audit kit.

Novara is an attempt to answer one simple question:

> When an AI system makes a harmful decision,  
> who did what, under which policy, and  
> how can the world verify it **without trusting the vendor**?

This repository contains the first code and specs for that stack.

---

## Relationship to `novara-core`

This repo is the **implementation side** of Novara:

- A small, deterministic **evidence bundle format**
- A Python reference library (`novara-evidence-bundle`)
- CLI tools to generate and verify bundles
- Specs, tests, and CI so that others can re-implement it

The **constitutional documents** (governance, incident protocol, human-readable proof)
live separately in **[`novara-core`](https://github.com/novara-labs/novara-core)**  
(text-only, CC0, spec-first).

This repo is **“how it runs”**.  
`novara-core` is **“what it must obey”**.

---

## Repository scope

This repository currently focuses on **Novara Evidence Bundle v0.1.0**:

- deterministic, tamper-evident daily bundles for AI behaviour
- append-only hash-chained logs (AAL)
- cryptographic anchors for offline verification
- minimal, readable Python implementation with tests and CI

It is **not** a product, a service, or a full “AI platform”.  
It is a **toolkit** for building verifiable AI systems and audits.

Target time horizon: **2040–2060 AI / ASI governance**,  
not just “next quarter” or “this year’s model release”.

---

## Novara Evidence Bundle (v0.1.0)

The core idea is a **1-day, tamper-evident ZIP bundle**:

```text
<subject>-<YYYY-MM-DD>.zip
 ├─ meta.json        # human-readable metadata
 ├─ aal.ndjson       # append-only log with SHA3-256 hash-chain
 └─ anchors.json     # digests / anchors for critical files

Properties:
	•	Deterministic: same inputs → same bundle, byte-for-byte.
	•	Tamper-evident: aal.ndjson is a hash-chain; anchors.json pins its digest.
Any modification breaks the chain or the digest.
	•	Independently verifiable: verification uses only the bundle itself and public algorithms.
No secret keys, no vendor cloud, no hidden services required.

The Python library in this repo provides:
	•	data model for AAL records
	•	hash-chain construction and verification
	•	bundle generation (ZIP)
	•	bundle verification (including anchors)
	•	CLI tools on top

⸻

Quick start

1. Clone and set up

git clone https://github.com/Novara-developer/Novara.git
cd Novara   # adjust if this package lives in a subdirectory

python3 -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -e ".[dev]"

Note: this assumes a standard src/novara_evidence/ layout.

2. Generate a demo bundle

python scripts/generate_demo_bundle.py

Example output:

Wrote: examples/hinata-2025-11-19/hinata-2025-11-19.zip

3. Verify the bundle (human-readable)

python scripts/verify_bundle.py examples/hinata-2025-11-19/hinata-2025-11-19.zip

Example output:

[OK]
- AAL verification: OK
- Anchors verification: OK
- Last entry hash: 46c3e0ec9d7dfb40e6510eab89ae516b2f454fd77380763a2ed9acbc41871afd
- Bundle chain hash: 3d487a71050ad38c25740c7a93ee6212c57be0dd8dab0eec5f878ebca3fbb761

4. Verify the bundle (JSON output)

python scripts/verify_bundle.py --json examples/hinata-2025-11-19/hinata-2025-11-19.zip

Example JSON:

{
  "ok": true,
  "messages": [
    "AAL verification: OK",
    "Anchors verification: OK"
  ],
  "last_hash": "46c3e0ec9d7dfb40e6510eab89ae516b2f454fd77380763a2ed9acbc41871afd",
  "chain_hash": "3d487a71050ad38c25740c7a93ee6212c57be0dd8dab0eec5f878ebca3fbb761"
}

This JSON can be consumed by other tools, dashboards, or audit pipelines.

⸻

Project layout

High-level directory structure (v0.1.0):

Novara/
├── README.md
├── pyproject.toml
├── src/
│   └── novara_evidence/
│       ├── __init__.py
│       ├── aal/
│       │   ├── __init__.py
│       │   ├── model.py        # AALRecord data model
│       │   └── hash_chain.py   # hash-chain logic
│       ├── bundle/
│       │   ├── __init__.py
│       │   └── build.py        # demo bundle generation
│       ├── verify/
│       │   ├── __init__.py
│       │   └── verify.py       # bundle verification
│       └── cli/
│           ├── __init__.py
│           ├── generate_demo.py
│           └── verify.py
├── scripts/
│   ├── generate_demo_bundle.py  # thin wrapper around CLI
│   └── verify_bundle.py         # thin wrapper around CLI
├── spec/
│   ├── aal-v0.1.md              # human-readable AAL spec
│   ├── bundle-v0.1.md           # bundle format spec
│   └── schema/
│       └── aal-record-v0.1.schema.json
├── tests/
│   ├── test_hash_chain.py
│   └── test_verify_bundle.py
├── examples/
│   └── hinata-2025-11-19/
│       └── hinata-2025-11-19.zip   # genesis demo bundle
└── .github/
    └── workflows/
        └── test.yml               # CI: tests + demo verification


⸻

Features (v0.1.0)
	•	✅ Deterministic bundle generation
	•	✅ SHA3-256 hash-chained AAL log
	•	✅ Anchors with digests for critical files
	•	✅ Independent verification (no vendor dependency)
	•	✅ JSON and human-readable output
	•	✅ JSON Schema for AAL records
	•	✅ PyPI-ready project structure (pyproject.toml)
	•	✅ GitHub Actions CI (tests + demo verification)

Not yet included (by design, for v0.1):
	•	no cryptographic signatures
	•	no external blockchain / CTK-2 anchors
	•	no network calls or cloud dependencies
	•	no production deployment guidance

This is a minimal audit kit, not the full Novara stack.

⸻

Development

Run tests

pytest -v

Run tests with coverage

pytest -v --cov=src/novara_evidence --cov-report=term-missing

Editable install

pip install -e ".[dev]"

After that, the CLI entry points are available:

novara-generate-demo
novara-verify-bundle examples/hinata-2025-11-19/hinata-2025-11-19.zip

These are defined in pyproject.toml under [project.scripts].

⸻

Status & roadmap

Current status: v0.1.0 — initial audit kit release.
This is a working proof-of-concept, not yet recommended for production use.

Completed milestones
	•	✅ Genesis bundle generated (2025-11-19 05:14 UTC+8)
	•	✅ Python reference implementation
	•	✅ Human-readable specs (AAL / bundle)
	•	✅ JSON Schema for AAL records
	•	✅ CI with demo verification

Next steps
	•	Multi-language implementations
	•	Rust
	•	Go
	•	TypeScript / JavaScript
	•	CTK-2 style external anchoring (multi-chain)
	•	Integration examples for:
	•	small AI agents
	•	simple web apps
	•	First real-world incident bundles (“Novara cases”)
	•	Tooling for insurers / regulators / courts

The long-term goal is for the format and core specs to be governed
by a neutral Novara Foundation, as described in novara-core.

⸻

Contributing

Contributions are welcome.
	•	Check existing issues and discussions
	•	Keep the code small, explicit, and test-covered
	•	For new features, please add tests and update the relevant spec(s)
	•	For breaking changes to the format, open a design proposal first

⸻

License

Code in this repository is licensed under the MIT License
(see the LICENSE file).

The separate novara-core
textual specifications are published under CC0 1.0 (public domain dedication).

⸻

Citation

If you use this work in research or policy discussions, please cite e.g.:

@software{novara_evidence_bundle_2025,
  author  = {Hinata (Yanshan)},
  title   = {Novara Evidence Bundle: A Minimal Audit Kit for the AI Era},
  year    = {2025},
  url     = {https://github.com/Novara-developer/Novara},
  version = {v0.1.0}
}


⸻

Novara is an experiment in evidence-first AI governance:
logs before UX, proof before branding, verification before trust.