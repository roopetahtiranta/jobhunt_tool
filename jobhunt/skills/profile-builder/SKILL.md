---
name: profile-builder
description: Build or update an applicant profile for the jobhunt workflow. Ingestion-first — reads the user's CV (PDF/docx) and LinkedIn data from a sources/ folder, then interviews only to fill gaps. Use when the user wants to set up their job-application profile, import their CV/LinkedIn, or refresh profile.md. Triggers: "build my profile", "set up my job hunt", "import my CV".
---

# profile-builder

Produce and maintain `profile.md`, the shared contract for the jobhunt plugin.

## Process

1. Ask the user for their job-hunt working folder (or offer to create one). Expect a `sources/` subfolder.
2. Read everything in `sources/`. For PDFs use the `pdf` skill; for .docx use the `docx` skill; read .md/.txt directly. Also accept pasted LinkedIn profile text or an exported PDF.
3. Draft `profile.md` from `references/profile-template.md`, filling every field you can confidently extract. Leave unknown fields empty.
4. Interview the user to fill ONLY the empty/ambiguous fields, using `references/interview-questions.md`. Ask ONE question at a time, multiple-choice when possible. Never re-ask something the sources already answered.
5. If the CV and LinkedIn conflict, surface the conflict and ask which is correct — do not silently pick one.
6. Present the completed draft and ask for approval. Save to `<folder>/profile.md` only after the user approves.
7. Set `updated:` to today's date.

## Rules
- Ingestion-first: minimize what you ask the user to type.
- Do not invent achievements or skills. Only record what sources or the user state.
- Keep frontmatter machine-clean (valid YAML, lists as lists). Keep prose human.

## References
- `references/profile-template.md` — the exact skeleton to produce.
- `references/interview-questions.md` — questions per field, for gaps only.
