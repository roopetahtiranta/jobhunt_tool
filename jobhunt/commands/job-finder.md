---
description: Find live job postings matching your profile.md and write a ranked matches.md.
---

Invoke the **job-finder** skill to discover live postings matching the user's
`profile.md`.

Follow the instructions in `${CLAUDE_PLUGIN_ROOT}/skills/job-finder/SKILL.md` exactly:
read the skill and its referenced files, then run its process (read `profile.md`,
derive queries, discover via nimble-web-expert with plain-search fallback, write a
ranked `matches.md`).

If the user gave arguments, treat them as their job-hunt working folder path or
specific boards/URLs to target: $ARGUMENTS
