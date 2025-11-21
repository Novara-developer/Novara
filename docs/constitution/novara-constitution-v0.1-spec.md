# Novara Constitution v0.1 — Spec

Frozen on 2025-11-22.

---

## Preamble

Novara is the final guardian of **evidence sovereignty** in the AGI/ASI era.  
It shall not be subordinated to any single state, corporation, individual, or ideology.  
This independence must be guaranteed **physically, cryptographically, and institutionally** for as long as Novara exists.

This document defines the core constitutional constraints for Novara.  
It is versioned as **v0.1** and is intended to remain immutable until at least v1.0 (earliest 2027),  
except in the case of a clearly documented catastrophic event.

---

## Article 1 — Independence by Design

1. **Funding Concentration Limit**

   - No single funding source may account for more than **10.0%** of Novara’s total annual revenue.
   - This applies to:
     - Direct donations
     - Certification / attestation fees
     - Insurance / risk-pool related distributions
   - Equity-like instruments that grant control over Novara’s governance are strictly prohibited.

2. **Allowed Funding Types**

   Novara may only receive funds from:

   - Voluntary donations
   - Publicly documented certification / attestation fees
   - Publicly documented insurance / risk-pool distributions

   Any other form of funding (e.g., undisclosed side contracts, opaque “consulting”) is incompatible with this constitution.

3. **Board Composition**

   The governing board of Novara must always consist of three classes of members:

   - **Technical / engineering representatives:** 33.3%
   - **Public sector / regulatory / policy representatives:** 33.3%
   - **Civil society representatives (NGOs, journalists, victim groups, academia, etc.):** 33.3%

   Small deviations due to rounding are permissible, but no single class may exceed 40% or fall below 30%.

4. **Term Limits**

   - Board members serve **2-year terms**.
   - Maximum **2 consecutive terms**.
   - After serving the maximum, there is a mandatory **4-year cooling-off period** before re-appointment.

5. **Conflict-of-Interest and Cooling-Off**

   - Active executives, board members, or employees of:
     - AI vendors under Novara attestation,
     - Governments directly regulating Novara,
     - Or entities holding more than 5% of funding volume in a given year  

     **may not** serve on Novara’s board.

   - A minimum **5-year cooling-off period** is required after leaving such positions before joining the Novara board.

---

## Article 2 — Self-Accountability Loop

Novara itself must always be the **most strictly audited subject** within its own system.

1. **Mandatory Logging**

   The following categories of actions **must** be recorded via Novara’s own AAL / CTK-2 mechanisms:

   - Board decisions and votes
   - Significant financial flows (in and out)
   - Major code changes affecting:
     - Attestation logic
     - Evidence formats
     - Governance rules
   - Changes to key operational policies

2. **Publication Deadline**

   - These records must be publicly accessible within **48 hours** of the underlying event.
   - Exceptions (e.g., for security-sensitive operations) must be explicitly justified and logged,  
     and may be delayed but not suppressed. Even in such cases, a redacted or delayed disclosure record is required.

3. **One-Click Transparency**

   For any recorded governance decision, any third party must be able to:

   - Verify, via a **One-Click** tool, who voted for or against,
   - Inspect the rationale text where applicable,
   - Trace where related funds came from and where they went.

4. **Self-Tampering Detection and Failsafe**

   - If Novara is detected to have tampered with its own governance or financial logs,  
     or if its own AAL / CTK-2 evidence contradicts itself, all Novara nodes must:

     - Immediately signal a **global red status**, and
     - Automatically halt all attestation and certification functions.

   - Recovery from this state requires:
     - A full public incident report,
     - External verification by an independent multi-institution panel,
     - And an explicit unfreeze vote according to Article 5 (Amendment).

---

## Article 3 — Multi-Anchor Neutrality

Novara’s CTK-2 based anchoring must not depend on a single geopolitical or corporate stack.

1. **Minimum Anchor Diversity**

   CTK-2 must anchor to at least **four distinct classes** of systems, including but not limited to:

   - A major **Proof-of-Work** blockchain (e.g., Bitcoin)
   - A major **Proof-of-Stake** blockchain (e.g., Ethereum-family)
   - At least one **non-Western / non–US-EU aligned L1**,  
     such as chains primarily governed or operated outside the dominant Western sphere
   - At least one **state-neutral, long-term storage oriented system**  
     (e.g., Arweave-like, WORM / archival systems)

2. **Degradation and Stop Condition**

   - If the number of active, healthy anchor classes falls below **3**,  
     Novara must automatically:
     - Stop issuing new attestations,
     - Mark the system as degraded,
     - And emit a public, machine-verifiable alert.

   - Attestation may only resume after anchor diversity is restored to **4 or more** classes.

---

## Article 4 — Independence Index

Novara’s independence must be **quantified and audited**.

1. **Annual Independence Audit**

   - Once per year, at or before **December 31**,  
     an independence audit must be conducted by an external consortium of universities and/or research institutions.

   - This audit must compute and publish an **Independence Index** score (0–100),  
     based on:
     - Funding diversity
     - Governance diversity
     - Infrastructure / anchor diversity
     - Legal / jurisdictional dispersion
     - Absence of dominant single-party control

2. **Automatic Consequences**

   - If the Independence Index is **below 90**,  
     the board is automatically dissolved, and a re-constitution process must be initiated according to this constitution.

   - If the Index is **95 or above**, Novara may be designated as **“Platinum Neutral”** for that year,  
     which can be used as a public trust mark.

---

## Article 5 — Amendment

This constitution is deliberately hard to change.

1. **Amendment Requirements**

   To amend any part of this document (including introducing v1.0 or later):

   - Each of the three board classes (technical, public sector, civil society) must approve the change by at least **3/4 majority** within that class.
   - A majority of active Novara nodes (as defined in protocol) must signal approval, recorded via Novara’s own evidence mechanisms.
   - A public review period of at least **24 hours** must be provided, during which:
     - The proposed change and its rationale are published,
     - Comments from the public and stakeholders are logged and preserved.

2. **Non-Retroactivity**

   - Amendments cannot retroactively reinterpret or invalidate past evidence bundles or incident decisions.
   - Past cases remain bound by the version of the constitution and protocols in force at the time.

---

## Immutability of v0.1

- This document is the **v0.1** specification of the Novara Constitution.  
- The `-spec.md` text is intended to remain unchanged until at least **v1.0**, targeted no earlier than **2027**,  
  except in the case of a clearly documented catastrophic event that makes continued operation impossible without revision.
- All operational learnings, clarifications, and case law must be recorded in separate `-notes.md` documents,  
  not by editing this file.

This file itself is part of the evidence of Novara’s long-term commitment to independence and self-accountability.