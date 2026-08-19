# Reinforce — what the brief glossed over, and the decision I would remake

## 1. The component I minimised, and whether the picture changes

Writing the system brief, I described the evidence store in one clause — "pages are chunked and
stored per scan" — and moved on. That clause is doing more work than the rest of the brief.

Three components make inferences or hold data, and only one of them was prominent in my own mental
model of the system:

| Component | What it actually does | Was it prominent to me? |
|---|---|---|
| The LangGraph research loop with an OpenAI model | Decides what to search for, reads pages, proposes candidate systems | Yes — this is "the system" in my head |
| The evidence gate | Deterministic code; checks quoted support and source currentness before a finding is emitted | Yes, and I am proud of it, which is part of the problem |
| The Pinecone evidence store | Ingests whole fetched pages, chunked and embedded, per company, in the US | **No.** It is described in the architecture doc as "written, not yet read" — so I had filed it as inert |

**Does the compliance picture change if I include them properly? The tier does not; the exposure
does.** The risk tier stays minimal — none of these components assesses a natural person. But the
store converts a system I described as researching organisations into one that quietly accumulates
personal data about individuals who happen to appear in company sources, in a third country, with no
retention limit. "Written, not yet read" felt like a reason to discount it. For data protection it is
the opposite: data that is collected and never used is the least justifiable kind, because the
necessity argument is empty.

The blind spot has a shape worth naming. I discounted the component that does no interesting work.
Compliance attaches to what a system *holds and does to people*, not to what is architecturally
interesting.

## 2. The design decision I would remake

**The decision:** fetch and store whole pages, rather than extracting and storing only the passages
the evidence gate needs.

**Why it was reasonable at the time.** The gate checks claims against retrieved passages and
provenance metadata rather than model memory, and whole pages meant no risk of cutting away the
context a later check might need. It also kept the door open for the vendor-corpus retrieval that
the architecture anticipates. Storing everything is the safe default when you do not yet know what
you will need.

**Why it creates a compliance burden.** It converts every scan into a personal-data collection event.
The published policy says individuals are not recorded; whole-page storage makes that untrue for any
source with a name on it. It puts that data in a US vector store with no retention limit and no
transfer mechanism. And it does all this for data the system does not currently read back.

**What I would do instead.** Store the quoted passage the gate actually validated, plus its URL,
retrieval timestamp and hash — the provenance contract, not the page. That preserves every property
the gate depends on, shrinks the store by an order of magnitude, and makes the privacy claim true by
construction rather than by intention. Where a whole page is genuinely needed, cache it for the life
of the scan and drop it at the end.

**The transferable lesson.** A privacy claim in a proposal is a design constraint, not a statement of
intent — if nothing in the code enforces it, it is a claim that will be false the first time the
system meets a real source. I wrote the ethics section before the ingestion path, and never went back
to check the second against the first.
