# Prompt: Sanitize Before You Share 🧼🔐

> **Author:** Cyclones92
> **Category:** muse-ai
> **Last updated:** 2026-11-18
> **Works with:** Any AI assistant

## What this does

Guides, screenshots, configs, and notes are full of things that should never go public: real names, email addresses, IP addresses, hostnames, tokens, and little personal details you don't even notice anymore. This prompt makes your AI scrub a document *before* you publish it — and show you everything it changed, so nothing slips through and nothing important gets silently eaten.

## The prompt

Paste your document after this prompt (or point the AI at the file):

```
Sanitize this document for public sharing. It will be posted publicly, so assume anyone can read it.

Replace, everywhere they appear:
- Real personal names (mine and anyone else's) -> Cyclones92 for the author, and generic roles for others (e.g. "a family member", "a coworker")
- Real email addresses -> user@example.com
- Public IP addresses -> 192.0.2.x (keep the last octet pattern if it helps the example make sense, e.g. 192.0.2.10)
- Private/LAN IPs -> 192.168.0.x style examples only if the guide is about a home network, otherwise 192.0.2.x
- Real domains and hostnames -> example.com and server1.example.com
- Usernames and account names -> Cyclones92
- API keys, tokens, passwords, and secrets -> <API_KEY>, <TOKEN>, <PASSWORD> placeholders — never shorten, mask, or partially show a real one
- Real street addresses, phone numbers, and locations -> remove them, or replace with a generic example city
- Dates, amounts, schedules, and other personal specifics that identify a real person or household -> generalize them or drop them

Rules:
- Do NOT change the technical meaning. Commands, steps, and explanations must still work with the example values swapped in.
- Do NOT silently delete content. Every change goes in the report below.
- If you are unsure whether something is personal, flag it in the report instead of guessing — I will decide.

After the sanitized document, give me a change report:
1. A table of what you replaced (type of data -> replacement used), without repeating the original secret values — for secrets, say only "API key replaced", never show any part of it
2. Anything you flagged as unsure
3. Anything you removed entirely, and why

Then stop and wait for my approval before treating the sanitized version as final.
```

## Why it works

- **Replacement table, not vibes.** You define the exact example values up front, so the document stays consistent and readable — readers can still follow the guide.
- **Secrets are named, never echoed.** A sanitizer that prints "I replaced key sk-abc123…" has just leaked the key. This prompt forbids that.
- **Unsure = flag, don't guess.** The AI doesn't get to decide what's personal on its own. Borderline items come back to you.
- **Approval gate at the end.** The sanitized copy is a draft until you say it's final.

## Checklist version (no AI needed)

Running through a file by hand? Search it for: `@`, `http` (check every URL), `192.` and any other IP patterns, `key`, `token`, `password`, `secret`, your own name, your username, your city, and any screenshot filenames. Then read it once top to bottom — the sneakiest leaks are in passing mentions, not config blocks.

## Notes

- Sanitize a *copy*. Keep your original private version untouched and clearly named, so you never overwrite your real notes with example values.
- Screenshots need the same treatment: crop or blur names, avatars, addresses, and notification text before uploading.
- Commit messages and file names leak too — keep them plain and neutral.
