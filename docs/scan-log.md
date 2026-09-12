# Scan Log

Dated entries appended by the `scan-targets` workflow after each sweep. Newest at the bottom.

- **Older entries:** `scan-log-archive.md` (create it when rotation first happens)
- **Target list:** [`../targets.md`](../targets.md)

## Rules

**This file is history, not status.** Anything that describes the *current* state of a target
(streak counts, last roster size, verification status) belongs in that target's `Last scan` line in
`targets.md`, which is overwritten every run. Never restate it here.

**Write only what changed since the previous entry.** Do not re-narrate prior runs. Phrases like
"ninth consecutive run", "identical to every scan since 07-27", or "118 jobs vs 119 on 09-07" are
status, not history — they belong in `targets.md` and they are what makes entries grow without
bound.

**Size discipline.** No bullet longer than roughly 300 characters or 2 sentences. Aim for an entry
under 80 lines. If an entry runs long, cut narrative, never the roles table.

**Rotation.** When this file passes ~12 entries, move the oldest into `scan-log-archive.md`
(append there, preserving order) as part of the run.

**Reading.** A scan run needs only the most recent 1-2 entries to diff for new roles. Do not read
the whole file, and do not read the archive unless asked about scan history.

## Entry format

```text
### YYYY-MM-DD — Target Scan

**Scanned:** N | **Accessible:** N | **Blocked:** N

| Company | Role | Location | URL | Why it may fit | Action |
|---|---|---|---|---|---|

**Blocked:** company — reason (one line each)

**Changes since last scan:** up to 3 bullets. Only deltas: roles that appeared or disappeared,
access that changed. Omit this section entirely when nothing changed.

**Fetch diagnostics:** what was unreadable and why, URL shapes that did or did not work,
pagination and parameter behaviour, bot-walls, and what a future run should do differently.
```

**This section is the only per-run home for technical detail.** It is deliberately kept out of the
HTML report, which is written for the job seeker and carries only a plain-language coverage note.
Anything that will still be true next run also goes in that org's `Notes` in `targets.md`; keeping
it here as well is what makes a trend visible, such as a portal degrading across three runs.

---
