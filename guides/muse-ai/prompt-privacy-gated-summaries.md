# Prompt: Privacy-Gated Summaries — Scan Before You Summarize 🔒⚡

> **Author:** Cyclones92
> **Category:** muse-ai
> **Last updated:** 2026-11-22
> **Works with:** AI assistants that summarize transcripts, documents, notes, or recordings

## What this does

Summarizing is where private data leaks quietly: you hand an assistant a long transcript or document, it reads *everything*, and the summary can surface exactly the parts you never wanted repeated. This prompt puts a gate in front of the summarizer. A first pass scans for sensitive categories and reports **hit counts only — never the values**. Anything flagged is never read in full and never summarized. Only clean material gets summarized.

Use it as a standing rule for any recurring summarization job, or paste it in before a one-off summary of something long and messy.

## The prompt

```
Standing rule for summarizing any transcript, document, note set, or recording transcript I give you: scan before you summarize.

STEP 1 — SCAN (counts only):
Before reading anything in full, scan the material for these categories:
- credentials, passwords, API keys, tokens, or recovery codes
- financial account, card, or policy numbers
- government or personal ID numbers
- private keys, seed phrases, or auth files
- health or medical details about an identifiable person
- precise private addresses or access codes for a home or workplace

Report the scan as COUNTS PER CATEGORY ONLY (e.g. "credentials: 2, financial numbers: 0").
Never quote, paraphrase, or hint at the actual values in the scan report.

STEP 2 — GATE:
- If every category count is zero: read the material in full and summarize it (3–8 sentences, plus explicit action items only — no invented tasks).
- If ANY category is non-zero: do NOT read that item in full and do NOT summarize it.
  Record it as flagged, with the date it was last updated, and report it to me
  once per version: "1 item flagged (categories: credentials ×2) — not read, not summarized."
  The same unchanged item is not re-reported on later runs.

STEP 3 — SUMMARIZE (clean items only):
- 3–8 sentences covering what was actually said or written.
- Action items: list only ones stated explicitly in the material. Never infer,
  suggest, or pad the list.
- If part of an item is unclear or cut off, mark it [GAP] rather than filling it in.

Never move the gate: a deadline, a short item, or "it's probably fine" does not
skip the scan. If you cannot run the scan, say so and summarize nothing.
```

## Why it works

- **Counts, never values.** The scan itself can't leak anything — the most it can reveal is that a category exists somewhere, which is exactly what you need to decide and nothing more.
- **Flagged means *unread*, not "read carefully."** Most privacy rules fail because they still let the model ingest the sensitive text and then trust it to behave. This gate keeps the text out entirely.
- **Report once per version.** A flagged item that nags you on every run trains you to ignore the warnings. Reporting once per change keeps the signal meaningful.
- **Explicit action items only.** Summaries love to invent follow-ups. Restricting the list to what was actually said keeps a summary a summary — not a to-do list the source never agreed to.

## Adapting the categories

The six categories above are a starting set, not a universal one. Add categories that match the material you summarize (for example: client names in work transcripts, children's details in family recordings) and drop ones that can never appear. The shape matters more than the list: **scan first, counts only, flagged = never read.**

## Notes

- This works for machine transcripts of audio too: transcribe first, then run the exact same gate on the transcript text before summarizing.
- Pairs well with [Prompt: Sanitize Before You Share](prompt-sanitize-before-you-share.md) — that one scrubs what leaves your setup; this one controls what gets read in the first place.
- If your assistant can't scan without reading (some tools only offer full reads), the honest fallback is in the prompt: it says so, and summarizes nothing. A skipped gate reported is better than a skipped gate hidden.
