# Interview question bank — gap-filling only

This bank exists to fill **missing or ambiguous** `profile.md` fields after ingestion.
Each section maps to one frontmatter field (or field pair).

**How to use it:**
- Ask about a field ONLY if you could not confidently extract it from `sources/`.
- Ask **one question at a time**. Wait for the answer before the next.
- Prefer **multiple-choice** (offer concrete options drawn from what you already
  know about the user) over open prompts — it's faster and easier to answer.
- Never re-ask something the CV/LinkedIn already answered. If a field is present but
  *ambiguous*, confirm rather than ask from scratch ("Your CV lists both X and Y —
  which do you want to target?").
- Skip optional fields gently; don't force an answer.

---

### Target titles  → `titles`
**Question:** "Which role titles are you targeting? (Pick any that fit, or add your own.)"
Offer options inferred from their history, e.g. *Backend Engineer · Tech Lead ·
Engineering Manager*.
**Good answer:** 1–4 concrete role titles they'd actually accept, not aspirational
fluff. Distinguish roles *held* from roles *targeted* if they differ.

### Seniority  → `seniority`
**Question:** "What seniority level are you aiming for?"
Offer: *junior / mid / senior / lead / staff / principal / director+*.
**Good answer:** one level (or a tight range) consistent with the years/scope in their
CV. If the CV implies a different level than they pick, surface the gap.

### Skills — core vs. familiar  → `skills.core`, `skills.familiar`
**Question:** "From the skills on your CV, which are your **core** strengths (the
ones you'd want to be hired for), and which are just **familiar** (working
knowledge)?" Present the extracted skill list and ask them to split it.
**Good answer:** a clear two-bucket split. Core = lead-with, defensible in an
interview. Familiar = honest working knowledge. Don't let everything be "core."

### Locations  → `locations`
**Question:** "Which locations are you open to?" Offer their current city + common
nearby hubs + *Remote*.
**Good answer:** specific cities/regions and/or a remote scope (e.g. "Remote-EU").

### Work mode  → `work_mode`
**Question:** "What's your preferred work mode?"
Offer: *remote / hybrid / onsite*.
**Good answer:** one preference. If hybrid, optionally note acceptable days onsite.

### Salary range  *(optional)*  → `salary_range`
**Question (asked gently):** "Optional — do you have a target salary range? It helps
filter postings, but you can skip it."
**Good answer:** a range with currency and period (e.g. "5500–6500 EUR/mo"), or an
explicit skip. Never pressure; record nothing if they decline.

### Must-haves  → `must_haves`
**Question:** "What are your non-negotiables — things a role MUST have for you to
consider it?" Offer examples to prime: *4-day week · strong eng culture · specific
tech · learning budget · no on-call*.
**Good answer:** 2–5 concrete requirements, not vague wishes.

### Deal-breakers  → `deal_breakers`
**Question:** "What are your hard nos — things that would make you reject a role
outright?" Offer examples: *full onsite · legacy-only stack · long commute ·
on-call rotation · no remote*.
**Good answer:** 2–5 concrete rejections. These are the inverse of must-haves; avoid
duplicating.

### Languages  → `languages`
**Question:** "Which languages do you work in, and at what level?"
Offer a starter from any hints (e.g. *Finnish (native) · English (fluent)*).
**Good answer:** each language with a proficiency tag (native / fluent /
professional / basic).

### Surfacing an understated achievement  → prose `## Signature achievements`
**Question:** "Looking at your experience, is there an accomplishment your CV
**undersells** — something with a real number or outcome behind it (revenue saved,
users served, time cut, team grown)?"
**Good answer:** one concrete, quantified achievement that strengthens the profile.
Capture the metric. Do not invent or inflate — if they have none beyond the CV, leave
the section as extracted.
