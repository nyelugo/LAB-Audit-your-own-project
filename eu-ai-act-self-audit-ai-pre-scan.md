# EU AI Act self-audit — AI Pre-Scan

**System audited:** AI Pre-Scan (Week 5 Project) · **Auditor:** Ugo Ahukannah
**Basis:** Regulation (EU) 2024/1689 as amended by Regulation (EU) 2026/1744 (in force 27 July 2026)

> First-pass compliance assessment, not a legal opinion, a conformity assessment, or a
> certification. Items marked **escalate** need a lawyer or DPO to settle.

---

## Phase 1: System brief

**What it does.** AI Pre-Scan takes the name of a company and produces a first draft of that
company's AI-system inventory — a list of the AI tools the company appears to be using, each one
tied to a quoted piece of published evidence. Alongside the list it produces a second output: the
questions that published evidence cannot answer, written so a client can answer them in a meeting.
It is a research tool for an external compliance adviser who has no access to the company's
internals.

**What it takes in.** One company name, typed by the adviser. From that it searches public sources —
web search, news, a company registry — and fetches the pages it finds. Those pages are chunked and
stored per scan so claims can be checked against retrieved text rather than model memory. The stated
design position is that the subject of research is the organisation and not any individual, and that
no personal data is collected.

**What it puts out.** A report with two parts: an inventory table (system, quoted evidence, vendor,
built or bought, where used, date first evidenced, confidence) and a discussion list of open
questions. Anything the evidence does not support comes back as `undetermined` rather than a guess.
It deliberately produces **no risk classification, no obligations, no articles and no legal
conclusion of any kind** — a separate deterministic checker does the legal step afterwards.

**Who is affected.** Primarily the **companies researched**, which are legal persons rather than
natural persons. A company could be approached, prioritised or questioned by an adviser on the
strength of a report about it. Secondarily, **individuals whose names appear in the fetched
sources** — an executive quoted in a press release, an author of a changelog, a recruiter named on
a careers page — because those pages are fetched and stored whole even though the policy is not to
record individuals.

**Human review.** Yes, and it is structural rather than optional. The adviser reads the report,
settles the open questions with the client, and only then feeds each verified system into the
separate checker. The system stops before the legal step by design, so no decision about any
company is produced by the tool alone.

**Who built it.** Ugo Ahukannah, solo, as a bootcamp project. It has not been placed on any market.

**Who would use it in production.** An external compliance adviser with a client list, entering a
client's name — never her own company's — and using the output to prepare for a client meeting.

---

## Phase 2: Risk tier classification

### CFU 1 — Recognize

| Question | Answer |
|---|---|
| Does this system fall under any prohibited category (Article 5)? | **No.** It performs no social scoring, no biometric processing, no emotion inference, no predictive policing and no untargeted facial scraping. It evaluates organisations against published evidence, and Article 5 is concerned throughout with practices directed at natural persons. |
| Does this system operate in any of the eight Annex III areas? | **No.** Its subject is a company's tooling, not a person's access to anything. The nearest candidates fail on their own terms: it makes no decision about employment (no applicant or worker is assessed), no decision about access to essential services, and it is not used by law enforcement or in migration or justice. |
| If Annex III: does it "significantly influence" decisions in that area, or is it narrow/preparatory? | **Not applicable** — Annex III is not engaged. Worth noting for completeness that even if it were, the output is expressly preparatory: it establishes facts for a human, and the legal determination is made elsewhere by a deterministic tool. |
| Does this system interact with end users or generate content requiring disclosure (Article 50)? | **Partly, and the duty is already substantially discharged.** It interacts with one professional user through a web interface. Article 50(1) requires that a natural person be informed they are interacting with an AI system unless it is obvious from context — here it is about as obvious as it gets: the product is named "AI Pre-Scan", and it announces demo mode on the page. It generates no synthetic audio, image or video, so Article 50(4)'s deepfake limb does not apply, and its reports are private client work rather than text published to inform the public, so that limb does not apply either. |
| **First-pass risk tier** | **Minimal risk** |
| One-sentence justification | The system assesses **organisations rather than natural persons**, which is what keeps it outside every Annex III area and outside Article 5, and its only user-facing disclosure duty under Article 50(1) is already met by context — so no specific AI Act obligations attach beyond the ones that apply to every AI system regardless of tier. |

**"Nothing applies" is a conclusion, so here is the evidence for it.** Every Annex III area is
defined by its effect on natural persons — biometric identification of people, access to education,
employment decisions about workers and applicants, access to essential services and benefits, law
enforcement against individuals, migration and asylum decisions, and the administration of justice.
AI Pre-Scan's output is a factual statement about a company's software estate. No natural person is
scored, ranked, admitted, refused or prioritised by it.

