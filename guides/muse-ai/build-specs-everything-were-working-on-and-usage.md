# Build Specs — Two Muse Spaces

> ⚡ **Steal this build.** Two battle-tested Muse Spaces, fully specced — paste a prompt, let your Muse do the rest.


For: someone who wants to recreate these two Spaces with their own Muse agent.
How to use: paste **Prompt A** into your Muse chat to build the first Space, and **Prompt B** for the second. The full specs underneath each prompt explain exactly how the originals work, so your Muse doesn't have to guess.

> 🛠️ Built from *your* world: both Spaces generate everything from your own Muse data — your goals, your scheduled jobs, your chats, your usage. Numbers in brackets are example-shaped, swap in yours.

---

## 1. Everything We're Working On

**Original:** Name `Everything We're Working On` · slug `everything-we-re-working-on` · **static** web artifact (single self-contained `index.html`, no server, no database, no actions) · placement: Library

### What it is
A one-page snapshot dashboard of *everything you and your Muse are working on together* — active projects, scheduled jobs, decisions waiting on you, your conversations, and what's paused/finished. Content is baked into the page at build time. It is a snapshot, not live data: updating it means your Muse rebuilds/edits the page with fresh counts and lists pulled from your goals, tracked items, cron/scheduled jobs, and chat list.

### Page structure (in order)
1. **Masthead** — small mono "stamp" line with a green live dot + snapshot date, giant headline `Here's what's moving.`, and a short note on the right explaining the page.
2. **Metrics strip — 5 numbers, computed from your own data:**
   - schedules running · workstreams in motion · dates to protect · reminders paused or finished · conversations catalogued
   - *(example snapshot: 10 / 8 / 2 / 12 / 40)*
3. **Dates to protect** — inverted dark panel. Rows of: date (mono, e.g. `OCT 20`), title, small detail line. Only genuinely time-critical dates.
4. **Toolbar** — filter pills: `All · Projects · Scheduled · Needs you · Conversations`, plus a live search box. Search + filters are client-side JS only: they hide non-matching items, hide sections that become empty, and show `Nothing matches that view.` when nothing matches.
5. **Work in progress** (`data-kind="projects"`) — numbered cards `01, 02, 03…`. Each card: title, 2–3 sentence plain-English description of what it is and where it stands, a **status pill**, and a short tag.
   - Status pills: `active` (green), `waiting` (gold), `focus` (accent orange), `done` (green), `ongoing` (cyan), `interrupted` (gold), `not done` (accent).
6. **What runs next** (`data-kind="scheduled"`) — every scheduled/cron job you have, grouped sensibly, each with its name, cadence/time, and what it does. Header note: `All times <your timezone> · verified active`. The count here must match the metrics strip.
7. **Where I need you** (`data-kind="decisions"`) — cards for pending decisions, blockers, and anything waiting on your input. Keep it short — small decisions with outsized leverage.
8. **Conversations** (`data-kind="conversations"`) — a catalogue of your chats, grouped (e.g. Pinned / Active), each item showing title + status. Sub-filter pills: `All statuses · Done · Ongoing · Interrupted`, each with a count. Header shows total chats catalogued + snapshot date.
9. **Past or paused** (`data-kind="all"`) — finished, cancelled, or paused work, so it's accounted for but not cluttering the active sections.

### Design
- Fonts: **Archivo** (headings/body, variable width/weight) + **IBM Plex Mono** (numbers, labels, status, dates) — Google Fonts import.
- Light palette: bg `#f2f0ea`, surface `#fbfaf6`, ink `#151a1e`, muted `#59636a`, line `#c9c7be`, accent `#bd3f1f`, cyan `#117a86`, green `#25623b`, gold `#8b5a00`.
- Dark mode via `prefers-color-scheme` (no toggle): bg `#101416`, surface `#171d20`, ink `#f0f0e9`, accent `#ff7553`, cyan `#58c5d0`, green `#73c68d`, gold `#e9b955`.
- Layout: max width `1220px`, generous whitespace, thin rule lines between sections, big tight-tracked headline (`clamp(38px, 6vw, 76px)`, letter-spacing `-0.055em`). Mobile responsive — metrics and the urgent panel collapse to one column.
- No backend, no forms, no saved state. All interactivity is the filter/search JS in the same file.

### Prompt A — paste this to your Muse
```
Build me a static Space (single-page, no database) called "Everything We're Working On", slug everything-we-re-working-on, in my Library.

First, gather my real current data yourself: my active goals and tracked items, my scheduled/cron jobs, my chats, and anything paused or finished. Do not invent items and do not copy anyone else's projects — every card must come from my actual work with you.

Page, in order: (1) masthead with a snapshot date and the headline "Here's what's moving."; (2) a 5-number metrics strip — schedules running, workstreams in motion, dates to protect, reminders paused/finished, conversations catalogued — computed from the data you gathered; (3) a dark "Dates to protect" panel with date rows; (4) filter pills (All / Projects / Scheduled / Needs you / Conversations) plus a live search box, client-side JS only, hiding empty sections and showing "Nothing matches that view." when empty; (5) "Work in progress" — numbered cards with title, 2–3 sentence status description, a colored status pill (active/waiting/focus/done/ongoing/interrupted) and a short tag; (6) "What runs next" — all my scheduled jobs with cadence and purpose; (7) "Where I need you" — pending decisions/blockers; (8) "Conversations" — my chats grouped with status sub-filters (All/Done/Ongoing/Interrupted with counts); (9) "Past or paused".

Style: Archivo + IBM Plex Mono, warm off-white background #f2f0ea, ink #151a1e, burnt-orange accent #bd3f1f, with a matching prefers-color-scheme dark mode. Max width 1220px. Tell me it's a snapshot and that you'll rebuild it when I ask for a refresh.
```

