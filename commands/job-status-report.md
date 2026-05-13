---
description: Report status across job seeker leads
---
Create a concise job-search status report for the current job tracker workspace.

Use these sources:

- `AGENTS.md`
- `targets.md`
- `leads/*.md`

Before reporting:

- Read the tracker guide and target list for context.
- Read every top-level Markdown lead file in `leads/` except `_template.md` and `_example-redacted.md`.
- Do not include private contact details, phone numbers, direct personal emails, sensitive recruiter messages, private compensation notes, or unnecessary PII.
- Do not modify files unless I explicitly ask you to update the tracker.

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