**The ambiguity I would flag for legal review.** Three changes would move this system out of minimal
risk, and two of them are plausible product directions:

| Change | Where it lands | Why |
|---|---|---|
| The inventory starts naming **which employees** use which AI tool | Likely Annex III(4), employment and workers management | It would then evaluate natural persons in a work context |
| The tool starts issuing the **risk classification itself** rather than handing facts to the checker | Still minimal on tier, but materially different exposure | Not an Annex III area, but it would be marketed as producing legal conclusions, which brings misleading-claims and professional-liability exposure the current boundary avoids |
| Output is used to **screen suppliers or score companies** for access to a service | Needs review | Assessment of organisations sits outside Annex III, but a scoring product used to deny access invites an Article 5(1)(c) conversation the moment natural persons are affected downstream |

I have not cross-checked this against the Commission's compliance checker; the lab suggests doing so
after forming an independent view, and the classification above is that independent view.

---

## Phase 3: Role map

### CFU 2 — Map roles

| Role | Entity | Key AI Act obligations |
|---|---|---|
| **Provider** | Ugo Ahukannah — **prospective**, not actual. The system has not been placed on the market or put into service, so no provider obligations have crystallised. If it were released under my own name, I would be the provider of a minimal-risk AI system | For a minimal-risk system: **Article 4 AI literacy** (support the AI literacy of staff and users — softened by Regulation (EU) 2026/1744 from *ensure* to *support*, but not removed); **Article 50(1)** disclosure where a user might not realise they are dealing with an AI; no conformity assessment, CE marking, registration or post-market monitoring, because those attach to high-risk systems only |
| **Deployer** | The external compliance adviser and her firm, in production use | Article 4 AI literacy in respect of her own staff; use of the system within its stated limits; **GDPR controller duties** for anything personal she processes through it. No Article 26 high-risk deployer duties and **no FRIA** — Article 27 reaches public bodies, private entities providing public services, and credit and life/health insurance deployers, none of which this is |
| **Vendor — OpenAI** | Supplies the language model behind the research loop | **GPAI provider** under Articles 51–56: technical documentation, information to downstream providers, EU copyright compliance, and a public summary of training data; systemic-risk duties on top if the model exceeds 10²⁵ FLOPs. These are OpenAI's obligations, not mine — but "powered by" transfers nothing upward, so the product-level responsibility for AI Pre-Scan stays with me |
| **Vendor — Pinecone** | Vector store holding chunked pages from each scan | No AI Act role of its own. It is a **GDPR processor** for whatever personal data ends up in those chunks, which is the subject of Gap 1 below |
| **Vendors — web search, news and company registry APIs** | Evidence sources | No AI Act role. Their terms of service and any database rights govern what may be fetched, stored and quoted |
| **Vendors — n8n and Notion** | Optional report delivery | No AI Act role; processors for whatever the report contains |

---

## Phase 4: Obligation checklist (high-risk only)

**Skipped, and here is why.** The eleven provider obligations in Articles 9–49 attach to high-risk
systems. AI Pre-Scan is minimal risk on the analysis in Phase 2, so the checklist does not apply and
completing it would misrepresent the system's status.

**What does apply is set out instead**, because "minimal risk" means minimal *under this Act* and
not unregulated:

| Obligation that does apply | Source | Status | Note |
|---|---|---|---|
| AI literacy — support users' and staff's ability to use the system competently | **Art 4** (as amended by Reg (EU) 2026/1744) | **Gap** | Applies to providers *and* deployers of **all** AI systems, at every tier. There is no user-facing statement of what the tool can and cannot conclude, and no onboarding material for an adviser |
| Disclosure that the user is dealing with an AI system | **Art 50(1)** | **Partial** | Discharged in practice by the product name and demo-mode banner, but nowhere stated explicitly, and nothing in the generated report itself says the content is AI-produced |
| Lawful, minimised processing of personal data | **GDPR** | **Gap** | See Gap 1 — the stated policy is not enforced by any control |
| Transfers of personal data outside the EEA | **GDPR Ch. V** | **Gap** | OpenAI and Pinecone are US-based; no mechanism documented |
| Respect for source terms, copyright and database rights | Copyright / sui generis database right | **Partial** | The system quotes evidence deliberately and attributes it, which helps, but no review of source terms has been done |
| Accurate description of what the product does | Consumer protection / misleading claims | **Met, and deliberately so** | The "no legal determination" boundary is enforced as a design rule and stated in the README |

