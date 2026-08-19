# Compliance memo — AI Pre-Scan

**To:** Head of Product · **From:** Ugo Ahukannah · **Date:** 19 August 2026
**Re:** EU AI Act position of AI Pre-Scan, and what to do before we ship it

**1. Classification.** AI Pre-Scan is **minimal risk** under the EU AI Act. The reason is
structural rather than lucky: everything the Act's high-risk list covers is defined by its effect on
*people*, and our system assesses *companies*. No individual is scored, ranked, admitted or refused
by it. That classification holds only while that stays true — see step 4.

**2. Roles.** Today, nobody. The system has not been placed on the market, so no obligations have
crystallised. On release, whoever puts it out under their own name is the **provider**: us if we
ship it, the adviser's firm if we build it for them to operate. The compliance adviser using it is
the **deployer**. OpenAI is the provider of the general-purpose model underneath and carries its own
obligations — which do not transfer to us, and do not shield us either.

**3. Key findings.** Three, in order of how much they should worry you.

*We say we don't collect personal data, and the code doesn't back that up.* Our own proposal states
that we research organisations, not individuals, and that named individuals are not recorded. In
practice we fetch whole pages — careers pages, press releases, changelogs — and store them chunked
in a US vector database. Those pages have people's names in them. This is a GDPR problem rather than
an AI Act one, and it is the gap I would fix first, because the mismatch between a stated policy and
the implementation is worse than having no policy.

*We don't tell users what the tool can't do.* Article 4 requires us to support the AI literacy of the
people using our system, and it applies at every risk tier. Our measured recall is 0.444: the
inventory is systematically incomplete, and an adviser who reads a short list as "this client has
little AI" has been misled by silence.

*Reports travel without their caveats.* The app makes it obvious you're using an AI tool. A report
forwarded to a client does not.

**4. Recommended next steps.** First, make the code match the privacy claim — redact person names at
chunk time or store only the passages the evidence gate needs, and add a retention limit. Second, put
the limitations and the measured metrics into the product and into every report footer, including a
line stating the report is AI-generated and requires verification. Third, decide the release model
and who the provider is *before* the first external user. Steps one and three need external review:
a DPO for the personal-data and US-transfer questions, and a lawyer for the role split if we
commercialise.

**5. Caveats.** This is a first-pass internal assessment, not a legal opinion, not a conformity
assessment, and not a certification. It reflects the system as built on 19 August 2026 and the law as
amended by Regulation (EU) 2026/1744. Classification is a judgement, and the three scenarios in the
audit that would change it are all plausible product decisions rather than hypotheticals.
