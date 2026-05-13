# Job Tracker Skill

Use this skill for advanced job-search tracking workflows that require branching, prioritization, or multi-step decision support beyond a simple command.

## When To Use

Use this skill when the user asks to:

- Compare multiple roles and rank fit.
- Generate tailored resume positioning for a specific role.
- Draft outreach or follow-up messages from lead context.
- Prepare interview talking points from a job posting and lead file.
- Review stale leads and recommend a weekly action plan.
- Convert target scan results into a prioritized application plan.

For simple recurring tasks, prefer commands:

- `/job-status-report`
- `/scan-targets`
- `/add-lead`

## Sources To Read

Before making recommendations, read relevant files from the tracker workspace:

- `AGENTS.md`
- `targets.md`
- `leads/*.md`
- Resume or positioning notes if the user provides them
- Public job postings when URLs are provided and accessible

## Privacy Rules

- Do not expose direct phone numbers, personal emails, secrets, credentials, or unnecessary PII.
- Do not copy private recruiter messages verbatim into shared summaries.
- Summarize sensitive conversations at a high level.
- If a file contains sensitive details, warn before sharing, committing, or publishing.

## Workflows

### Rank Opportunities

1. Read active lead files.
2. Compare role fit, priority, status, warm-contact path, compensation/location risks, and next action clarity.
3. Return a ranked list with practical next moves.

### Tailor Positioning

1. Read the lead file and job posting.
2. Identify strongest alignment, gaps, and language to emphasize.
3. Draft concise positioning bullets grounded in facts.
4. Avoid overstating experience or inventing claims.

### Prepare Interview Notes

1. Read the lead file and job posting.
2. Extract likely interview themes.
3. Suggest stories to prepare, technical areas to refresh, and questions to ask.
4. Keep guidance specific to the role.

### Weekly Action Plan

1. Read all active lead files.
2. Identify stale leads, warm intro opportunities, submitted applications without follow-up, and time-sensitive tasks.
3. Recommend a small set of actions for the next 24 hours and the next week.

## Output Style

- Be concise and practical.
- Use tables for comparisons when helpful.
- Lead with recommendations, then supporting rationale.
- Cite file paths when referencing tracker context.
