# Stretch — human oversight procedure for AI Pre-Scan

Drafting the artefact for the most significant gap I can close without a lawyer. Gap 1 (personal
data in the evidence store) is more serious, but its remediation is a code change plus a DPO
conversation, not a document. The gap a document actually closes is **Gap 2 and Gap 4 together**:
the adviser relies on output whose measured limits are recorded in a repository she will never read.

**Purpose.** To ensure that no AI Pre-Scan output reaches a client, or informs advice given to one,
without a competent human having checked the things the system cannot check about itself.

**Who reviews.** The compliance adviser who ran the scan. Not a delegate, and not the client — the
review requires knowing what the tool does not do, which is the point of the procedure.

**What they check, before the report is used or forwarded:**

| # | Check | Why it exists |
|---|---|---|
| 1 | Every inventory row has a quoted piece of evidence and a working source link | The provenance contract is the system's core guarantee; a row without it is a defect, not a finding |
| 2 | Each quoted passage actually supports the claim made from it | Measured over-claim rate is 0.333 against a 0.10 target — one row in three is the expected failure mode, not an anomaly |
| 3 | The `first evidenced` date is consistent with the cited source | It drives the Article 111(2) transition question the downstream checker never asks |
| 4 | `built or bought` is right for each row | Measured role correctness is 0.739; this is the field that decides provider versus deployer downstream, so an error here propagates into the legal step |
| 5 | The absence of a finding is **not** reported to the client as an absence of AI | Measured recall is 0.444. Silence is missing data, never a clean bill of health |
| 6 | Any source the report lists as unavailable is chased or recorded as unchecked | A scan that lost a source and reported a clean result is the worst possible output |
| 7 | Nothing in the report has been paraphrased into a legal conclusion | The system produces facts; the checker applies law. The boundary survives only if the human keeps it |

**How overrides are recorded.** The adviser edits the report directly and marks each change with one
of three tags — `corrected` (the row was wrong), `demoted` (evidence too thin, moved to the
discussion list), or `added` (a system the scan missed, with the adviser's own source). Every tagged
change carries her initials and the date. The tagged copy is what goes to the client; the untouched
machine output is retained alongside it.

**Why the tags matter beyond the client meeting.** They are the only feedback signal this system has.
`added` counts measure real-world recall, `demoted` counts measure over-claiming, and `corrected`
counts on the built-or-bought field measure role accuracy — the same three metrics the evaluation
tracks, gathered from live use rather than a 12-company ground truth. Six months of tagged reports
would be a better evaluation set than the one the system was built against.

**Escalation.** If checks 2 or 5 fail on more than a third of rows in a single scan, the report is
not sent: the scan is rerun or abandoned and the failure is recorded. A tool that is wrong often
enough to need rewriting is not saving the adviser time, and the procedure should surface that
rather than absorb it.
