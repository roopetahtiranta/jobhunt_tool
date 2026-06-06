---
name: posting-analyzer
description: Analyze one job posting against the applicant's profile.md — produces fit score + gap analysis, positioning angle, red/green flags, and tailored talking points. Use when the user shares a posting (URL or text) and wants to know how well they fit and how to apply. Triggers: "analyze this job", "should I apply", "how do I fit this role".
---

# posting-analyzer

Deeply analyze a single posting against `profile.md`.

## Process
1. Locate `profile.md` in the job-hunt folder. If absent, tell the user to run profile-builder first.
2. Obtain the posting: from a `matches.md` entry, a URL, or pasted text.
   - For a URL, fetch via `nimble-web-expert` if available; otherwise fetch plainly. (See job-finder's `references/nimble-usage.md` for the detection + fallback pattern; the same applies here.)
3. Produce the analysis using `references/analysis-template.md`, following the honesty rules in `references/positioning-guide.md`.
4. Save to `<folder>/analyses/<company>-<role>.md` (kebab-case, lowercase). Show the user a summary.

## Rules
- Every "Meet" must cite evidence from the profile. Gaps are named "Lack" — never hidden.
- Do not invent qualifications. Talking points frame real experience; they never fabricate.
- Be concrete: scores justified, flags tied to specific posting language.

## References
- `references/analysis-template.md` — the 4-part output.
- `references/positioning-guide.md` — positioning method + honesty rules.
