# Build Specs — Two More Muse Spaces

> ⚡ **Steal this build.** Two more Muse Spaces, fully specced — including the two link tricks that took real trial-and-error to crack.


For: someone who wants to recreate these two Spaces with their own Muse agent.
How to use: paste **Prompt C** into your Muse chat to build the first Space, and **Prompt D** for the second. The full specs underneath each prompt explain exactly how the originals work, including the two link tricks that took real trial-and-error to get right.

> 🛠️ Built from *your* world: both Spaces generate everything from your own Muse data — your Spaces, your digest jobs, your channels. Examples are example-shaped, swap in yours.

---

## 3. All My Spaces

**Original:** Name `All My Spaces` · slug `all-my-spaces` · **static** web artifact (single self-contained `index.html`, no server, no database, no actions) · placement: Sidebar

### What it is
A terminal-style launchpad hub for **every Space you have**. One page, every Space as a clickable card, grouped into categories, with live search and category filters — so you never hunt through the sidebar again. Content is baked into the page at build time; adding a Space means editing the page to add a card (see "Keeping it in sync" below).

### ⚠️ THE LINK RULE — the whole point of this Space, get it right the first time
**Every card is a link that opens the target Space in a NEW TAB, using an absolute URL:**

```html
<a class="card"
   href="https://muse.ai/library/artifacts/<target-slug>"
   target="_blank" rel="noopener noreferrer">
  …
</a>
```

- `href` is **always** the absolute form `https://muse.ai/library/artifacts/<slug>` — never a relative path.
- `target="_blank"` on **every** card, with `rel="noopener noreferrer"`. Clicking a card leaves the hub open in its own tab and opens the Space in a new one.
- **Why — this was learned the hard way, after three failed attempts:** Spaces run inside a sandboxed frame. Relative links like `../<slug>/` fail every way they were tried: same-frame navigation silently does nothing, `target="_top"` does nothing, and `target="_blank"` with a relative URL opens `about:blank`. The builder's test rig can falsely show relative links working — the real client does not. The absolute-URL + new-tab pattern is the only one verified working in the real client, so build it that way from the start and don't "fix" it later.
- The same rule applies to **any** cross-Space link in **any** Space you build, not just this hub.

### Page structure (in order)
1. **Terminal bar** — window dots (●●●), a fake shell path like `you@your-agent: ~/spaces — zsh`, and a live counter on the right: a green pulsing dot + `N online` (N = total Spaces).
2. **Hero** — a shell prompt line (`you@your-agent:~/spaces$ ls -1 ./all` + blinking cursor block), giant headline `All My / Spaces_`, a one-paragraph lede ("One launchpad for everything you've built with Muse…"), a stats row (`▸ N SPACES INDEXED · 5 CATEGORIES · PRESS / TO SEARCH`), and a small ASCII-art box with your agent's name.
3. **Controls** — search box styled as a terminal prompt (`>_ grep your spaces…`, with a `/ to focus` hint — pressing `/` anywhere jumps to search) + category filter chips (`./all *` plus one chip per category). A result line underneath: `N spaces found · tap a card to open it · updated <date>`. Search and filters are client-side JS only: they match each card's `data-search` keywords, hide non-matching cards and empty sections, and update the found count live.
4. **Category sections** — one per category, each with: a heading with an icon, a fake path (`~/spaces/command`), a rule line, and a module count (`08 modules`). Cards in a responsive grid.
   - Example categories — use categories that fit *your* Spaces: **⌘ Command Center** (example: 5) · **▣ Knowledge Vault** (example: 3) · **$ Money & Home** (example: 4) · **`</>` Example Lab** (example: 4) · **◇ Ventures & Research** (example: 2) — example: 18 Spaces total.
5. **Each card** contains, in order:
   - a **monogram tile** — 2 letters (e.g. `EH` for Example Hub) on a color-coded background (lime / cyan / amber / pink / violet, rotating by category);
   - a sequential **index number** (`01`–`NN`, continuous across all sections, not restarting per section);
   - the Space's **title** (heading font) + a `→` arrow on the right;
   - a **one-line description** of what that Space does;
   - a slug line: `~/ <slug>`;
   - `data-cat="<category>"` and `data-search="<title, slug, and keyword synonyms>"` attributes so search finds it by more than its exact name (e.g. a trading Space should also match "stocks", "spreads", "options").

