---
name: scan-targets
description: >
  This skill should be used when the user asks to "scan targets",
  "scan target companies", "check career pages", "find new roles at
  my target companies", "look for openings", "sweep my targets", or
  "scan for jobs". It sweeps the tracked target companies in the
  current job-tracker workspace for likely-fit roles using
  targets.md, AGENTS.md, and existing leads.
metadata:
  version: "0.2.0"
---

Scan target companies in the current job tracker workspace.

Use these sources:

- `AGENTS.md`
- `targets.md`
- `leads/**/*.md`

Workflow:

1. Read `AGENTS.md`, `targets.md`, and existing leads recursively with `leads/**/*.md`.
   For diffing against the previous sweep, read only the **last 1-2 entries** of `docs/scan-log.md`.
   Do not read the whole log, and do not read `docs/scan-log-archive.md` unless asked about history.
2. For each target company in `targets.md`, fetch the listed careers URL when accessible.
3. After fetching a careers page, extract individual job posting URLs from the raw HTML wherever possible — look for `href` attributes on job listing anchor tags (e.g. Greenhouse, Lever, Workday, or similar ATS link patterns). Use these direct URLs in all output rather than linking back to the generic careers page.
4. Look for likely-fit roles based on each target's `Target themes` plus any role preferences stated by the user.
5. Do not create lead files unless the user explicitly asks or a role is clearly strong and you ask for confirmation first.
6. Overwrite each scanned target's `Last scan` line in `targets.md` with its current status: date,
   accessible or blocked, posting count if known, new roles found, and any running count such as
   consecutive verified runs. This line is **state** — replace it, never append to it.
7. Append a dated entry to the end of `docs/scan-log.md` by default. Skip this only if the user
   explicitly asks for a read-only scan or no file updates. Do **not** append to `targets.md`; its
   `## Scan Log` section is a pointer only. If `docs/scan-log.md` has passed ~12 entries, move the
   oldest into `docs/scan-log-archive.md` (append there, preserving order) in the same run.
8. End the `docs/scan-log.md` entry with a **Fetch diagnostics** section. This is where every
   technical observation goes and the only place it goes in a per-run form: which boards were
   unreadable and why, URL shapes that did or did not work, pagination and parameter behaviour,
   bot-walls, and anything a future run should do differently. Keep it factual and terse. Anything
   that will still be true next run also goes in that org's `Notes` in `targets.md`; the diagnostics
   section is the per-run record and the trend, so a portal degrading over three runs is visible.
9. Keep the scan concise and factual, and keep the log entry disciplined:
   - Write only what changed since the previous entry.
   - Never restate prior runs. "Ninth consecutive run", "identical to every scan since 07-27",
     "118 jobs vs 119 last time" are status; they belong in the target's `Last scan` line. Carrying
     them into each entry is what makes a scan log grow without bound.
   - No bullet longer than roughly 300 characters or 2 sentences.
   - Aim for an entry under 80 lines. If it runs long, cut narrative, never the roles table.
   - The roles table is the point of the entry. Prose is support, not the deliverable.

## Two audiences, two documents

**The report is written for the job seeker. The scan log is written for whoever maintains the
scanner.** These are different readers and mixing them makes the report worse for the person it is
actually for.

The job seeker wants roles, fit, and what to do next. They do not want ATS names, portal mechanics,
URL-parameter findings, or fetch-tool behaviour. Keep all of that out of the report. It goes in the
scan log, under **Fetch diagnostics** (see below), and anything persistent also goes in that org's
`Notes` in `targets.md`.

The one technical fact the job seeker does need is **coverage**: which organizations could not be
read this run, so they know where the list is thin. State it as coverage, not cause — name the orgs,
not the reason.

Report format:

## Target Scan

- Date: today's date
- Organizations checked:
- Openings found:
- **Coverage note** — only if something could not be read. One plain sentence naming the
  organizations, e.g. "4 of 16 could not be checked this run, so there may be openings at Mary's
  Center, Unity Health Care, Chase Brexton and DC Health that are not listed here." No ATS names,
  no error descriptions, no mechanics.

## Likely-Fit Roles

Create a compact table with these columns:

- Company
- Role
- Location
- URL (direct job posting link where available)
- Why it may fit
- Suggested action

## What Changed

Role-level changes only: openings that appeared or closed since the last scan, and any that are
worth acting on now. Never portal or tooling changes.

## Recommended Next Moves

Give 3-5 practical next actions, such as creating a lead file, applying, finding a warm intro, or
refining target filters. Frame them as things the job seeker does, not maintenance tasks.

Privacy rules:

- Do not include personal contact details or unnecessary PII.
- Do not copy sensitive recruiter messages into reports or scan logs.

## HTML Export

After delivering the report in chat, write the full report as a self-contained HTML file to the `reports/` directory at the workspace root (the same directory that contains `AGENTS.md` and `leads/`). Name it `scan-report.html`. In a workspace whose targets are sharded by market (one scheduled run per market), name it `scan-<market>.html` instead — e.g. `scan-boston.html`, `scan-nj.html` — so each run writes its own report rather than overwriting another market's. Create `reports/` if it does not exist. Do this by default whenever a target scan is run, unless the user explicitly asked for a read-only scan or no file updates.

HTML requirements:

- Single file, no external dependencies (all CSS inline in a `<style>` block).
- `<meta name="viewport" content="width=device-width, initial-scale=1">` for mobile rendering.
- Font stack: `system-ui, -apple-system, sans-serif`.
- Body: `max-width: 700px; margin: 0 auto; padding: 1rem 1.25rem; color: #1a1a1a; background: #fff; line-height: 1.5;`
- Headings: `color: #111; margin-top: 2rem;`
- Tables: `width: 100%; border-collapse: collapse; font-size: 0.85rem; margin: 1rem 0;` wrapped in a `<div style="overflow-x:auto">` for horizontal scrolling on mobile.
- Table cells: `padding: 0.45rem 0.65rem; border: 1px solid #ddd; vertical-align: top;`
- Alternating table rows: `background: #f9f9f9` on even rows.
- Table headers: `background: #f0f0f0; font-weight: 600; text-align: left;`
- New roles (not in the prior scan): highlight with row background `#f0fdf4` and a small green "NEW" badge inline in the role cell.
- Role titles should be clickable links using the direct job posting URL if one was extracted; otherwise link to the company careers page.
- Coverage note (only when something could not be read): a single `#fffbeb` callout with an amber left border, naming the organizations in plain language. Do **not** render a blockers/technical section in the HTML at all — that belongs in `docs/scan-log.md`.
- Page header: report title, scan date, and "Auto-generated by scan-targets skill" in muted small text.
- Do not include any private contact details or unnecessary PII.

After writing the report file, update `reports/index.html`: set the `id="stamp-scan"` span to today's date in `YYYY-MM-DD` format. In a market-sharded workspace, set only that market's stamp span (`id="stamp-scan-<market>"`) and leave the other markets' stamps alone. Do not change the status stamp. If the index does not exist, create it using the template in `reports/index.html` in this repository.

After writing both files, provide a link to `reports/scan-report.html` so the user can open it directly.
