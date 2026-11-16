# How to Build Wonton Work — Your Own Dumpling Bot Crew 🥟

> **Author:** Cyclones92
> **Category:** muse-ai
> **Last updated:** 2026-11-16

## What this is

**Wonton Work** is a Muse Space that runs a whole crew of tiny bot jobs — each one is a **dumpling**. 🥟

One dumpling, one job. An inbox cleaner. A morning brief. A bill watcher. A ghostwriter. Instead of one giant assistant prompt trying to do everything, you steam up a tray of little specialists, each with its own instructions, its own memory, and its own skills — and you run whichever one you need, whenever you need it.

```
🥟 Wonton Work
├── 🧩 Skill library        ← shared know-how, written once, used by everyone
├── 🥟 Dumpling #1          ← Instructions / Memory / Skills
├── 🥟 Dumpling #2          ← Instructions / Memory / Skills
└── 🥟 Dumpling #3 …        ← add as many as you can eat
```

## Anatomy of a dumpling

Every dumpling has a name, a face (pick a head/color so you can spot it in the tray at a glance), and exactly **three sections**:

### 1. Instructions 📜
What this dumpling does, step by step. Short, exact, bossy. This is the recipe — if it isn't written here, the dumpling doesn't do it.

> Example: *"Search the inbox for promo mail from the last 24 hours. Group what you find by sender. Report back as one numbered list. Do not delete anything — wait for my reply."*

### 2. Memory 🧠
The standing facts this dumpling should never forget — your rules, your exceptions, your preferences. Memory is per-dumpling: what the inbox dumpling knows, the ghostwriter doesn't need to.

> Example: *"Mail from my favorite people is never junk — always flag it important. Example address: `user@example.com`."*

### 3. Skills 🧩
Reusable know-how picked from the **shared Skill library** (below). A dumpling doesn't carry its own copy — it just picks the skills it needs, and the library text rides along on every run.

> Example picks: `Email search` · `Calendar read` · `Web search` · `One numbered list report format`

## The Skill library — write once, steam everywhere 🧩

The library lives on the Space's home page and is **shared by every dumpling**:

- Write a skill once — how to search email properly, how you like reports formatted, how a book gets written — and every dumpling that picks it gets smarter instantly.
- Edit a skill in the library and the edit applies to **all** dumplings using it. No copy-paste drift, no hunting through 20 jobs to fix the same paragraph.
- Keep the library **collapsed by default** on the home page. You rarely touch it, and the dumplings are the main course — don't scroll past the pantry to reach the tray.

Starter library that covers most crews:

| Skill | What it teaches |
|-------|-----------------|
| Email search | How to find mail by sender, date, and keyword |
| Calendar read | How to check what's on today / tomorrow |
| Web search | How to look things up and cite what came back |
| One numbered list report | The house report format (see Runs, below) |
| Ghostwriting | Interview-first writing, in the author's voice |

## Draft → Deploy — the golden rule 🚀

Dumplings are edited as **drafts**. Runs never see a draft.

- **Edit freely** — Instructions, Memory, and Skills picks are all just a draft until you say so.
- **Deploy** publishes all three sections together as **one version** (`v1`, `v2`, …). One snapshot, no half-updated dumplings.
- **Runs only ever use the deployed version.** If a run looks wrong, check what's *deployed*, not what you were just typing.

This one rule prevents 90% of "why did it do THAT?" moments.

## Running a dumpling 🏃

1. Pick a dumpling, hit **Run**.
2. It does its job fresh — Instructions + Memory + picked Skills loaded in, nothing stale from last time.
3. For list-type jobs (inbox, bills, coupons), the report comes back as **ONE numbered list** with checkboxes and a reply box:

```
All items found
1. ☐ Promo — Example Store — 3 emails
2. ☐ Promo — Example Airline — 1 email
3. ☐ Bill — Example Power Co — due Friday

Reply with the numbers, e.g. "delete 1, keep 2"
```

4. **Nothing happens without your say-so.** You reply with the numbers, *then* it acts. Reports propose; you dispose.

## An example crew 🌟

Steal these, rename them, make them yours:

| Dumpling | Job |
|----------|-----|
| Inbox Cleaner | Finds promo clutter, groups by sender, one numbered list |
| Spam Sweeper | Sweeps the junk folder for anything that isn't junk |
| Morning Brief | Calendar + weather + what's due, in five lines |
| Bill Watch | Spots bills and due dates before they spot you |
| Coupon Hunter | Tracks coupons and expiry dates |
| Ghost Writer | Interviews you, then writes in your voice — every chapter approved by you first |

## House rules that make it work ⚡

- **One job per dumpling.** Two jobs in one dumpling is just a confused dumpling.
- **Instructions short and exact.** A paragraph that says precisely what to do beats three pages of vibes.
- **Facts go in Memory, know-how goes in Skills.** "Never delete mail from X" is Memory. "Here's how to search mail" is a Skill.
- **Approve before action.** Dumplings draft, list, and propose. Sending, deleting, and filing wait for a human yes.
- **Deploy is a decision.** If it isn't deployed, it doesn't exist.

## Prompt E — paste this to your Muse and build your own

```
Build me a fullstack Space called "Wonton Work" — a home for a crew of small bot jobs, each one called a dumpling.

Each dumpling has: a name, a fun head/color so I can spot it, and three sections — Instructions (what it does, step by step), Memory (standing facts and my rules for that job only), and Skills (a picker choosing from a shared Skill library that lives on the Space's home page, collapsed by default).

Editing is draft-based: I edit Instructions, Memory, and Skills picks as a draft, and nothing changes for runs until I hit Deploy, which publishes all three sections together as one version (v1, v2, ...). Runs only ever use the deployed version.

Add a shared Skill library on the home page where I can create and edit skills once, and every dumpling that picks a skill uses the current library text on its runs. Seed it with: Email search, Calendar read, Web search, and One numbered list report format.

Running a dumpling loads its deployed Instructions + Memory + picked Skills and does the job fresh. For list-type jobs, the run report must be ONE numbered list with checkboxes and a reply box, so I can reply with item numbers to approve actions. A dumpling must never send, delete, or file anything without my approval of the exact items first.

Start me with two example dumplings so I can see the shape: an Inbox Cleaner (finds promo mail, groups by sender, reports one numbered list, deletes nothing without my reply) and a Morning Brief (calendar + what's due today, five lines max). All example data must be examples — user@example.com, example.com — never real accounts.
```

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Dumpling ignored my new instructions | You edited the draft but didn't **Deploy** — runs use the deployed version |
| Two dumplings do the same job differently | The know-how lives in both Instructions — move it into a shared **Skill** instead |
| Report came back as three separate lists | Add the `One numbered list report` skill and say "one list only" in the Instructions |
| Dumpling forgot a standing rule | Rules belong in **Memory**, not buried mid-Instructions |
| Home page is all library, no dumplings | Collapse the Skill library by default — dumplings first 🥟 |
