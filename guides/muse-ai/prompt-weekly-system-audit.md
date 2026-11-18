# Prompt: The Weekly System Audit — Your AI Setup's Police Job 🛡️⚡

> **Author:** Cyclones92
> **Category:** muse-ai
> **Last updated:** 2026-11-18
> **Works with:** AI assistants with memory, scheduled jobs, and connected accounts

## What this does

An AI setup grows barnacles: jobs that quietly stopped working, permissions granted once and forgotten, backups that haven't actually run, instructions that contradict each other. This prompt runs a weekly audit that catches all of it — report-first, with fixes split into "done safely" and "needs your OK," and open items that carry over until they're closed.

Set it as a weekly scheduled task, or just paste it in whenever things feel off.

## The prompt

```
Run my weekly system audit. Check everything, report first, and fix only what is safe.

AUDIT THESE AREAS:
1. Scheduled work — every recurring job, reminder, and automation: is it enabled when it should be, did the last runs succeed, is anything stuck, failing silently, or reporting success without delivering?
2. Backups — did each backup actually run, when was the last verified copy, and does the backup cover everything it claims to (files, settings, memory, creations)?
3. Permissions & access — what accounts and services are connected, what can act without asking me, and has anything gained access since last week? List durable grants separately.
4. Security — any risky settings, overly broad sharing, public links that should not be public, or open findings from previous audits still unresolved?
5. Data flows — what information leaves my setup (syncs, uploads, shares) and what stays local? Flag anything flowing somewhere I did not intend.
6. Memory & knowledge — by CATEGORY ONLY (never quote secret values): what kinds of sensitive information does your memory hold, and what would be risky if it were exposed?
7. Health of the setup itself — storage, failing services, expired connections, anything degrading quietly.

RULES:
- Give the whole audit one verdict at the top: Healthy / Needs attention / Action required.
- Safe, reversible fixes: do them during the audit and list them under "Fixed."
- Risky, costly, or permission-changing fixes: do NOT do them. List them under "Needs your OK" with the exact change you propose.
- Anything left open carries over to next week's audit until it is closed. Never drop an open item silently.
- Report only what you actually checked. Anything you could not check goes under "Not verified" — never present an unchecked area as clean.
- No scans, sends, or pushes beyond this audit unless I ask for them this week.
```

## Why it works

- **One verdict, on top.** You learn the state of your whole setup in one line; the detail is there when you want it.
- **"Fixed" vs. "Needs your OK."** The audit is useful the day it runs — safe fixes just happen — but it can never quietly change permissions, spend money, or delete things.
- **Carry-over is the memory.** A finding that disappears next week because nobody fixed it is how small risks become big ones. Carrying items forward makes ignoring them a visible choice.
- **"Not verified" is its own section.** An audit that only reports what it checked, and admits the rest, is worth ten that declare everything green.

## Running it

- **Cadence:** weekly is the sweet spot — long enough for drift to happen, short enough to catch it cheap.
- **Keep the reports.** One file per week, named by date, verdict in the title line. A folder of these becomes the history of your setup's health — and proof of what was known, when.
- **First run will be the longest.** Expect a backlog of small findings. That's the audit paying for itself on day one.

## Notes

- Scale the checklist to your setup: no scheduled jobs? Drop section 1. The shape — verdict, fixed, needs-OK, carry-over, not-verified — is what matters.
- Pairs well with [Sanitize Before You Share](prompt-sanitize-before-you-share.md) when the audit turns up anything public that shouldn't be.
