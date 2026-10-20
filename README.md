# TDL

A day planner where **planned** time and **actual** time sit side by side against your calendar, so you can see where the day went without being scored on it.

Built because a Google Sheet with conditional formatting was doing four jobs at once and only one of them was calendar-shaped.

## What it does

**Three lanes, one day.** Calendar on the left (fixed commitments), Planned in the middle (what you intended), Actual on the right (what happened). Toggle to a single merged lane when you want the whole day in one place, or pick a date range to get one lane per day.

**Reconciliation, not streaks.** Once a planned block's time has passed, a faded copy appears in the Actual lane with ✓ and ✕. Confirm it, drag it to when it really happened, or mark that it didn't. Nothing nags you before the fact.

**Drift, shown plainly.** When planned and actual differ, the block shows `1h15 → 45m`. No percentages, no completion rate, no streak counter. Toggle it off with the stopwatch.

**Time decides what a block is.** Drag out a block before the now-line and it's a log of what you did. Drag one after it and it's a plan. Same gesture either way.

## Interactions

| Action | How |
| --- | --- |
| Create a block | Drag on empty space; type a name; Enter or click away to save |
| Discard a new block | Escape, or leave the name empty |
| Move / resize | Drag the block, or its top or bottom edge (15-minute snap) |
| Mark done | The circle on a planned block |
| Confirm what happened | ✓ / ✕ on the faded block in Actual |
| Change date or range | The date pill — drag across days in the month grid |
| Jump to today | `t` |
| Step the range | `Cmd`/`Alt` + `←` / `→` |

## Running it

Static page, no build step, no dependencies beyond Google Fonts.

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploying

Vercel serves this as a static site with no framework and no build command. `vercel.json` sets clean URLs and keeps `index.html` uncached so updates land immediately.

If a deploy fails, check the project settings in Vercel: Framework Preset should be **Other**, and Build Command, Output Directory, and Install Command should all be empty or overridden to blank. A preset that expects a `package.json` will fail on a repo that doesn't have one.

## Data

Everything lives in `localStorage` under `tdl.v1`, so it is per-browser and per-device. Clearing site data resets it. The shape is the one a real backend should use:

```js
{
  id, t,            // id, title
  p,                // palette index
  day,              // "YYYY-MM-DD"
  ps, pd,           // planned start (minutes from midnight), planned duration
  as, ad,           // actual start, actual duration
  done, skip        // confirmed, or explicitly didn't happen
}
```

## Not built yet

- Google Calendar read (the Calendar lane currently shows seeded events)
- Projects, categories, and task types
- Reminders (push and email)
- The dashboard queue with pinning
- Calibration analytics — estimate vs actual over a term, where time goes by type

## License

MIT