---

## 2. Usage

**Original:** Name `Usage` · slug `usage` · **fullstack** web artifact (React client + TypeScript server actions + SQLite/Drizzle) · placement: Sidebar · managed cron: daily `09:09 <your timezone>` → action `refreshUsage`

### What it is
A token-usage tracker for your scheduled jobs. Before each job runs, your current Muse usage % is logged; after it runs, it's logged again. The Space pairs the two readings, computes the delta per job, and graphs **what burns the most**.

### The one honest limitation — build this in, don't work around it
Muse only reports usage as a **whole % of your weekly allowance** (via the subscription-status check). There are **no exact per-job token counts**. So most small jobs will read 0% before and 0% after — that means **<1%**, not a logging failure. The UI must say this plainly next to the ranking, and display a 0 delta as `<1%`.

### Data source
- Live check: `subscription-status status` → parse: weekly % used, reset text (e.g. `Jan 20 at 3:04 PM EST`), additional tokens % used, additional tokens left (e.g. `1.0B tokens left`).
- On-disk log: a helper script appends one JSON line per reading to `usage-log.jsonl`. The Space's refresh re-reads that file and imports new lines, deduplicating so re-reading never double-counts.

### Helper script spec — `log_usage.sh`
```
log_usage.sh <job-slug> start [note]        # at the top of a job; prints RUN_ID=...
log_usage.sh <job-slug> end <run-id> [note] # at the bottom of a job
log_usage.sh <job-slug> snapshot [note]     # one-off reading, no pairing
```
- On `start`, generate `run_id = YYYYMMDD-HHMMSS-<job-slug>`.
- Each call runs the subscription-status check and appends one JSON line:
  `{"ts": ISO, "job": "...", "phase": "start|end|snapshot", "run_id": "...", "weekly_pct": number|null, "additional_pct": number|null, "additional_left": "...", "reset": "...", "note": "..."}`

### Wiring into jobs
- Pro move: **wire ALL scheduled jobs** (example: dozens at build time) — every cron body calls the logger at the top (`start`) and bottom (`end` with the run id). Offer your user the choice first: all jobs vs. only the heavy daily jobs.
- Known gap to handle: jobs that run as **Space/artifact actions** never execute a cron body, so their logging has to live **inside the artifact action itself**, not in the cron wrapper.

### Database schema — one table: `readings`
| field | type | notes |
|---|---|---|
| `id` | integer PK, autoincrement | |
| `ts` | timestamp (epoch ms) | instant of the reading; display in the user's home timezone |
| `job` | text | free text — never hard-code a job set into the schema |
| `phase` | text enum: `start` / `end` / `snapshot` | |
| `run_id` | text, default `""` | pairs a start + end |
| `weekly_pct` | integer, nullable | whole % of weekly allowance |
| `additional_pct` | integer, nullable | |
| `additional_left` | text, default `""` | e.g. `1.0B tokens left` |
| `reset_text` | text, default `""` | |
| `note` | text, default `""` | |
| `source` | text, default `manual` | `manual` / `refresh` / seed |
| `created_at` | timestamp | |

### Server actions (8)
1. `getDashboard({limit})` — returns: `current` (latest reading), `readings` (newest-first), `ranking`, `openRuns`, `stats`.
   - **Ranking:** pair start/end by `run_id`, group by job → `totalDelta, avgDelta, maxDelta, lastDelta, runs, lastRunAt`. Sort by totalDelta descending, then run count.
   - **Open runs:** a `start` with no matching `end`.
   - **Stats:** `totalReadings, totalRuns (paired), jobsTracked, subOneRuns (delta = 0)`.
2. `recordReading(...)` — one reading; exact duplicates on `(ts, job, phase, run_id)` are ignored and reported as deduped.
3. `startRun({job, weeklyPct, note})` — logs the before-reading, returns the `runId`.
4. `finishRun({runId, weeklyPct})` — logs the after-reading, returns the measured delta + a message.
5. `deleteReading({id})` — for correcting a bad entry.
6. `refreshUsage({})` — starts a background refresh: an agent task runs the live subscription-status check, re-reads `usage-log.jsonl`, and saves new readings via `saveRefreshReadings`.
7. `saveRefreshReadings(...)` — callback for the refresh task; stores + dedupes on `(ts, job, phase, run_id)`.
8. `importSeedReadings({})` — one-time seed from the on-disk log, **only when the readings table is completely empty**. Never reseed over real data.

