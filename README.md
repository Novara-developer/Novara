

# Novara

[![Test](https://github.com/Novara-developer/Novara/workflows/Test/badge.svg)](https://github.com/Novara-developer/Novara/actions)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Evidence-first AI governance stack — starting with a minimal, verifiable audit kit.

**Novara is not a personal assistant.  
It is an evidence & payment rail for AI-driven decisions.**

Novara is an attempt to answer one simple question:

> When an AI system makes a harmful decision,  
> who did what, under which policy, and  
> how can the world verify it **without trusting the vendor**?

This repository contains the first code and specs for that stack.

Novara is **not** an alternative to LLM vendors.  
It is the layer that will later audit, price, and sometimes overrule them.

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
- append-only hash-chained logs (AAL: AI Action Ledger)  
- cryptographic anchors for offline verification  
- minimal, readable Python implementation with tests and CI

It is **not** a product, a service, or a full “AI platform”.  
It is a **toolkit** for building verifiable AI systems and audits.

Target time horizon: **2040–2060 AI / ASI governance**,  
not just “next quarter” or “this year’s model release”.

---

## Who is this for?

Novara is aimed at people who need **verifiable AI behaviour**, not just better UX:

- **Regulators / auditors** who want portable, tamper-evident logs for AI systems  
- **Insurers / risk engineers** who must price and pay AI-driven claims  
- **Engineers / SREs / ML teams** who want a minimal, deterministic audit kit  
- **Researchers / policy people** exploring evidence-first AI governance

If you just want a “smart personal assistant”, this is probably the wrong repo.  
If you want **receipts for AI decisions that move money**, you are in the right place.

---

## Novara Evidence Bundle (v0.1.0)

The core idea is a **1-day, tamper-evident ZIP bundle**:

```text
<subject>-<YYYY-MM-DD>.zip
 ├─ meta.json        # human-readable metadata
 ├─ aal.ndjson       # append-only log with SHA3-256 hash-chain
 └─ anchors.json     # digests / anchors for critical files
```
Properties:
- Deterministic: same inputs → same bundle, byte-for-byte.
- Tamper-evident: aal.ndjson is a hash-chain; anchors.json pins its digest.
- Independently verifiable: verification uses only the bundle itself and public algorithms.
- No secret keys, no vendor cloud, no hidden services required.

The Python library in this repo provides:
	•	data model for AAL records
	•	hash-chain construction and verification
	•	bundle generation (ZIP)
	•	bundle verification (including anchors)
	•	CLI tools on top

⸻

Example use case: insurance payout

One concrete scenario for Novara Evidence Bundles:
	1.	An AI model proposes a payout amount for an insurance claim.
	2.	The claims system writes AAL records and builds a daily evidence bundle.
	3.	A payment rail refuses to move money unless:
	•	a valid bundle exists,
	•	the hash-chain is intact, and
	•	the decision matches the active policy.
	4.	Auditors (or courts) can later:
	•	pull the ZIP file,
	•	verify it offline with a small CLI, and
	•	replay what the AI and the surrounding system actually did.

Today this is done with a mix of ad-hoc logs, screenshots, and vendor dashboards.
Novara tries to make “one day, one verifiable bundle” the default instead.

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

Implementation status (2025-11)

Novara v0.1 is intentionally small but already running:
	•	✅ Python reference library for AAL + bundle generation
	•	✅ Demo bundle (examples/hinata-2025-11-19/*.zip) built by CI
	•	✅ Verification CLI (novara-verify-bundle) with JSON output
	•	✅ JSON Schema for AALRecord and basic tests

Planned for public releases:
	•	v0.1.1 — more examples (insurance / credit / subsidy flows)
	•	v0.1.2 — CTK-2 style external anchoring (multi-chain, optional)
	•	v0.2.0 — first Novara Cases (real-world incident bundles)

⸻

Existing audit logs vs Novara Evidence Bundle

Novara does not replace all logs or SIEM.
It defines a portable, verifiable summary that other tools can consume and compare.

Aspect	Typical audit logs / SIEM	Novara Evidence Bundle v0.1
Format	DB tables, ad-hoc JSON, vendor-specific	Small fixed ZIP (meta.json + aal.ndjson + anchors.json)
Mutability	Often mutable by admins or migrations	Append-only hash-chain + anchored digest
Reproducibility	Rarely specified	Deterministic build (same inputs → same ZIP)
Verification dependency	Needs database + vendor infra	Stand-alone CLI, offline, no secrets
Anchoring	Usually none	Designed for CTK-2 / multi-anchor extensions
Interoperability	Per-vendor formats	Spec + schema intended for multi-language re-implementations


⸻

Standardisation and ecosystem

Novara Evidence Bundle v0.x is intentionally implementation-first:
	•	A minimal spec and schema that others can re-implement in any language
	•	A small Python reference library + CLI to show what “correct” looks like
	•	No dependency on any particular cloud, LLM vendor, or blockchain

Formal standardisation (ISO / IEC / IETF, etc.) is not the starting point.
If the format proves useful in real pilots (insurers, regulators, auditors),
we expect the community or a neutral foundation to take it further.

For now, the goal is:

small, boring, well-specified bundles
that other tools and organisations can reliably build and verify.

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

Run tests:

pytest -v

Run tests with coverage:

pytest -v --cov=src/novara_evidence --cov-report=term-missing

Editable install:

pip install -e ".[dev]"

After that, the CLI entry points are available:

novara-generate-demo
novara-verify-bundle examples/hinata-2025-11-19/hinata-2025-11-19.zip

These are defined in pyproject.toml under [project.scripts].

⸻

Status & roadmap

Current status: v0.1.0 — initial audit kit release.
This is a working proof-of-concept, not yet recommended for production use.

Roadmap (high-level)

Novara is designed as a long-horizon protocol. Rough phases:
	•	2025–2027 — Evidence Bundle era
	•	v0.x of AAL + bundle format
	•	Multi-language reference implementations (Python / Rust / Go / TypeScript)
	•	Pilot integrations with small insurers / regulators
	•	First public Novara Cases published as .zip
	•	2028–2033 — Proof Rail era
	•	Novara Proof Rail deployed as a pre-payment gate
(AI-driven payouts require valid evidence bundles)
	•	A share of AI-driven claims / credit / subsidies executed through Novara rails
	•	De-facto usage in RegTech / audit tools
	•	Drafts for formal standardisation (ISO / IEC / IETF) if there is demand
	•	2034–2040+ — Civic infrastructure era
	•	Time Court / counterfactual re-trial tooling for past AI decisions
	•	Gen-Z / civic right of “ask for evidence” from AI systems
	•	Evidence bundles used in courts, insurance pricing, and public policy

The long-term goal is for the format and core specs to be governed
by a neutral Novara Foundation, as described in novara-core.

⸻

Ethics & safeguards (scope boundaries)

Novara is built for systems that already move money
(claims, credit, subsidies, payouts), not for turning every aspect of human life into a log.

If a deployment starts to look like general surveillance of people,
it is probably outside the intended scope of this project.

Bundles are designed so that:
	•	they can be generated and verified locally, without calling a central service
	•	personally identifying information can be pseudonymised or excluded at the edge
	•	zero-knowledge style extensions (ZK proofs over bundles) remain possible in future versions

⸻

Contributing

Contributions are welcome:
	•	Check existing issues and discussions
	•	Keep the code small, explicit, and test-covered
	•	For new features, please add tests and update the relevant spec(s)
	•	For breaking changes to the format, open a design proposal first

⸻

License

Code in this repository is licensed under the MIT License
(see the LICENSE file).

The separate novara-core textual specifications are published under CC0 1.0
(public domain dedication).

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

Novara Core – Key Principles (v0.1)
	1.	Evidence First
Logs before UX, proof before branding, verification before trust.
	2.	Evidence Sovereignty
“Ground truth” is whatever can be shown by open, tamper-evident evidence bundles,
not by press releases or PR.
	3.	Zero-Trust Verification
Anyone should be able to verify what happened without trusting the vendor, cloud, or hidden keys.
	4.	Determinism
Same inputs → same outputs → same evidence bundle, byte-for-byte.
If two runs produce different evidence, that difference itself must be explainable and logged.
	5.	Tamper-Evidence
Any change to logs, policies, models, or configs must be either:
	•	impossible, or
	•	visible as a cryptographic “scar” (hash chain break, anchor mismatch, etc.).
	6.	Attribution-Ready
Every decision can be traced to:
	•	actors (AI / operator / user),
	•	policy version,
	•	model/version,
	•	time window.
	7.	SLO-Bound Remedy
Once harm crosses a public threshold (e.g. ¥10,000),
compensation is driven by pre-funded SLO-Bonds and an open attribution formula,
not by ad-hoc negotiation.
	8.	Human-Readable Proof
Victims and the public receive a plain-language narrative
(“what happened / who pays / what changed”), not just hashes and JSON.
	9.	Multi-Anchor Neutrality
Evidence anchors must be spread across multiple independent infrastructures and jurisdictions
(different chains, different operators, different political blocs).
	10.	Civic Time Horizon
Novara Core is designed as public infrastructure for 2040–2060,
not as a feature of any single company, startup, or product cycle.