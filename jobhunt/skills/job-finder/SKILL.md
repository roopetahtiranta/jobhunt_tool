---
name: job-finder
description: Find live job postings matching the applicant's profile.md. Uses nimble-web-expert to search job boards when available, falling back to plain web search and user-supplied URLs. Produces a ranked matches.md. Use when the user wants to discover jobs to apply to. Triggers: "find me jobs", "search for openings", "what should I apply to".
---

# job-finder

Discover live postings matching `profile.md` and write a ranked `matches.md`.

## Process
1. Read `profile.md`. If absent, tell the user to run profile-builder first.
2. Derive search queries from titles, core skills, locations, and work_mode.
3. Discover + fetch postings using the engine in `references/nimble-usage.md`
   (nimble-web-expert primary, plain web search + user URLs as fallback).
4. For each promising posting, write a row in `references/matches-template.md` format:
   company, role, location, link, and a one-line quick-fit tied to the profile.
5. Rank by quick-fit strength. Save to `<folder>/matches.md`. Show the top results.
6. If discovery is thin, ask the user for URLs or specific boards — never block.

## Rules
- Respect must_haves / deal_breakers / locations / work_mode when filtering.
- Quick-fit lines must reference the profile, not generic praise.
- Do not fabricate postings or links — only list ones actually found/fetched.

## References
- `references/nimble-usage.md` — live web access + fallback.
- `references/matches-template.md` — output table format.
