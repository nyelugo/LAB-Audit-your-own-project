# Audit your own project

**Track:** Module 7 — EU AI Act · **When:** Week 7, Day 2 · **Status:** Required

This repository contains everything you need for this lab.

## Files

- [`instructions.md`](./instructions.md) — the lab instructions
- [`rubric.md`](./rubric.md) — how your submission is graded; this is what the AI reviewer checks your PR against

## How to complete this lab

1. **Fork** this repository.
2. Do the work described in `instructions.md`, committing to your fork.
3. Open a **pull request** back into this repository.
4. You'll receive **AI feedback** on your PR based on `rubric.md`. Address any blocking feedback and push updates to the same PR.

## Submission hygiene

- Keep this repository scoped to this lab only — no unrelated projects or personal files.
- Use clear, descriptive filenames.
- Remove secrets, API keys, and tokens before committing.

---

## Submission contents (Ugo Ahukannah)

**System audited:** [AI Pre-Scan](https://github.com/nyelugo/PROJECT-AI-Pre-Scan) — my Week 5
Project. Give it a company name, get an evidence-backed first draft of that company's AI-system
inventory, plus the questions public evidence cannot settle.

| File | Contents |
|---|---|
| [`eu-ai-act-self-audit-ai-pre-scan.md`](./eu-ai-act-self-audit-ai-pre-scan.md) | The audit: Phase 1 system brief, Phase 2 risk-tier classification with the tier-change triggers, Phase 3 role map, Phase 4 (why the high-risk checklist is skipped and what applies instead), Phase 5 gap analysis and remediation |
| [`compliance-memo-head-of-product.md`](./compliance-memo-head-of-product.md) | Phase 6: the one-page memo to a Head of Product — classification, roles, three findings, next steps, caveats |
| [`reinforce-ai-pre-scan.md`](./reinforce-ai-pre-scan.md) | Reinforce: the component I glossed over in my own brief, and the design decision I would remake |
| [`stretch-human-oversight-procedure.md`](./stretch-human-oversight-procedure.md) | Stretch: a human oversight procedure — who reviews, what they check, how overrides are recorded |

**Headline finding:** the system is **minimal risk** under the AI Act, because it assesses companies
rather than people — but the audit's most serious gap is not an AI Act gap at all. The project's own
proposal states that no personal data is collected and that named individuals are not recorded;
there is no redaction anywhere in `src/`, and whole fetched pages are chunked and stored in a US
vector database. The memo puts that first.
