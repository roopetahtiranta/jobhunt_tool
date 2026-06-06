# jobhunt_tool

**An AI-native job-application copilot** — packaged as an installable Claude/Cowork
plugin. Build a structured applicant profile from your existing CV and LinkedIn data,
discover live job postings that match it, and get a deep, honest analysis of any
posting: fit score, positioning angle, red/green flags, and tailored talking points.

The plugin itself lives in [`jobhunt/`](jobhunt/) and is packaged as `jobhunt.plugin`.

---

## What's inside

Three modular skills that share **one `profile.md` file** as their common contract —
every skill reads it; the pipeline skills write their outputs alongside it.

| Skill | What it does | Reads | Writes |
|---|---|---|---|
| **profile-builder** | Ingestion-first: parses your CV (PDF/docx) and LinkedIn data, then interviews you *only* to fill gaps. | `sources/` | `profile.md` |
| **job-finder** | Derives search queries from your profile and finds live postings. | `profile.md` | `matches.md` |
| **posting-analyzer** | Analyzes one posting against your profile — fit, positioning, flags, talking points. | `profile.md` + a posting | `analyses/<company-role>.md` |

---

## Install

You need [Claude Code](https://claude.com/claude-code) (or another Claude/Cowork
client that supports plugins).

**Option A — install the packaged plugin**

1. Download [`jobhunt.plugin`](jobhunt.plugin) from this repo.
2. Install it through your client's plugin manager (it's a standard plugin archive).

**Option B — load the folder directly**

Place the [`jobhunt/`](jobhunt/) directory under your Claude plugins directory.

No API keys are required.

> **Optional but recommended:** install [`nimble-web-expert`](#live-web-access)
> for higher-quality live job-board search. The plugin works without it.

---

## Set up your job-hunt folder

All your data lives in a working folder you choose — **not** inside the plugin. Create
one anywhere, with a `sources/` subfolder for your raw inputs:

```
my-job-hunt/
  sources/            # ← drop your CV and LinkedIn export here
    cv.pdf
    linkedin.pdf
```

After you run the skills, it fills out like this:

```
my-job-hunt/
  profile.md                  # built by profile-builder
  sources/                    # your inputs
  matches.md                  # built by job-finder
  analyses/
    northwind-backend-lead.md # built by posting-analyzer (one file per posting)
```

---

## How to use it

Point Claude at your job-hunt folder and run the three skills in order. You drive it
with plain language — the triggers below are examples, not exact commands.

### 1. Build your profile

> *"Build my job-hunt profile from the files in `my-job-hunt/sources/`."*

profile-builder reads everything in `sources/` (CV + LinkedIn), drafts your
`profile.md`, then asks you a **few** targeted questions only about what it couldn't
extract — things like target seniority, work mode, salary range, must-haves, and
deal-breakers. One question at a time, multiple-choice where possible. It saves
`profile.md` only after you approve the draft.

*No CV handy?* It falls back to a fuller interview. *CV and LinkedIn disagree?* It
surfaces the conflict and asks you which is right — it won't silently pick one.

### 2. Find matching jobs

> *"Find jobs that match my profile."*

job-finder reads `profile.md`, derives search queries from your titles, core skills,
locations, and work mode, and writes a ranked `matches.md` — a table of company, role,
location, link, and a one-line "why it fits you." It respects your must-haves,
deal-breakers, and location/work-mode preferences when filtering.

If live search is thin (or `nimble-web-expert` isn't installed), it asks you to paste
posting URLs or name specific boards rather than inventing results.

### 3. Analyze a posting

> *"Analyze this posting against my profile: <paste a URL or the job text>"*

posting-analyzer is the centerpiece. Give it a posting (a row from `matches.md`, a
URL, or pasted text) and it produces a four-part analysis saved to
`analyses/<company>-<role>.md`:

1. **Fit score & gap analysis** — an overall score plus a requirement-by-requirement
   table marking each one **Meet / Partial / Lack**, with evidence from your profile.
2. **Positioning angle** — which 2–3 experiences to lead with for *this* role, the
   "why now" behind the role, and a one-sentence strategic spine.
3. **Red & green flags** — reading between the lines: vague comp, scope creep, culture
   tells, growth signals.
4. **Tailored talking points** — résumé tweaks, cover-letter hooks, and draft answers
   to likely screening questions.

**Honesty guarantee:** every "Meet" must cite real evidence from your profile, gaps
are named "Lack" plainly, and it never invents qualifications you don't have. An
honest read is what keeps you safe in the actual interview.

---

## Live web access

`job-finder` and `posting-analyzer` need to reach the live web. They prefer
[`nimble-web-expert`](https://github.com/nimbleway) (Nimble Web Search Agents), which
is purpose-built to search and fetch job boards (LinkedIn, Indeed, company career
pages) as a managed layer.

`nimble-web-expert` is **not required**. When it's absent, the plugin falls back to
plain web search and asks you to supply posting URLs directly — so it stays portable
and shareable.

---

## The profile.md contract

`profile.md` is Markdown with a YAML frontmatter block (structured fields) plus prose
sections. It's human-editable, git-friendly, and read natively by AI tools — you can
hand-edit it any time. Frontmatter fields include: `name`, `titles`, `seniority`,
`skills` (split into `core` / `familiar`), `locations`, `work_mode`, `salary_range`,
`must_haves`, `deal_breakers`, `languages`, and `updated`. Prose sections cover your
professional summary, signature achievements, career narrative, and positioning notes.

See [`jobhunt/skills/profile-builder/references/profile-template.md`](jobhunt/skills/profile-builder/references/profile-template.md)
for the canonical skeleton.

---

## Try it with the included fixtures

The [`fixtures/`](fixtures/) folder has sample data so you can see the workflow without
using your own:

- `sample-cv.md` — a fake CV to feed profile-builder.
- `sample-profile.md` — a filled profile to feed job-finder / posting-analyzer.
- `sample-posting.md` — a fake job posting to analyze.

Example: *"Analyze `fixtures/sample-posting.md` against `fixtures/sample-profile.md`."*
You should see at least one requirement honestly marked **Lack** (the posting wants a
people-manager; the sample profile has only mentoring experience).

---

## Status & roadmap

- **v0.1.0 (current):** profile-builder, job-finder, posting-analyzer.
- **Planned:** application-writer (cover letters / tailored CV bullets / screening
  answers) and an application tracker.

## License

[MIT](LICENSE)