### UI (single column, max-w-3xl, mobile-first)
1. **Hero — current weekly allowance:** label `Free weekly limit used`, giant mono % (text-7xl), `as of <time> ET`, a progress bar at that %, reset text, `Additional tokens X% used (Y left)`, a **↻ Refresh** button, and a stats line: `N readings · N paired runs · N jobs tracked · N runs under 1%`.
2. **What burns the most** — the honest-limitation paragraph (above), then a **vertical bar chart** (Recharts) of ranking by total Δ with % labels, plus a list under it per job: runs · total · avg · biggest · last run date. Empty state explains how to create the first paired run.
3. **Weekly % over time** — step-after **line chart**, 0–100% Y axis, readings oldest → newest. Needs ≥2 readings to draw.
4. **Before / after a job** — Start-run form (job with autocomplete suggestions from known + previously logged jobs, weekly % now, optional note, `▶ Start run (log before)`), then a card per open run with a weekly-%-after input and `■ Finish run` button.
5. **Log a reading** — manual form: job, phase (snapshot/start/end), run id (only shown for start/end), weekly %, additional %, additional left, resets, note.
6. **The log** — newest-first list. Each row: job, big % (with `Δ <1%`/`Δ N%` in accent on end readings), timestamp in home timezone, phase (start = teal, end = accent), additional %, reset text, note, and a delete link.

### Design
- Fonts: **IBM Plex Sans** + **IBM Plex Mono**. Tailwind.
- Light: bg `#f4f2ec`, surface `#ffffff`, text `#1c2b33`, dim `#5d6d77`, border `#ddd8cc`, accent amber `#d97706`, teal `#0f766e`.
- Dark (`prefers-color-scheme`): bg `#10161b`, surface `#1a232b`, text `#ece7db`, dim `#93a3ad`, border `#2e3a43`, accent `#f59e0b`, teal `#2dd4bf`.
- Charts: Recharts — vertical BarChart for ranking, LineChart (stepAfter) for timeline, colors from the CSS variables above.

### Refresh / automation
- Managed cron on the Space itself: **daily ~09:09 in the user's timezone** → `refreshUsage`.
- Manual Refresh button does the same on demand.
- Start empty (or seed only from *your own* on-disk log if you already have one). Do not import anyone else's readings.

### Prompt B — paste this to your Muse
```
Build me a fullstack Space called "Usage", slug usage, in my sidebar, with a daily refresh at about 9:09 AM my timezone.

Purpose: log my Muse usage % before and after each of my scheduled jobs, pair the readings, and graph which jobs burn the most.

First, tell me this limitation and build around it honestly: Muse only reports usage as a whole % of my weekly allowance via the subscription-status check — there are no exact per-job token counts, so a job that moves less than 1% must display as "<1%", not 0% and not an error. Put that explanation in the UI next to the ranking.

Build:
1. A helper script log_usage.sh <job> start|end|snapshot that runs the subscription-status check, parses weekly %, reset text, and additional-tokens %/left, and appends one JSON line {ts, job, phase, run_id, weekly_pct, additional_pct, additional_left, reset, note} to usage-log.jsonl. On start it generates run_id YYYYMMDD-HHMMSS-<job> and prints RUN_ID=.
2. Ask me whether to wire the logger into ALL my scheduled jobs or only the heavy dailies, then wire the ones I pick: start at the top of each job, end at the bottom. If a job runs as a Space action, put its logging inside the action instead.
3. One SQLite table "readings": id, ts (epoch ms), job (free text), phase (start/end/snapshot), run_id, weekly_pct, additional_pct, additional_left, reset_text, note, source, created_at.
4. Actions: getDashboard (latest reading + newest-first readings + per-job ranking from paired runs with total/avg/max/last delta + open runs + stats), recordReading (dedupe on ts+job+phase+run_id), startRun, finishRun (returns delta), deleteReading, refreshUsage (background: live subscription check + re-read usage-log.jsonl, deduped), saveRefreshReadings, importSeedReadings (only if the table is empty).
5. UI in this order: hero with giant current weekly % + progress bar + reset + additional tokens + Refresh button + stats line; "What burns the most" vertical bar chart + per-job list; "Weekly % over time" step line chart (0–100%); Start/Finish run forms; a manual "Log a reading" form; and "The log", newest first, with delta shown on end readings and a delete option per row.
6. Style: IBM Plex Sans + IBM Plex Mono, warm off-white #f4f2ec, amber accent #d97706, teal #0f766e, with prefers-color-scheme dark mode (#10161b bg, #f59e0b accent). Recharts for both charts. Display all times in my home timezone.
```

---

### Differences at a glance
| | Everything We're Working On | Usage |
|---|---|---|
| Type | Static, single HTML file | Fullstack: React + server actions + SQLite |
| Data | Baked-in snapshot, rebuilt on request | Live database, grows one row per reading |
| Updates | Muse rebuilds the page from goals/crons/chats | Daily cron refresh + logger wired into every job + manual forms |
| Charts | None — metrics strip only | Bar ranking + timeline line chart (Recharts) |
| Sidebar | Library | Sidebar |
