# Job Seeker Agent Guide

## Purpose

- This folder is a private job-search workspace.
- It tracks target companies, roles, contacts, application status, interview prep, positioning, and follow-up actions.
- Keep the system simple: Markdown files first, no database, no app framework, no automation beyond AI-assistant command prompts unless explicitly added.

## Context Files — Read These First

Before running any workflow, read the following files if they exist. They provide the
personal context needed to evaluate role fit, generate useful recommendations, and
write on the user's behalf.

### profile.md
Located at the repo root. Contains target roles, preferred industries, company size and
stage preferences, location and remote preferences, must-haves, nice-to-haves,
deal-breakers, a career summary, and any explicit notes from the user about what they
want next.

Treat `profile.md` as the source of truth for what the user is looking for. When
evaluating any role — whether scanning targets, reviewing a lead, or generating a status
report — assess fit against this profile first.

### resume/ folder
Located at `resume/` in the repo root. May contain one or more Markdown resume files.

- If a single file exists (e.g., `resume.md`), read it.
- If multiple files exist (e.g., `resume-engineering.md`, `resume-management.md`), use
  the one most relevant to the current task, or ask the user which to use if unclear.
- `resume/_template.md` is a blank template — skip it unless the user asks about it.
- Do not attempt to read PDF or Word files in this folder; use only Markdown versions.

Use the resume to identify skills and experience that match or gap against a job
description, inform fit notes in lead files, and suggest how the user might tailor
their application materials for a specific role.

**Privacy reminder:** `resume/` may contain personally identifiable information. Do not
quote it verbatim in reports or outputs intended to be shared. Summarize instead.

---

## Main Files And Folders

- `README.md` - Setup and usage instructions.
- `profile.md` - Career profile: target roles, preferences, must-haves, and background summary. Read before every workflow.
- `resume/` - Plain-text Markdown resume(s). Read alongside `profile.md` to evaluate fit.
- `resume/_template.md` - Blank resume template; copy and rename to fill in.
- `targets.md` - Recurring target-company career search list. Each target's `Last scan` line is overwritten each run.
- `docs/scan-log.md` - Scan history, append-only. Read only the last 1-2 entries.
- `docs/scan-log-archive.md` - Older scan entries, created on first rotation. Read only if asked about scan history.
- `leads/` - Company folders, each containing one Markdown file per opportunity (`leads/<company-name>/<role-title>.md`).
- `leads/_template.md` - Full template for new lead files.
- `leads/_template-minimal.md` - Short template for early-stage or low-priority leads.
- `leads/_example-redacted.md` - Safe example lead with no personal details.
- `commands/` - Optional AI-assistant command/prompt templates (work with OpenCode, Claude, ChatGPT, Cursor, and similar).
- `plugins/job-tracker/` - Source for the Cowork plugin that packages the workflows as skills (`scan-targets`, `add-lead`, `job-status-report`, `job-tracker-advanced`).
- `job-tracker.plugin` - Prebuilt plugin archive for one-step install in Cowork.

## Lead Tracking

- Use `targets.md` for recurring company career pages and scan notes before creating individual lead files.
- Use `leads/` for opportunity-specific tracking.
- Store each opportunity in a company folder: `leads/<company-name>/<role-title>.md`, for example `leads/exampleco/solutions-architect.md`. Create the company folder if it does not already exist.
- Use an existing company folder when one exists, preserving its casing. For new company folders, use lowercase kebab-case unless the company name has established casing in this tracker.
- Use lowercase kebab-case for role filenames.
- Check existing leads recursively with `leads/**/*.md` before creating a new file to avoid duplicates. Do not create opportunity files directly under `leads/`; only templates and shared tracker files belong at the top level.
- Use `_template-minimal.md` for early-stage or low-priority leads; promote to `_template.md` once a lead is in screening, warm-intro, or interviewing.
- Track role links, company context, contact names, warm intros, application status, interview notes, follow-up tasks, and tailored positioning.
- Suggested status values: `researching`, `applied`, `warm-intro`, `screening`, `interviewing`, `offer`, `closed`, `paused`.
- Keep lead notes factual and dated.
- Preserve prior notes; append updates instead of overwriting useful history.
- When preparing tailored resume or application language, ground recommendations in the job posting, resume, and existing lead notes.

## Target Scanning

- Use `targets.md` as the source of companies and career URLs to scan.
- Record scan dates and outcomes in `docs/scan-log.md` by default whenever a target scan is run, unless the user explicitly asks for a read-only scan or no file updates. Overwrite the target's `Last scan` line in `targets.md` in the same run.
- **An unchanged roster is a signal to inspect, not to stay quiet about.** Some career boards apply query parameters client-side and return a default or stale payload to a server-side fetch, which makes "nothing changed" indistinguishable from "the fetch silently failed". Where a target's `Fetch mechanics` names a browser as the required path, use it; where a run cannot, mark that target UNVERIFIED in the report rather than reporting a clean scan. Never suppress an unchanged-roster observation on the assumption that the target is simply quiet.
- Keep state and history apart: cumulative facts about a target (streaks, posting counts, verification status) go in its `Last scan` line and are overwritten; the log records only what changed that run. Restating prior runs in the log is what makes it grow without bound.
- Update `reports/scan-report.html` and the scan stamp in `reports/index.html` by default whenever a target scan is run, under the same exception.
- If a career site blocks automated access, note the limitation and ask for a direct job URL or manual review.
- Create dedicated lead files only for roles worth pursuing or explicitly requested.

## Privacy And Safety

- Treat this folder as private-ish, not guaranteed private.
- Do not store secrets, API keys, credentials, or tokens.
- Avoid storing direct phone numbers, personal email addresses for contacts, or unnecessary PII.
- Do not copy sensitive recruiter messages or private contact details into shareable files.
- Summarize sensitive conversations instead of storing full transcripts.
- If a lead includes sensitive information, flag it before sharing, committing, or publishing.

## Reporting

- Status reports should be concise and factual.
- Use root project files (`AGENTS.md`, `profile.md`, `targets.md`) and recursive lead folders (`leads/**/*.md`) as sources.
- Prioritize active leads, stale leads, warm intros, upcoming deadlines, and next actions.
- Always write `reports/job-status-report.html` and update the status stamp in `reports/index.html` whenever the user asks for a job status report. Treat this as the user's standing preference even if a pasted generic prompt says not to modify files; skip these report-file updates only if the user explicitly says the status report is read-only or says not to update report files.
- Do not expose private contact details in reports unless explicitly requested.

## Tooling

- The recurring workflows are available in two forms: plain prompt templates in `commands/` (for OpenCode, Claude, ChatGPT, Cursor, and similar) and a Cowork plugin in `plugins/job-tracker/`.
- The Cowork plugin packages four skills: `scan-targets`, `add-lead`, `job-status-report`, and `job-tracker-advanced` (ranking, positioning, outreach drafts, interview prep, weekly planning).
- When a request matches one of these workflows, follow the steps defined in the relevant `commands/*.md` or `SKILL.md` file instead of improvising.
- Both forms assume the file layout described above. Keep filenames and conventions stable so the workflows keep working.
- Rebuild `job-tracker.plugin` by zipping the contents of `plugins/job-tracker/` after edits.

## Sharing This Kit

- Share the templates, commands, plugin source, prebuilt `job-tracker.plugin`, and redacted examples.
- Do not share real lead files without reviewing and redacting them first.
- Do not include personal resumes, phone numbers, recruiter messages, or private contact details in a reusable copy.