### Keeping it in sync — required whenever a new Space is built
Adding a card is never just adding a card. In the same edit:
1. Insert the card in the right category, with the absolute new-tab link above.
2. **Renumber** all following cards so the `01…N` sequence stays clean.
3. Update **every count**: terminal bar (`N online`), hero (`N SPACES INDEXED`), result line (`N spaces found`), and that category's module count.
4. Update the `updated <date>` date.
5. Standing rule for your Muse: **every time it builds you a new Space, it adds it to this hub in the same turn** — don't leave it for later.

### Design
- Fonts: **Chakra Petch** (headlines, card titles, section heads — uppercase, techy) + **JetBrains Mono** (everything else — the whole page is monospace by default).
- Hard-shadow "terminal card" look: cards have a solid ink border and a `4px 4px 0` offset shadow, radius `14px`, and lift/shift on hover.
- Light palette: bg `#eef1e6` → `#e3e8d6`, surface `#ffffff`, ink `#101410`, muted `#5b665b`, accent lime `#365314` on `#d9f99d`, cyan `#0e7490` on `#cffafe`, amber `#92400e` on `#fef3c7`, plus pink `#fce7f3` and violet `#ede9fe` tile backgrounds.
- Dark mode via `prefers-color-scheme`: bg `#070907`, surface `#111511`, ink `#e8f5e0`, muted `#93a58f`, accent `#a3e635`, cyan `#22d3ee`, amber `#fbbf24`.
- No backend, no forms, no saved state. All interactivity is the search/filter JS in the same file.

### Prompt C — paste this to your Muse
```
Build me a static Space (single-page, no database) called "All My Spaces", slug all-my-spaces, in my sidebar. It's a launchpad hub linking to every Space I have.

First, list all my actual Spaces yourself — do not invent any and do not copy anyone else's list. Group them into 4–6 categories that fit what I actually have.

CRITICAL LINK RULE — build this way from the start, do not experiment: every card must be <a href="https://muse.ai/library/artifacts/<slug>" target="_blank" rel="noopener noreferrer">. Absolute URL, new tab, every time. Relative links (../<slug>/) do NOT work inside a Space's sandboxed frame — they silently do nothing or open about:blank, even if a test preview looks fine. Clicking a card must open that Space in a new browser tab and leave the hub open.

Page: a terminal-style bar (window dots, a fake shell path, and "N online" with the total count); a hero with a shell-prompt line, the headline "All My Spaces_", a stats row with the total count, and a search box (pressing / focuses it) plus category filter chips, all client-side JS; then one section per category showing its module count. Each card: a 2-letter monogram tile, a sequential number (01, 02, … continuous across sections), the Space's title with a → arrow, a one-line description, its slug, and data-search keywords including synonyms so search finds it by topic, not just exact name.

Style: terminal/geeky — Chakra Petch for headings, JetBrains Mono for body, warm green-tinted off-white background, solid borders with a 4px offset hard shadow on cards, and a matching prefers-color-scheme dark mode.

Also make this a standing rule: whenever you build me a new Space from now on, add its card to this hub in the same turn — inserted in the right category, all cards renumbered, and every count on the page (online count, indexed count, found count, category module count, updated date) updated to match.
```

---

## 4. Daily Posts

**Original:** Name `Daily Posts` · slug `daily-posts` · **fullstack** web artifact (React client + TypeScript server actions + SQLite/Drizzle + blob storage) · placement: Sidebar · no managed cron of its own — the digest jobs themselves write to it

### What it is
A simple, compact ledger of your daily digest/posting runs — originally three morning Discord digests. One row per run: **date · channel · post count · upload status · note/errors**. And the key feature: **each run's generated HTML file is stored inside the Space itself**, so you can click a date and read that day's actual digest right there. Only ~7 days are kept; older rows (and their files) delete themselves.

Example shape — three channels: `#digest-one` (example digest, ~7:10 AM), `#digest-two` (example digest, 7 AM), `#digest-three` (example digest, 8 AM). Use *your* digest jobs/channels.

### Database schema — one table: `runs`
| field | type | notes |
|---|---|---|
| `id` | integer PK, autoincrement | |
| `run_date` | text, `YYYY-MM-DD` | the digest's local calendar date (user's home timezone) |
| `channel` | text | e.g. `#digest-one` |
| `post_count` | integer, nullable | null on a failed run |
| `status` | text enum: `verified` / `partial` / `failed` | shown as "upload verified" / "posted — partial" / "did not post" |
| `note` | text, nullable | errors, gaps, coverage notes |
| `html_blob_key` | text, nullable | pointer to the stored HTML file — see below |
| `html_filename` | text, nullable | original filename, e.g. `digest-2026-01-16.html` |
| `created_at` | timestamp (epoch ms) | insert instant |

