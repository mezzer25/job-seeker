# job-tracker (Cowork plugin)

A Cowork plugin that packages the job-seeker kit's recurring workflows as installable skills.

## Skills

- **scan-targets** — Sweep target career pages and produce a structured scan report.
- **add-lead** — Create a new lead file in `leads/` from a URL or supplied job details, using the project's template and naming conventions.
- **job-status-report** — Consolidate active leads into a status report with follow-ups, stale items, and recommended next moves.
- **job-tracker-advanced** — Advanced workflows: rank opportunities, tailor positioning, draft outreach, prep interviews, build a weekly action plan, convert a scan into an application plan.

## Workspace Expectations

The skills assume the workspace follows the job-seeker kit conventions:

- `AGENTS.md` — operating rules
- `targets.md` — target-company watchlist and scan log
- `leads/` — one Markdown file per opportunity
- `leads/_template.md` — full template
- `leads/_template-minimal.md` — short template for early-stage leads

## Installation

The prebuilt `job-tracker.plugin` file at the repo root is a single-step install in Cowork: drop it into the chat or open it from your file manager, then click "Install."

To rebuild the `.plugin` archive after edits, zip the contents of this directory (not the directory itself) into a file named `job-tracker.plugin`.

## Setup

No environment variables or external services required. The plugin only reads and writes files in the active workspace.

## Privacy

Skills avoid copying direct phone numbers, personal emails, sensitive recruiter messages, private compensation notes, or unnecessary PII into reports or files. The status-report skill also skips the lead templates and the redacted example file when summarizing.

## Source

This plugin's source lives in `plugins/job-tracker/` inside the job-seeker kit repo. The `commands/` folder at the repo root preserves the same workflows as plain prompts for users of other AI tools (OpenCode, ChatGPT, Cursor, etc.).
