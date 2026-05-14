---
name: job-status-report
description: >
  This skill should be used when the user asks for a "job status
  report", "status of my job search", "where am I in my search",
  "summarize my applications", "weekly job recap", "show me all my
  leads", or "what's happening with my job hunt". It consolidates
  every active opportunity in the current job-tracker workspace into
  a single structured report with follow-ups and risks flagged.
metadata:
  version: "0.1.0"
---

Create a concise job-search status report for the current job tracker workspace.

Use these sources:

- `AGENTS.md`
- `targets.md`
- `leads/*.md`

Before reporting:

- Read the tracker guide and target list for context.
- Read every top-level Markdown lead file in `leads/` except `_template.md`, `_template-minimal.md`, and `_example-redacted.md`.
- Do not include private contact details, phone numbers, direct personal emails, sensitive recruiter messages, private compensation notes, or unnecessary PII.
- Do not modify files unless the user explicitly asks you to update the tracker.

Report format:

## Job Search Status

- Date: today's date
- Total active leads:
- Status counts: `researching`, `applied`, `warm-intro`, `screening`, `interviewing`, `offer`, `closed`, `paused`
- Highest-priority items:

## Lead Summary

Create a compact table with these columns:

- Company
- Role
- Status
- Priority
- Applied / Shared Date
- Last Updated
- Next Action

## Follow-Ups

List open follow-up tasks grouped by urgency:

- Today / next 24 hours
- This week
- Waiting / blocked

If urgency is not explicit, infer it conservatively from status, last update, and task wording.

## Stale Or Risky

Flag leads that need attention because:

- no update in 7+ days
- no warm-contact path identified
- company facts are unverified
- application is submitted but no follow-up action exists
- role fit or compensation risk is noted

## Recommended Next Moves

Give 3-5 practical next actions. Prioritize warm intros, time-sensitive follow-ups, and high-fit roles.

Keep the report concise and factual. Include file references when citing specific lead context.
