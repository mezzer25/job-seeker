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
