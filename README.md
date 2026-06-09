# Personal HQ

A daily command surface. The job: in ten seconds, show the one thing to do now,
and let you capture and triage without thinking.

Lives in `briefing/`. One HTML file plus a data file, installable as a PWA.

## Architecture

- **The app never reads Gmail, Calendar or Strava itself.** Claude is the
  ingestion engine: say *"refresh my HQ briefing"* and Claude regenerates
  `briefing.json` (contract below). The app fetches it at load and layers
  local edits on top.
- **Local edits always win and always survive.** Every ingested item carries a
  stable `srcId`. Local state stores lane overrides, dismissed and completed
  srcIds, user-created tasks, session ticks/skips and lists. A task you have
  killed stays dead across refreshes.
- **Honest header.** Shows `briefing as of <date>, N days old`; amber past
  2 days, red past 4. No "live data" claims.

## Files

| File | Role |
|---|---|
| `briefing/index.html` | the app (no baked-in data) |
| `briefing/briefing.json` | Claude-generated data: tasks, inbox digest, calendar, training block + rules, Strava actuals, `proposedDay` |
| `briefing/manifest.webmanifest`, `sw.js`, `icon-*.png` | PWA install + offline (shell cache-first, briefing network-first with cache fallback) |

## Features

- **Now / Next / Later / Waiting** lanes. One item max in Now. Waiting shows
  "waiting on [who] since [date]" and stays out of the way.
- **Claude's proposed day**: one Now plus up to three Next from `proposedDay`;
  one tap Accept applies lanes, Tweak leaves everything editable. Hidden when
  missing or stale. Nothing auto-applies.
- **Always-on quick capture**: floating button from any scroll position, or
  press `n`. Lands in Later, gone from your head in four seconds.
- **Training block** read from briefing data: tickable sessions auto-matched to
  Strava run dates, a skip state that is neutral by design ("skipped, no
  drama"), season grid, weekly volume chart.
- **Forgiving streak**: one quiet day between completions does not reset it.
- **Focus mode** with 25-minute timer, undo snackbar, confetti.
- **Export / import** of all local state as JSON.

## Refresh loop

Once a morning, tell Claude: **"refresh my HQ briefing."** Claude reads Gmail,
Calendar and Strava, writes `briefing.json` in the contract shape (see the
current file for a worked example) and proposes the day. Always
Claude-in-the-loop; the app cannot read anything by itself.

## Deploy

Static hosting of the `briefing/` directory (same place as the meal planner).
Serve over HTTPS for the service worker; pin to the phone home screen.