### Server actions (5)
1. `listRuns({})` — runs from the last 7 days, newest first. Each run is presented with `has_html`, `html_url` (from blob storage, see below), and `html_filename` added.
2. `logRun({run_date, channel, post_count, status, note, html_content?, html_filename?})` — logs one run. **Replaces** any existing row for the same date + channel (a re-run overwrites, never duplicates). If `html_content` is passed, the file is stored in the same call. On every insert it **prunes**: deletes rows older than 7 days *and deletes their stored files too*.
3. `attachHtml({id, html_content, html_filename})` — attaches (or replaces) the HTML file on an already-logged run.
4. `deleteRun({id})` — deletes one row and its stored file (for corrections).
5. `seedHistory({})` — optional one-time import of your real recent runs; no-ops if any runs already exist. Never seed with anyone else's history.

### How the runs get logged — wiring
Each digest job, at the end of its run, calls `logRun` itself with its date, channel, post/story count, upload status, a one-line note, **and the HTML file it just generated** (`html_content` + `html_filename`). No separate cron for this Space. A manual "Log a run" form in the UI covers corrections and one-offs.

### ⚠️ HOW THE HTML FILES ARE EMBEDDED INSIDE THE SPACE — the part to copy exactly
There are two halves: getting the file **in**, and making clicking it **work**. The second half is where the naive approach fails.

**Half 1 — storage (files live inside the Space, not as external links):**
- Files are stored in the Space's own **blob storage** (`ctx.blobs`), *not* linked from Discord, a file host, or anywhere external.
- Deterministic key, one file per date + channel: `digests/<run_date>/<channel-slug>.html` (e.g. `digests/2026-01-16/digest-two.html`), content type `text/html`.
- The database row stores **only** the pointer (`html_blob_key` / `html_filename`) — never the HTML in the database.
- `listRuns` resolves the pointer server-side: `html_url = ctx.blobs.getUrl(html_blob_key)` (a relative `./blobs/<key>` URL), and returns `has_html` so the client knows which dates are clickable.
- A run with no file (e.g. a failed run that produced nothing) simply has `has_html = false` until someone attaches one via `attachHtml` or the row's "Attach HTML" control (a hidden file picker in the UI).
- Retention is tied together: when a row is pruned (>7 days) or deleted, its blob is deleted in the same operation.

**Half 2 — viewing (dates are BUTTONS opening an in-page reader, NOT links):**
- **Do not render the date as an `<a href>` to the file.** That was tried twice and failed both times in the real client:
  - `<a target="_blank" href="<blob URL>">` → opens **`about:blank`**. The Space runs in a sandboxed frame, and a top-level navigation to a blob response lands on a blank page (the blob response also deliberately carries CSP `sandbox`/`nosniff` headers — leave those alone).
  - Generating a link with `URL.createObjectURL(...)` / blob-URL anchors → also `about:blank`.
- **The working pattern (live, verified):**
  1. If the run `has_html`, render its date as a **`<button>`** — underlined with a thick accent underline so it clearly reads as tappable. If it has no file, render the date as plain dim text (not clickable at all).
  2. Clicking the button opens a **full-screen in-page reader** (a dialog overlay inside the Space, not a new tab and not a navigation).
  3. The reader **`fetch`es the `html_url`** — a subresource read, which is *not* blocked the way top-level navigation is — and gets the file's HTML as text.
  4. It renders that HTML into a **sandboxed `<iframe srcDoc={html} sandbox="allow-popups">`** — `srcDoc`, not `src`. No script privileges for the digest's HTML; `allow-popups` only, so outbound links *inside* a digest can still open in a real tab.
  5. Reader chrome: a header with `<channel> — <date>` and a **Close ✕** button, **Escape** key also closes, a "Loading the digest…" state, and an error state ("That day's HTML file couldn't load.") with a **Retry** button that re-fetches.
- Footer hint in the UI, shown once any run has a file: *"Tap an underlined date to read that day's digest right here."*

### UI layout
- Single column, max-w-2xl, deliberately simple/compact — it's a ledger, not a dashboard. No charts.
- **Grouped by channel**, fixed group order: your primary channel first, your last channel last, any others in between (example order: `#digest-one` first, `#digest-two` middle, `#digest-three` last). Newest run first inside each group.
- Per channel group:
  - Channel heading.
  - **Latest run** called out first under a `LATEST RUN` micro-label, in a larger ledger line.
  - The rest under a `LAST 7 DAYS` micro-label, as a compact divided list.
