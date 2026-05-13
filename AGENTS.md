# Job Seeker Agent Guide

## Purpose

- This folder is a private job-search workspace.
- It tracks target companies, roles, contacts, application status, interview prep, positioning, and follow-up actions.
- Keep the system simple: Markdown files first, no database, no app framework, no automation beyond OpenCode commands unless explicitly added.

## Main Files And Folders

- `README.md` - Setup and usage instructions.
- `targets.md` - Recurring target-company career search list and scan log.
- `leads/` - One Markdown file per company or opportunity.
- `leads/_template.md` - Template for new lead files.
- `leads/_example-redacted.md` - Safe example lead with no personal details.
- `commands/` - Optional OpenCode command templates.
- `optional/job-tracker-skill/` - Optional skill scaffold for advanced workflows.

## Lead Tracking

- Use `targets.md` for recurring company career pages and scan notes before creating individual lead files.
- Use `leads/` for opportunity-specific tracking.
- Prefer one Markdown file per company or opportunity.
- Use lowercase kebab-case filenames, such as `exampleco-solutions-architect.md`.
- Track role links, company context, contact names, warm intros, application status, interview notes, follow-up tasks, and tailored positioning.
- Suggested status values: `researching`, `applied`, `warm-intro`, `screening`, `interviewing`, `offer`, `closed`, `paused`.
- Keep lead notes factual and dated.
- Preserve prior notes; append updates instead of overwriting useful history.
- When preparing tailored resume or application language, ground recommendations in the job posting, resume, and existing lead notes.

## Target Scanning

- Use `targets.md` as the source of companies and career URLs to scan.
- Record scan dates and outcomes in the scan log.
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
- Prioritize active leads, stale leads, warm intros, upcoming deadlines, and next actions.
- Do not expose private contact details in reports unless explicitly requested.

## Sharing This Kit

- Share the templates, commands, and redacted examples.
- Do not share real lead files without reviewing and redacting them first.
- Do not include personal resumes, phone numbers, recruiter messages, or private contact details in a reusable copy.
