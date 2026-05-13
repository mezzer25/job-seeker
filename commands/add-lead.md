---
description: Create a job lead from role details
---
Create a new job lead file in the current job tracker workspace from the job details I provide.

Use these sources:

- `AGENTS.md`
- `leads/_template.md`
- Existing `leads/*.md` files to avoid duplicates and follow naming conventions.

Workflow:

1. Read `AGENTS.md` and `leads/_template.md`.
2. Check existing top-level lead files in `leads/` for duplicates.
3. If I provide a URL, fetch it if accessible and use the public job posting as the source.
4. Create one Markdown lead file using lowercase kebab-case, such as `company-role-title.md`.
5. Fill only facts that are provided or visible in the source. Use `To be confirmed` for unknowns.
6. Add tailored positioning based on the job posting and any user-supplied background.
7. Do not store direct phone numbers, personal emails, secrets, or unnecessary PII.
8. Do not overwrite existing lead files.

Default status rules:

- If already applied, use `applied`.
- If a contact reached out or an intro exists, use `warm-intro`.
- If evaluating only, use `researching`.
- If interviews are scheduled or underway, use `screening` or `interviewing` as appropriate.

After creating the file, report:

- File created
- Status
- Priority
- Key fit points
- Gaps or risks
- Recommended next action