- **Ledger line format** (monospace "ledger" font), one line per run:
  `Sun, Jan 15 · #digest-one · 42 posts · upload verified`
  - Date formatted from the `YYYY-MM-DD` with pure calendar math (no timezone drift).
  - Failed runs / null counts show `no posts`.
  - Status is colored: verified = green, partial = amber, failed = red. Labels: `upload verified` / `posted — partial` / `did not post`.
  - The run's note (errors/coverage) prints underneath in small dim text.
  - Per-row controls on the right: **Attach HTML** (only when the run has no file) and a **✕ delete** that turns into an inline `Delete / Keep` confirm.
- **Manual form** (`+ Log a run manually`): date (defaults to today in the user's timezone), channel, post count, upload status dropdown, **HTML file picker (optional, `.html`)**, errors/notes textarea.
- Footer note: *"Rows older than 7 days are deleted automatically."*

### Design
- System monospace ledger font for run lines (`ui-monospace / SF Mono / Menlo / Consolas`), sans for the rest. Tailwind.
- Light: bg `#f7f5f0`, surface `#fffdf8`, text `#1c1a17`, dim `#6f6a5e`, border `#ddd6c9`, accent/ok green `#1e7d46`, warn `#9a6a12`, bad `#b3352b`, radius `10px`.
- Dark (`prefers-color-scheme`): bg `#16140f`, surface `#201d17`, text `#ece7da`, dim `#a39a87`, border `#38332a`, accent/ok `#4caf7d`, warn `#d9a441`, bad `#e06a5e`.

### Prompt D — paste this to your Muse
```
Build me a fullstack Space called "Daily Posts", slug daily-posts, in my sidebar. It's a simple ledger of my daily digest runs, and it stores each run's generated HTML file inside the Space so I can read that day's digest by tapping its date.

Data: one table "runs" — id, run_date (YYYY-MM-DD in my home timezone), channel, post_count (nullable), status (verified/partial/failed), note, html_blob_key, html_filename, created_at.

Actions: listRuns (last 7 days, newest first, each run presented with has_html, html_url resolved from blob storage, and html_filename); logRun (replaces any existing row for the same date+channel, optionally stores an HTML file passed as html_content + html_filename in the same call, and on every insert deletes rows older than 7 days AND their stored files); attachHtml (attach/replace a file on an existing run by id); deleteRun (deletes the row and its file); seedHistory (optional one-time import of my own real recent runs only, no-op if any runs exist).

Wiring: after you build it, wire each of my daily digest jobs to call logRun at the end of its run, passing its date, channel, post count, upload status, a one-line note, and the HTML file it generated. There is no separate refresh cron for this Space.

HOW THE HTML FILES MUST BE STORED: in the Space's own blob storage (ctx.blobs), never as external links. Key: digests/<run_date>/<channel-slug>.html, content type text/html. The row stores only html_blob_key/html_filename.

HOW CLICKING MUST WORK — copy this exactly, do not use a link: rendering the date as an <a href> to the blob URL opens about:blank in the real client (top-level navigation from the sandboxed frame is blocked), and blob-URL anchors fail the same way. Instead: if a run has a file, render its date as an underlined <button>; if not, plain dim text. Clicking opens a full-screen in-page reader dialog: fetch the html_url as text (a subresource fetch works where navigation doesn't), render it into <iframe srcDoc={html} sandbox="allow-popups">, with a header showing channel + date, a Close button, Escape to close, a loading state, and an error state with Retry.

UI: compact, grouped by channel in a fixed order I’ll confirm with you (primary channel first, last channel last), newest first in each group, latest run called out per channel, the rest under "Last 7 days". One monospace ledger line per run: "Sun, Jan 15 · #channel · 42 posts · upload verified" — status colored green/amber/red for verified/partial/failed, note underneath in small dim text, per-row Attach HTML (only when no file) and a delete with inline confirm. Plus a manual "Log a run" form with an optional HTML file picker. Footer: "Rows older than 7 days are deleted automatically" and, once any file exists, "Tap an underlined date to read that day's digest right here."

Style: warm off-white #f7f5f0, green accent #1e7d46, with prefers-color-scheme dark mode (#16140f bg, #4caf7d accent). Keep it simple — no charts, no dashboard.
```

---

### The two link lessons, in one place
| Situation | What fails | What works |
|---|---|---|
| Linking **to another Space** (All My Spaces hub) | Relative `../<slug>/` links — do nothing or open `about:blank` | Absolute `https://muse.ai/library/artifacts/<slug>` + `target="_blank"` — opens in a **new tab** |
| Opening a **stored HTML file inside the same Space** (Daily Posts) | `<a href>` to the blob URL, and blob-URL anchors — both open `about:blank` | Date as a **button** → `fetch` the blob URL → render in an in-page reader via `<iframe srcDoc sandbox="allow-popups">` |
