# Job Search Targets

Use this file to track recurring company career searches. Keep entries factual.

**State vs history.** A target's `Last scan` line below is *status*: overwrite it every run.
Scan history is appended to [`docs/scan-log.md`](docs/scan-log.md) and never restated here.
Keeping the two apart is what stops the log growing without bound.

## Target Companies

### Example Company

- Careers URL: https://example.com/careers
- Filter intent: Remote, New York City, or preferred region.
- Target themes: partner, solutions, applied AI, cloud, security, program management, customer engineering.
- Last scan: not scanned yet.
- Fetch mechanics: (optional) standing facts about how this board must be fetched — size limits, provenance quirks, or a browser requirement where query parameters are applied client-side. Survives the Last scan overwrite.
- Notes: Replace this example with a real target company.

The `Last scan` line is **overwritten** by each scan and holds everything cumulative about this
target, so the scan log never has to restate it. Format it as a single line, for example:

`- Last scan: 2026-09-10 · accessible · 586 postings · 0 new · verified 4 runs running`

## Scan Log

Scan history lives in [`docs/scan-log.md`](docs/scan-log.md), not in this file, so that reading the
target list stays cheap. `scan-targets` appends there; nothing is appended here.

See that file for the entry format and the rules that keep entries from growing run over run.
