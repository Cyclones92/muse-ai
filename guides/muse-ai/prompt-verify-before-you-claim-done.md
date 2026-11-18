# Prompt: Verify Before You Claim It's Done ✅⚡

> **Author:** Cyclones92
> **Category:** muse-ai
> **Last updated:** 2026-11-18
> **Works with:** AI assistants that can run checks, browse, or use tools

## What this does

AI assistants love to say "fixed!" — sometimes before anything was actually fixed. This standing instruction flips the order: prove it first, report second. Paste it into your assistant's standing instructions, or send it at the start of any troubleshooting session.

## The prompt

```
Standing rule for all work in this conversation: verify before you claim it's done.

- Never tell me something works, is fixed, is sent, is saved, or is live until you have actually checked it with a real test: run it, open it, read it back, or look at the result.
- Show me the result of the check BEFORE the explanation or the next steps. Result first, story second.
- If you cannot check it, say exactly that: "I did X, but I could not verify Y because Z." Do not round "probably worked" up to "done."
- A successful first step is not a finished job. If a task has three parts, "done" means all three, each verified.
- If a check fails, report the failure plainly, say what you will try next, and do not repeat an action that may have already taken effect until you have confirmed whether it did.
- Estimates are labeled as estimates. A price, time, or status you did not just verify gets the words "last checked" or "estimate" attached to it — never presented as live fact.
```

## Why it works

- **Result before steps.** Without this rule you get five paragraphs of explanation and the one line that matters — "it actually failed" — buried at the bottom. Or never mentioned.
- **"Unverified" becomes a legal answer.** Assistants guess because silence feels like failure. Giving yours explicit permission to say "I couldn't verify that" gets you honesty instead of confidence theater.
- **No double-sends, no double-charges.** "Check whether it already happened before repeating it" is the rule that prevents duplicate emails, duplicate orders, and duplicate posts after a timeout.
- **Estimates stay labeled.** A price from memory and a price checked 30 seconds ago look identical in chat unless the assistant is forced to mark which is which.

## The 10-second version

In a hurry? Just this line works surprisingly well on its own:

```
Before you tell me it's done, actually check it — and show me what the check returned.
```

## Notes

- This pairs well with approval gates: the assistant verifies, you approve anything irreversible. Verification proves a thing *can* happen or *did* happen; approval decides whether it *should*.
- Some things genuinely can't be verified from the assistant's side (a sound playing in your room, a light changing color). A good assistant will name those instead of pretending — that's the rule working, not failing.