---

## Phase 5: Gap analysis and remediation plan

### CFU 3, 4 and 5 — obligations, gaps, remediation

**Gap 1 — Personal data reaches the evidence store despite a policy that says it does not**

- **Obligation:** GDPR Articles 5(1)(c) data minimisation and 6 lawful basis; Chapter V for transfers. Not an AI Act obligation, but the most serious finding in this audit.
- **Current state:** `docs/proposal.md` states that the subject of research is the organisation, that no personal data is collected, and that named individuals encountered in sources are not recorded. The implementation does not do this. Pages found during a scan are fetched, chunked, embedded and upserted per company, whole. Careers pages carry recruiter names, press releases carry executive names and quotes, changelogs carry author names. **There is no redaction, filtering or PII handling anywhere in `src/`** — I checked before writing this, and the absence is the finding.
- **Required state:** either the policy is true in the implementation, or the processing has a documented lawful basis, a retention period, a transfer mechanism for the US vendors, and a record of processing.
- **Remediation:** the cheap and honest fix is to make the code match the claim — strip or hash person-name entities at chunk time, or narrow what is stored to the passages the evidence gate actually needs rather than whole pages. Add a retention TTL to the per-scan namespace, since the store is written but never read after the scan. Then either restate the policy accurately or keep it and enforce it.
- **Escalation needed?** **Yes** — DPO or privacy counsel, both on the lawful-basis question and on the US transfers.

**Gap 2 — No AI literacy material for the user (Article 4)**

- **Obligation:** Article 4, which survives the Digital Omnibus in softened form: providers and deployers must *support* the AI literacy of those using their systems.
- **Current state:** the README explains the system to a technical reader. There is nothing that tells an adviser, in the product, what the tool can conclude, what `undetermined` means, or that recall was measured at 0.444 — meaning the inventory is systematically incomplete and absence of a finding is not evidence of absence.
- **Required state:** users supported in understanding capabilities and limits well enough to use the output competently.
- **Remediation:** a short limitations panel in the web UI and a header block in every generated report, stating in plain words what the tool does not do and what the measured recall implies about missing systems.
- **Escalation needed?** No.

**Gap 3 — Article 50(1) disclosure is implicit rather than stated**

- **Obligation:** Article 50(1) — inform a natural person they are interacting with an AI system unless it is obvious from context.
- **Current state:** obvious from context in the app, given the name and the demo banner. But the generated report is a document that travels: it can be forwarded to a client with no indication that its contents were produced by an AI system.
- **Required state:** the disclosure should survive the artefact leaving the tool.
- **Remediation:** one line in the report footer stating that the inventory was generated by an AI system from public sources and requires verification. This is a five-minute change that also reduces the risk of the report being read as a professional opinion.
- **Escalation needed?** No.

**Gap 4 — Measured over-claiming, in a product whose output feeds compliance decisions**

- **Obligation:** none under the AI Act at minimal risk. This is professional-liability and misleading-claims exposure, and it belongs in the audit because tier does not equal risk.
- **Current state:** the evaluation is honest and public — over-claim rate 0.333 against a 0.10 target, described as the outstanding defect; recall 0.444 against 0.75; role correctness 0.739 against 0.90. Three metrics pass, including an honest-refusal rate of 1.0 and zero provenance violations.
- **Required state:** the user must not be able to mistake the output's reliability, given that an adviser may act on it in front of a client.
- **Remediation:** publish the measured metrics *with the report*, not only in the repository — the same numbers that make the evaluation credible make the output safe to rely on correctly. Keep the "no legal determination" boundary enforced in code and copy.
- **Escalation needed?** Partial — no lawyer needed to publish the numbers, but professional-indemnity implications are worth a conversation before any commercial use.

**Gap 5 — The provider/deployer line moves the moment this is shipped**

- **Obligation:** Article 3(3) provider definition; Article 25 on when a deployer becomes a provider.
- **Current state:** nothing has been placed on the market, so no obligations have crystallised. This is a real finding rather than a technicality: the audit is of a system that does not yet have a regulatory status.
- **Required state:** clarity, before release, about who is the provider and under whose name it is offered.
- **Remediation:** decide the release model before the first external user — released under my name makes me the provider; delivered as a bespoke build the adviser's firm operates under its own name makes them the provider. Document the choice, in the contract if there is one. Note the trap the project's own documentation already identifies for *its subjects*: rebranding or substantially modifying a bought system turns a deployer into a provider under Article 25, and it applies to AI Pre-Scan's own users too.
- **Escalation needed?** Yes, if it is ever commercialised — a lawyer should confirm the role split.
