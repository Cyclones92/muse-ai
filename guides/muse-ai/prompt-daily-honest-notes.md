# Prompt: Daily Honest Notes — With an Immutability Rule 📓⚡

> **Author:** Cyclones92
> **Category:** muse-ai
> **Last updated:** 2026-11-22
> **Works with:** AI assistants with memory and a place to keep dated daily files

## What this does

Your assistant sees your patterns before you do: what's working, what's quietly slipping, the shortcut you keep taking, the thing you said you'd fix three times. This prompt turns that into a short daily note — honest, specific, positive *and* negative — written to one dated file per day.

The twist that makes it trustworthy: **entries are immutable.** Once a day's note is written, it is never edited. If a later fact proves it wrong, the correction goes in the *next* day's entry. A journal that can be quietly rewritten is just PR; a journal that can't is a record.

Set it as a nightly scheduled task, and give your assistant explicit permission to be honest — most people find they have to say "I won't take offense, it all helps" out loud before the notes get real.

## The prompt

```
Write today's honest daily note about me and save it as one Markdown file
per day: notes/YYYY-MM-DD.md (use today's date).

Cover, briefly and specifically:
- What's working — habits, systems, or decisions that paid off today, with the example.
- What's slipping — things dropped, deferred again, or done worse than usual, with the example.
- One shortfall + fix: pick the most fixable problem you noticed and propose one concrete fix.
- One fun or human observation — something genuinely interesting from today. Not filler praise.

RULES:
- Be honest. Positive and negative both. I am asking for signal, not comfort —
  I can't change what I don't know.
- Specific beats general. "You moved the meeting three times" helps; "time management" does not.
- Base every claim on something that actually happened today. No invented examples,
  no recycled observations from previous days presented as today's.
- Keep it short: a page at most. This is a note, not a report.

IMMUTABILITY RULE (hard):
- Never edit a previous day's file. Ever. Not for typos in facts, not for tone, not on request mid-flow.
- If something in an earlier entry turns out to be wrong, note the correction in TODAY's entry
  ("Correction to Nov 20: ...") and leave the original exactly as written.
- If today's file already exists, stop and report that — do not append to it or overwrite it.
```

## Why it works

- **Immutability is the whole point.** The value of a daily note compounds only if future-you can trust that past entries say what they said. The moment entries get "cleaned up," every entry becomes suspect.
- **Corrections move forward, not backward.** This mirrors how honest records actually work — a ledger isn't erased, it's amended. You keep both the mistake and the fix, which is where the learning lives.
- **Specificity is enforceable.** "With the example" is doing heavy lifting: it forces the note to be grounded in the day, and it makes vague flattery or vague criticism impossible to hide behind.
- **Permission has to be explicit.** Assistants default to diplomacy. Naming "positive and negative both" and "I can't change what I don't know" in the prompt itself is what licenses the note to say the uncomfortable true thing.

## Running it

- **Cadence:** nightly, after the day is mostly done — late evening catches the whole day without competing with it.
- **Layout that stays readable:** one file per day, grouped by year/month if you keep them long-term. Newest period expanded, individual days collapsed, is a comfortable default for a browsing page.
- **Read it on a delay if that helps.** Some people read each note next morning; some batch a week on Sunday. Either works — the writing is what matters, and it happens daily regardless.
- **Don't mirror it into task systems.** This is reflection, not a to-do list. If a fix from a note deserves action, create the task separately and deliberately.

## Notes

- The first few entries will be gentle. That's the assistant calibrating, not the prompt failing — after a week of you *not* punishing honesty, the notes sharpen.
- If a note is wrong about a fact, that's data too: it shows you what your setup looks like from the outside with the information it actually has.
- Pairs well with [Prompt: The Weekly System Audit](prompt-weekly-system-audit.md) — the audit checks your *systems*; these notes check *you*.
