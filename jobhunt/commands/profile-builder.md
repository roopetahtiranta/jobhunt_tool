---
description: Build or update your applicant profile (profile.md) from your CV and LinkedIn data, interviewing only to fill gaps.
---

Invoke the **profile-builder** skill to build or update the user's `profile.md`.

Follow the instructions in `${CLAUDE_PLUGIN_ROOT}/skills/profile-builder/SKILL.md`
exactly: read the skill and its referenced templates, then run its process
(ingestion-first from `sources/`, interview only to fill gaps, save only after the
user approves).

If the user gave arguments, treat them as the path to their job-hunt working folder
or `sources/` directory: $ARGUMENTS
