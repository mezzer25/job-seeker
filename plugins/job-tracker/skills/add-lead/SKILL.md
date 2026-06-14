---
name: add-lead
description: >
  This skill should be used when the user asks to "add a lead",
  "create a job lead", "track this role", "log this opening", "make
  a lead file for this posting", "save this opportunity", or "I found
  a job to apply to". It creates a single markdown file under the
  current job-tracker workspace's leads/<company-name>/ directory,
  creating that company folder if needed, using the project's
  template and naming conventions.
metadata:
  version: "0.1.0"
---

Create a new job lead file in the current job tracker workspace from the job details the user provides.

Use these sources:

- `AGENTS.md`
- `leads/_template.md` (or `leads/_template-minimal.md` for early-stage or low-priority leads)
- Existing `leads/**/*.md` files to avoid duplicates and follow naming conventions.

Workflow:

1. Read `AGENTS.md` and the relevant template.
2. Check existing lead files recursively with `leads/**/*.md` for duplicates.
3. If the user provides a URL, fetch it if accessible and use the public job posting as the source.
4. Create one Markdown lead file at `leads/<company-name>/<role-title>.md`, such as `leads/exampleco/solutions-architect.md`. Create the company folder if it does not already exist.
5. Fill only facts that are provided or visible in the source. Use `To be confirmed` for unknowns.
6. Add tailored positioning based on the job posting and any user-supplied background.
7. Do not store direct phone numbers, personal emails, secrets, or unnecessary PII.
8. Do not overwrite existing lead files.

Naming rules:

- Use an existing company folder when one exists, preserving its casing.
- For new company folders, use lowercase kebab-case unless the company name has established casing in this tracker.
- Use lowercase kebab-case for the role filename.
- Do not create opportunity files directly under `leads/`; only templates and shared tracker files belong at the top level.

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
