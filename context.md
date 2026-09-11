# job-seeker — Context

> **Notion project name:** job-seeker (not yet confirmed in Notion)
> **Last Updated:** 2026-06-14 (later session)
> **Status:** Active
> **Priority:** Medium

---

## Overview

Public, generic, open-source version of a Markdown-based job-search tracker "kit" — companion repo to Alex Gomez's private tracker `job-seeker-ag`. Provides a reusable folder structure (targets, leads, templates), AI-assistant prompt templates (`commands/`), and a Cowork plugin (`plugins/job-tracker/`, packaged as `job-tracker.plugin`) implementing three core workflows: scan-targets, add-lead, job-status-report (plus a 4th skill, `job-tracker-advanced`, not yet present in job-seeker-ag). Designed to be forked/copied and kept shareable — no personal data belongs in this repo.

---

## Tech Stack

- **Format:** Markdown workspace + Cowork plugin (skills) + AI-assistant command/prompt templates
- **Repo:** job-seeker (local at `C:\Data\Tech\GitHub\job-seeker`, git initialized)
- **Related repo:** `job-seeker-ag` (Alex's private/personal instance, local at `C:\Data\Tech\GitHub\job-seeker-ag`)
- **Hosting docs:** `docs/hosting.md` (Caddy + cloudflared + Cloudflare Access for publishing `reports/`)

---

## Current Status

Public kit is built and has shipped LinkedIn launch assets (2026-05-20). Core structure (README, AGENTS.md, templates, commands, plugin) is in place. `job-tracker.plugin` archive exists at repo root. Git history shows recent cleanup/migration work and addition of profile/resume templates with instructions (latest commit `fe0c7e5`).

**Key constraint:** This repo must stay generic. Any workflow, template, or skill improvements made in `job-seeker-ag` (Alex's private tracker) should be mirrored here — but never personal data: no real leads, target lists, profile content, resume content, or application statuses. Only `_template*.md` / `_example-redacted.md` style content belongs here.

---

## Project Files & Structure

| Path | Purpose |
|---|---|
| `README.md` | Project overview, quick start, full workflow docs |
| `AGENTS.md` | Working conventions for the generic tracker |
| `LICENSE` | Open-source license |
| `targets.md` | Empty/example target-company watchlist template |
| `notes.md` | Free-form scratch space; contains kit "talk track" / pitch notes and LinkedIn launch log |
| `commands/` | AI-assistant prompt templates (`scan-targets`, `add-lead`, `job-status-report`) |
| `leads/` | `_template.md`, `_template-minimal.md`, `_example-redacted.md` — no real leads |
| `resume/` | Resume template(s) only — no real resume content |
| `profile.md` | Generic profile template |
| `docs/hosting.md` | Self-hosting `reports/` via Caddy + cloudflared + Cloudflare Access |
| `reports/` | Generated report landing pages/templates |
| `linkedin/` | Launch assets: post copy, infographic, thumbnail, generation script |
| `plugins/job-tracker/` | Cowork plugin source: `scan-targets`, `add-lead`, `job-status-report`, `job-tracker-advanced` skills |
| `job-tracker.plugin` | Prebuilt installable plugin archive |

---

## Key Decisions & Rationale

| Decision | Rationale | Date |
|---|---|---|
| Split private tracker (job-seeker-ag) from this generic kit | Keep this repo shareable/public; no personal data risk | (pre-2026-05-14) |
| Ship as Markdown + prompt templates + optional Cowork plugin, no app/database | Lightweight, copyable, works with any AI assistant | (pre-2026-05-20) |
| LinkedIn positioning: lead with "local-first tracking + AI workflows," not layoffs | Broader appeal; layoffs kept as origin-story context only | 2026-05-20 |

---

## Open Threads

- [ ] Sync `job-tracker-advanced` skill (and any other drift) from job-seeker-ag's `plugins/job-tracker/` and vice versa — confirm which repo is currently ahead.
- [ ] Confirm Notion project record exists for "job-seeker" (not yet verified).

---

## Blockers

None currently noted.

---

## Related Projects

| Project | Relationship | Context path |
|---|---|---|
| job-seeker-ag (`C:\Data\Tech\GitHub\job-seeker-ag`) | Alex's private/personal instance of this kit, with real leads, targets, profile, and resume. Workflow/template/skill improvements should sync both ways; personal data never flows into this repo. | `C:\Data\Tech\GitHub\job-seeker-ag\context.md` |

---

## Session Log

### 2026-09-11
- **Split scan history out of `targets.md`, and separated state from history.** Two changes that go together; the second is the one that matters.
  - Scan history now lives in `docs/scan-log.md` (append-only). `targets.md` keeps a pointer stub that is never appended to. `docs/scan-log-archive.md` is created on first rotation, at ~12 entries.
  - Each target's `Scan status` field is renamed **`Last scan`** and is now explicitly *state*: overwritten every run, holding date, access result, posting count, new roles, and any running count such as consecutive verified runs.
- **Why the second change exists.** Found on 2026-09-11 while investigating `job-seeker-ag`: its `targets.md` had reached 308KB from **5 target companies**, of which 301KB was scan log — 98% of the file. Entries had grown from 1.8KB (2026-05-12) to 23.7KB (2026-09-10), roughly doubling every six weeks. Cause was not entry count but entry content: each run re-narrated prior runs ("ninth consecutive run", "identical to every scan since 07-27", "118 jobs vs 119 on 09-07"), so entry size tracked elapsed time rather than what was found. One bullet in the 09-10 entry was a single 8,520-byte line.
- The instruction driving it was this repo's own `targets.md` header, "append updates rather than overwriting useful history", propagated into instance `CLAUDE.md` files. Append-only is right for history and wrong for status. That line is rewritten here to say so.
- Skill and prompt changes: `scan-targets` now (a) reads only the last 1-2 log entries for diffing, (b) overwrites the `Last scan` line, (c) appends to `docs/scan-log.md` with a rotation step, and (d) carries explicit entry discipline — only what changed, no restating prior runs, no bullet over ~300 characters, entry under 80 lines, roles table is the deliverable and prose is support. Same rules mirrored into `commands/scan-targets.md`, `AGENTS.md`, and the new `docs/scan-log.md` header.
- `job-tracker-advanced` now reads the most recent entry from `docs/scan-log.md`. `README.md` and `plugins/job-tracker/README.md` updated. `job-tracker.plugin` rebuilt.
- **Propagation still owed** (this repo is the baseline, so it goes first — done here now): `job-seeker-ag` needs the skill change, the log split, the `Last scan` convention, a `CLAUDE.md` line-55 fix, and its scheduled scan prompt regenerated — note its prompts are self-contained, so a skill edit alone will not change automated runs. `job-seeker-aag` already has the log split (done 2026-09-11) but needs this entry-discipline change and the `Last scan` convention.


### 2026-06-14 (later session)
- Mirrored recent job-seeker-ag conventions into this repo: `AGENTS.md`, `commands/*.md`, and `plugins/job-tracker/skills/*/SKILL.md` (add-lead, scan-targets, job-status-report) updated.
  - Leads now use company folders: `leads/<company-name>/<role-title>.md`, created as needed; lookups/dedup now check `leads/**/*.md` recursively instead of flat `leads/*.md`.
  - scan-targets now appends `targets.md` scan log entries and writes `reports/scan-report.html` + updates `reports/index.html` stamp by default (not just when asked).
  - job-status-report now always writes `reports/job-status-report.html` + updates `reports/index.html` stamp by default, treated as a standing preference that overrides generic "don't modify files" instructions.
  - Also updated `README.md` (folder structure diagram, Quick Start) for the company-folder convention.
- Rebuilt `job-tracker.plugin` (zip of `.claude-plugin/`, `README.md`, `skills/` from `plugins/job-tracker/`) to pick up the SKILL.md changes.

### 2026-06-14
- Created initial `context.md` for the project.
- Established cross-repo sync rule with job-seeker-ag: mirror workflow/skill/template changes both ways, never personal data (real leads, targets, profile, resume, statuses) into this public repo.
- Noted plugin parity gap: this repo's plugin has 4 skills (including `job-tracker-advanced`); job-seeker-ag's currently has 3.
