---
name: job-tracker-advanced
description: >
  This skill should be used for advanced job-search workflows that
  go beyond a simple scan or status report. Trigger phrases include
  "rank my leads", "compare these roles", "help me prioritize",
  "tailor my resume for this role", "draft outreach", "draft a
  follow-up message", "prep me for the interview at ...", "interview
  talking points", "weekly action plan", "what should I focus on this
  week", or "turn my scan into an application plan". It performs
  ranking, positioning, outreach drafting, interview prep, and
  weekly planning grounded in the current job-tracker workspace.
metadata:
  version: "0.1.0"
---

Run advanced job-search workflows that require branching, prioritization, or multi-step decision support beyond a simple recurring action.

For simple recurring tasks, prefer the `scan-targets`, `add-lead`, and `job-status-report` skills.

## Sources To Read

Before making recommendations, read the relevant files in the tracker workspace:

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

### Draft Outreach Or Follow-Up

1. Read the relevant lead file for context (status, recent updates, contacts).
2. Draft a short, factual message matched to the lead's stage (cold outreach, warm intro request, post-application follow-up, post-interview thank-you).
3. Keep tone professional and specific to the role and contact.
4. Do not include phone numbers, personal emails, or sensitive recruiter content in the draft.

### Prepare Interview Notes

1. Read the lead file and job posting.
2. Extract likely interview themes.
3. Suggest stories to prepare, technical areas to refresh, and questions to ask.
4. Keep guidance specific to the role.

### Weekly Action Plan

1. Read all active lead files.
2. Identify stale leads, warm intro opportunities, submitted applications without follow-up, and time-sensitive tasks.
3. Recommend a small set of actions for the next 24 hours and the next week.

### Scan-To-Plan

1. Use the most recent `## Scan Log` entry in `targets.md` (or run `scan-targets` first if none is fresh).
2. Convert likely-fit roles into a prioritized application plan with target dates and warm-intro paths where known.

## Output Style

- Be concise and practical.
- Use tables for comparisons when helpful.
- Lead with recommendations, then supporting rationale.
- Cite file paths when referencing tracker context.
