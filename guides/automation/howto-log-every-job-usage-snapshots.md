# How to Log Every Job — Before/After Usage Snapshots for All Automations 📊⚡

> **Author:** Cyclones92
> **Category:** automation
> **Last updated:** 2026-11-22
> **Works with:** Scheduled jobs / cron tasks, dashboard or Space refreshes, reminders, and ad-hoc assistant work — anything with a measurable usage or quota meter

## What this does

Automations burn quietly. A dozen scheduled jobs, a few dashboard refreshes, and a stream of small ad-hoc tasks can eat a surprising share of a weekly allowance — and when the meter runs out, nobody can say which job did it. This guide wraps **every** task in a before/after usage snapshot: each run records the meter reading when it starts and when it ends, under one shared run ID, in one log. No exceptions by task type.

The honest caveat up front: if your meter only reports whole percentages, most small tasks will legitimately show a **0% delta**. That's a real result, not a failure — the log still proves the run happened, when, and what surrounded it. Never invent a finer-grained number than your meter actually gives you.

## Prerequisites

- Some way to check your current usage/quota from the command line or an assistant action (examples use a placeholder `usage-status` command — substitute your own)
- A single append-only log file or table every job can write to (example: `usage-log.jsonl`)
- A job name/slug for every task — ad-hoc work gets one too (example pattern: `adhoc-<short-slug>`)

## Steps

### 1. Define the snapshot shape

Every entry, start or end, carries the same fields:

```json
{"ts": "2026-11-22T12:00:00Z", "job": "example-job", "phase": "start", "run_id": "20261122-120000-example-job", "weekly_pct": 42, "additional_pct": 5, "additional_left": "some tokens left", "reset": "example reset text"}
```

The `run_id` is minted at start and reused at end — that pairing is what makes two readings one run instead of two unrelated numbers.

### 2. Wrap scheduled jobs in their saved body

Bake the logging into the job definition itself, as the first and last steps, so no run can skip it:

```
Step 0: run `log_usage.sh <job-slug> start` and note the RUN_ID it prints.
... the job's actual work ...
Final step: run `log_usage.sh <job-slug> end <RUN_ID>`.
```

A minimal helper script:

```bash
#!/usr/bin/env bash
# log_usage.sh <job-slug> <start|end> [run_id]
JOB="$1"; PHASE="$2"; RUN_ID="${3:-$(date +%Y%m%d-%H%M%S)-$JOB}"
READING="$(usage-status --json)"   # placeholder — your meter check here
# append one JSON line built from $READING + $JOB/$PHASE/$RUN_ID to usage-log.jsonl
echo "RUN_ID=$RUN_ID"
```

### 3. Handle refresh-style jobs that never run a body

Some scheduled refreshes (a dashboard that refreshes itself, a data import action) have no instruction body that executes — logging written *inside* them is dead code and will never run. Convert those to a small **agent wrapper job** on the same schedule:

1. Log start.
2. Invoke the same refresh action with the same arguments.
3. Log end with the same run ID.
4. Stay silent on success; report only failures.

The refresh behaves identically — the wrapper just makes it visible to the log.

### 4. Log ad-hoc work too

One-off chat tasks, subagent runs, and dashboard builds are usually the biggest blind spot. Give each a slug (`adhoc-<short-slug>`), log start before the work and end after, using the same shape. If it's worth doing, it's worth two log lines.

### 5. The rule that keeps it honest

- **Logging never blocks the work.** If the meter check or the log write fails, do the job anyway and note the gap in the run's record.
- **Record the delta you measured, including 0%.** A week of honest zeros around one 3% jump tells you more than a spreadsheet of invented per-task token counts.
- **A new job without logging is incomplete.** Add the start/end steps at creation time, not in a cleanup pass you'll never schedule.

## Verify it worked

Run any one job manually, then check the log:

```bash
grep "<job-slug>" usage-log.jsonl | tail -2
```

Expected: exactly two lines — a `start` and an `end` — sharing one `run_id`, with readings from before and after the run. Then create a brand-new throwaway job *with* the wrapper baked in and confirm its first scheduled run also lands as a pair.

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Start logged, no end | The job died mid-run or its final step was skipped — check that run for a real failure, and make the end step unconditional (runs even when the work errors) |
| End logged with a different run ID | The job minted a new ID instead of reusing the start ID — pass the start ID explicitly as an argument |
| Refresh jobs never appear in the log | They're body-less refresh actions — see Step 3; they need the agent-wrapper conversion |
| Every delta is 0% | Probably correct, if your meter reports whole percentages. Judge the system by pairing and coverage, not by invented precision |

## Notes

- Keep the log append-only and boring: one line per event, no edits. Corrections are new lines, not rewrites.
- Review the log weekly (it pairs naturally with a [Weekly System Audit](../muse-ai/prompt-weekly-system-audit.md)) — look for jobs whose runs pair badly, jobs that run far more often than you remembered, and whole categories of work with no coverage.
- All commands, job names, and readings in this guide are examples or placeholders — substitute your own meter and scheduler.
