# Personal Briefing

A self-contained, offline-capable HTML dashboard generated from live personal data
(Google Calendar, Gmail, Strava) via Claude Code MCP connectors.

- **`briefing/index.html`** — the briefing for Tuesday 9 June 2026: week ahead,
  inbox triage, and a Training HQ with 13 weeks of run volume, pace trend, and
  10k-plan progress. No external dependencies — open it in any browser.

To regenerate, ask Claude Code: *"refresh my briefing"* — it pulls fresh data
from the connected accounts and rewrites the embedded data block.
