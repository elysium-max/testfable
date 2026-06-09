# Personal HQ

A self-contained, ADHD-friendly daily HQ generated from live personal data
(Gmail, Google Calendar, Strava) via Claude Code MCP connectors.

**`briefing/index.html`** — open it in any browser, works offline. One file, no dependencies.

## What's inside

- **Now / Next / Later planner** — one task in NOW, max three on deck, everything
  else parked in Later so it's out of sight but not lost. Full-screen **focus mode**
  with a 25-minute timer, confetti on completion, daily streak counter.
- **Today's shape** — calendar events + exercise sessions merged into a timeline
  that knows the weekday (recurring run/gym sessions render on the right days).
- **Inbox digest** — emails distilled into actions with extracted deadlines,
  sorted urgent-first; FYI items demoted below the fold.
- **Training: your plan vs reality** — an editable 11-week plan (weekly km +
  long-run targets) compared week-by-week against actual Strava volume, with
  adherence %, target-vs-actual chart, race-day countdown, and computed insights.
- **Shopping list & brain dump** — quick-capture lists with one-tap ticking.

## Persistence model

- **Live data** (emails, calendar, Strava actuals) is embedded at generation time.
- **Your stuff** (tasks, plan targets, race date, lists, collapsed sections,
  streak) lives in `localStorage` — regenerating the page never overwrites it.

To regenerate with fresh data, ask Claude Code: *"refresh my briefing"*.
