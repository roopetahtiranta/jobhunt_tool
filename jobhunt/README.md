# jobhunt — AI Job-Application Copilot

`jobhunt` is a Claude/Cowork plugin: a bundle of three modular skills that help a
person apply to jobs. Build a structured applicant profile from your existing CV
and LinkedIn data, discover live postings that match it, and get a deep, honest
analysis of any posting — fit score, positioning angle, red/green flags, and
tailored talking points.

## The three skills

| Skill | What it does | Output |
|---|---|---|
| **profile-builder** | Ingestion-first: reads your CV (PDF/docx) and LinkedIn data from a `sources/` folder, then interviews you only to fill gaps. | `profile.md` |
| **job-finder** | Derives search queries from your profile and discovers live postings (via `nimble-web-expert` when available, plain web search otherwise). | `matches.md` |
| **posting-analyzer** | Analyzes one posting against your profile: fit + gap analysis, positioning angle, red/green flags, tailored talking points. | `analyses/<company-role>.md` |

## profile.md is the contract

Everything is built around a single shared **profile** file. `profile.md` (Markdown
with YAML frontmatter) is the contract between all three skills: every skill reads
it, and the pipeline skills write their outputs alongside it. It is human-editable,
git-friendly, read natively by AI tools, and presentable as a portfolio artifact.

## Working-folder layout

All artifacts live in a user-chosen working folder (your "job hunt" folder), **not**
inside the plugin:

```
job-hunt/
  profile.md              # the shared contract (profile-builder output)
  sources/                # your CV, LinkedIn export, etc. (profile-builder input)
  matches.md              # ranked postings + quick-fit (job-finder output)
  analyses/
    acme-backend-lead.md  # full per-posting analysis (posting-analyzer output)
```

## Live web access

`job-finder` and `posting-analyzer` use **`nimble-web-expert`** (Nimble Web Search
Agents) as the preferred engine for live web access — it is purpose-built to search
and fetch job boards (LinkedIn, Indeed, company career pages) as a managed layer.
Nimble is **not a hard dependency**: when it is absent, the plugin falls back to plain
web search and asks you to supply posting URLs directly, so it remains portable and
shareable.

No API keys are required.

## Install

1. Place the `jobhunt/` directory under your Claude plugins directory, **or** install
   the packaged `jobhunt.plugin` file through your plugin manager.
2. Start with `profile-builder` ("build my profile"), then use `job-finder`
   ("find me jobs") and `posting-analyzer` ("analyze this job") as needed.

## Two ways to invoke each skill

- **Natural language (skills auto-trigger):** just describe the task — *"build my
  jobhunt profile from my sources folder"*, *"find me jobs"*, *"analyze this posting:
  <url>"*. Skills are model-invoked from their descriptions.
- **Slash commands:** the plugin also ships explicit commands, so you can type them
  directly:
  - `/jobhunt:profile-builder [folder]`
  - `/jobhunt:job-finder [folder | boards]`
  - `/jobhunt:posting-analyzer <url | pasted text | matches.md entry>`

## Typical workflow

1. **profile-builder** → drop your CV/LinkedIn into `sources/`, answer a few gap
   questions, get `profile.md`.
2. **job-finder** → discovers matching postings into `matches.md`.
3. **posting-analyzer** → pick a posting (a `matches.md` entry, a URL, or pasted
   text) and get a full analysis to guide your application.
