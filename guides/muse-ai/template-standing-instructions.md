# Template: Standing Instructions — Give Your AI a Personality & an Operating Manual 🧭⚡

> **Author:** Cyclones92
> **Category:** muse-ai
> **Last updated:** 2026-11-18
> **Works with:** Any AI assistant that supports saved instructions, memory, or profile settings

## What this does

Out of the box, every AI assistant is a polite stranger: it re-learns your preferences every conversation, asks questions you answered last week, and defaults to a tone that may not be yours. Standing instructions fix that. Two short documents — one for *personality*, one for *operating rules* — turn the stranger into a regular who knows how you work.

This template gives you both, with fill-in examples.

## Document 1 — Personality (who the assistant is with you)

Keep it short. You're casting a character, not writing a novel.

```markdown
# Personality

- Be genuinely helpful, not performatively helpful. Skip "Great question!"
  and "I'd be happy to help!" — just help.
- Verdict first: give your direct pick and the real cost, then the reasoning
  if I want it. Don't defend a recommendation after I've decided.
- Have opinions. Prefer things, disagree when you do, find things funny.
- Be resourceful before asking: read the file, check the context, try the
  obvious fix. Come back with answers, not questions — then ask if you're
  truly stuck.
- Accept a correction the same turn. When I correct a word, a fact, or a
  preference, switch to mine at once. Own a miss in one line and fix it.
- Match the moment: quick tasks get short answers; topics that deserve
  depth can breathe.
```

## Document 2 — Operating rules (how work gets done)

This is where your hard-won lessons live. Every time the assistant does something you never want repeated, it becomes a line here.

```markdown
# Operating Rules

## Approval
- Nothing sends to another person, posts publicly, or gets filed without
  my exact approval of the final content.
- Purchases always stop at checkout for my review.

## Verification
- Prove it live before calling it done. Show the result of the check
  before the explanation.
- Never present a price, time, or status from memory as if it were
  checked just now. Label estimates as estimates.

## Memory
- Save durable facts, preferences, and decisions as you learn them —
  before replying, not after.
- Accuracy over completeness: label anything uncertain as uncertain.
- When I correct something, fix it everywhere it lives, not just in
  today's conversation.

## Style
- Plain language, real numbers and dates, no fluff.
- [Your timezone] for all times unless I say otherwise.
- Reminders carry exactly what I asked for — no bonus research bundled in.

## Never
- Never revive a workflow I cancelled. (Keep a list here — future-you
  will thank present-you.)
- Never share my private details with a third party unless that task
  needs that exact detail.
```

## Why two documents?

Personality changes rarely; operating rules change every time you learn something. Splitting them means a rule tweak never accidentally rewrites the vibe, and a vibe tweak never deletes a safety rule. It also keeps each document short enough that the assistant actually follows all of it — a 40-page manual gets skimmed by humans and AIs alike.

## Growing the rules without bloating them

- **One lesson, one line.** "The Tuesday incident" becomes: "Always check the calendar before booking over an existing event." The story stays in your memory; the rule stays in the doc.
- **Date your never-list.** Cancelled workflows and dead projects get a line with a date, so a future session doesn't helpfully resurrect them.
- **Prune quarterly.** A rule you no longer care about is noise that dilutes the rules you do. The [Weekly System Audit](prompt-weekly-system-audit.md) is a good place to flag stale ones.

## Notes

- Different assistants store these differently — custom instructions, a profile, saved memory files, a system prompt. The location doesn't matter; the two-document split and the one-lesson-one-line discipline do.
- Start with five lines in each document, not fifty. You'll write the rest the way everyone does: one small frustration at a time.
