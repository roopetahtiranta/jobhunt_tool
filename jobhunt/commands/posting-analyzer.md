---
description: Analyze one job posting against your profile.md — fit score, positioning, red/green flags, and tailored talking points.
---

Invoke the **posting-analyzer** skill to analyze a single posting against the user's
`profile.md`.

Follow the instructions in `${CLAUDE_PLUGIN_ROOT}/skills/posting-analyzer/SKILL.md`
exactly: read the skill and its referenced templates/guide, then run its process and
honor its honesty rules (every "Meet" cites profile evidence; gaps named "Lack"; never
fabricate qualifications). Save the result to `analyses/<company>-<role>.md`.

The user's arguments are the posting to analyze — a URL, pasted job text, or a
`matches.md` entry: $ARGUMENTS
