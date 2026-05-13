# Job Seeker Tracker Kit

A lightweight job-search operating system built from Markdown files and optional OpenCode commands.

This kit is intended for people managing multiple job opportunities, especially after a displacement or layoff. It keeps target companies, active leads, follow-ups, interview prep, and weekly status reporting in one simple folder without requiring a database, SaaS tool, or CRM.

## What This Does

- Tracks one job opportunity per Markdown file.
- Maintains a recurring target-company watchlist.
- Produces concise job-search status reports with OpenCode.
- Helps organize follow-up actions by urgency.
- Captures role fit, risks, positioning, company facts, contacts, application materials, and interview prep.
- Encourages privacy-safe tracking that avoids unnecessary personally identifiable information.

## Folder Structure

```text
job-seeker/
  README.md
  AGENTS.md
  targets.md
  leads/
    _template.md
    _example-redacted.md
  commands/
    job-status-report.md
    scan-targets.md
    add-lead.md
  optional/
    job-tracker-skill/
      SKILL.md
```

## Quick Start

1. Copy this folder to a private workspace.
2. Edit `targets.md` with companies and career-page URLs you want to monitor.
3. Copy `leads/_template.md` for each job opportunity you want to track.
4. Name lead files with lowercase kebab-case, such as `exampleco-solutions-architect.md`.
5. Use `AGENTS.md` as the operating guide for OpenCode sessions in this folder.
6. Optionally copy files from `commands/` into your OpenCode commands folder.

Typical OpenCode commands folder:

```text
~/.config/opencode/commands/
```

On Windows, this is commonly:

```text
C:\Users\<you>\.config\opencode\commands\
```

## Basic Workflow

1. Add target companies to `targets.md`.
2. Ask OpenCode to scan targets or use `/scan-targets` if installed.
3. Create a lead file for each promising role.
4. Update lead files after applications, conversations, interviews, and follow-ups.
5. Run `/job-status-report` weekly to summarize status and next actions.

## Status Values

Use these status values consistently:

- `researching`
- `applied`
- `warm-intro`
- `screening`
- `interviewing`
- `offer`
- `closed`
- `paused`

## OpenCode Commands

This kit includes command templates in `commands/`.

- `/job-status-report`: summarize active leads, status counts, follow-ups, stale/risky leads, and recommended next moves.
- `/scan-targets`: check career URLs in `targets.md`, summarize likely-fit roles, and append a scan log.
- `/add-lead`: create a new lead file from pasted job details or a job URL.

To install a command, copy the corresponding Markdown file into your OpenCode commands folder. Restart OpenCode if the command does not appear immediately.

## Privacy Guidance

- Assume this folder may eventually be shared or committed.
- Do not store direct phone numbers, personal emails, secrets, or credentials.
- Do not copy recruiter messages verbatim unless you are certain the folder is private.
- Summarize sensitive conversations instead of storing full messages.
- Keep public resume or portfolio material separate from private lead notes.
- Use `_example-redacted.md` as the pattern for shareable examples.

## What You Can Add Later

- Resume-tailoring command.
- Outreach and follow-up draft command.
- Interview prep command.
- Fit scoring by role and company.
- Weekly metrics report.
- CSV export.
- Calendar/task integration.
- Static dashboard.
- Optional skill for more advanced workflows.

## Pitch Summary

This is a practical, low-friction job-search operating system for people managing multiple opportunities. It uses Markdown and OpenCode instead of a heavy CRM, making it easy to copy, customize, and keep private. It helps job seekers stay organized, follow up consistently, and turn scattered job activity into a repeatable workflow.
