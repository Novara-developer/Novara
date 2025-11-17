# Novara

Evidence-first AI governance experiment for Novara Phase 1.

> A minimal, verifiable way to prove  
> what an AI system did, under which policy,  
> and who should still have the **refusal right**.

---

## What is this repo?

This repo will host the **specs and examples** for the first version of the **Novara Evidence OS**:

- how to log AI behaviour in a tamper-evident way,
- how to bundle logs + anchors + policies into one ZIP,
- how to make **third-party verification** possible in minutes, offline.

Right now (2025-11-17) this is:

- `v0.0.x` – **spec-first, code-later**
- written by a 19-year-old student in Taiwan
- targeting **2040–2060 AI / ASI governance**, not just “next quarter”.

---

## Why does this exist?

By 2050, AI systems will be involved in:

- insurance, credit, and pricing,
- high-stakes decisions in medicine, policing, safety,
- e-sports / competitive gaming, sports analytics,
- culture and identity (anime / games / VTubers / digital personas).

Without a **verifiable evidence trail**, we get:

- responsibility ping-pong (“it was the model / vendor / user”),
- invisible policy shifts,
- and no way to check what really happened.

Novara’s answer is:

- **Evidence first. UI later.**
- **Logs and refusal rights stay on the human side.**
- Decisions can be **replayed, audited and priced**.

---

## Phase 1 scope (this repo)

This repo will focus on two initial use-cases:

1. **Insurance / finance (Proof-to-Pay & rate cards)**  
   - AI-assisted decisions must come with a verifiable bundle  
     that insurers and auditors can check.

2. **Culture & play (anime / games / sports)**  
   - anti-cheat / analytics / recommendation systems should also  
     be explainable and refutable with evidence bundles.

Planned structure (will be added step by step):

- `docs/` – Novara Manifesto and high-level design
- `specs/` – **Novara Evidence Bundle v0.9** draft
- `examples/` – minimal sample bundles (JSON + ZIP layout)

---

## Status

- **Very early draft. Breaking changes guaranteed.**
- No reference implementation yet – spec comes first.
- The long-term goal is to hand the format to a neutral  
  **Novara Foundation** so that no single vendor or country owns it.

---

## Contributing

For now, the most helpful feedback is about:

- missing fields for real-world audits (law / insurance / esports),
- ways to simplify the bundle while keeping it verifiable,
- alignment with upcoming regulations (EU AI Act, etc.).

Issues and discussions are welcome.
