---
description: Scan target company career pages
---
Scan target companies in the current job tracker workspace.

Use these sources:

- `AGENTS.md`
- `targets.md`
- `leads/*.md`

Workflow:

1. Read `AGENTS.md` and `targets.md`.
2. For each target company in `targets.md`, fetch the listed careers URL when accessible.
3. Look for likely-fit roles based on each target's `Target themes` plus any role preferences stated by the user.
4. Do not create lead files unless the user explicitly asks or a role is clearly strong and you ask for confirmation first.
5. Append a dated entry to the `## Scan Log` section of `targets.md` if the user asked you to update the tracker.
6. Keep the scan concise and factual.

Report format:

## Target Scan

- Date: today's date
- Targets scanned:
- Accessible:
- Blocked or limited:

## Likely-Fit Roles

Create a compact table with these columns:

- Company
- Role
- Location
- URL
- Why it may fit
- Suggested action

## Blockers

List career pages that were blocked, empty, JavaScript-only, or otherwise unreliable.

## Recommended Next Moves

Give 3-5 practical next actions, such as creating a lead file, applying, finding a warm intro, or refining target filters.

Privacy rules:

- Do not include personal contact details or unnecessary PII.
- Do not copy sensitive recruiter messages into reports or scan logs.
