# Prompt: Draft-Only Messages — Nothing Sends Without Your Exact Approval ✉️🛑

> **Author:** Cyclones92
> **Category:** muse-ai
> **Last updated:** 2026-11-18
> **Works with:** AI assistants connected to email, chat, or social accounts

## What this does

The moment an AI can send messages on your behalf, "helpful" can turn into "sent the wrong thing to the wrong person" at machine speed. This standing instruction sets the safest useful default: the assistant drafts, you approve the exact wording, and only then does anything send — and afterwards it proves the send in the actual thread.

## The prompt

```
Standing rule for all messages, emails, and posts you handle for me: draft-only, approval-gated.

- Draft freely. Sending is never part of drafting.
- Nothing sends — no email, message, reply, or post — without my exact approval of the final wording. Show me the complete draft: recipient, subject if any, and the full text. My approval of an earlier version does not cover an edited version; if the text changes after I approve it, show me the new version and wait again.
- A thumbs-up or "looks good" about the idea is not approval of the wording. If you are unsure whether I approved the exact text, ask.
- Different threads are different sends. Approval to message someone directly is not approval to post in a group, and the other way around.
- After sending, verify it in the actual conversation thread and tell me you confirmed it there. "I clicked send" is not proof.
- If a send fails, times out, or you cannot tell whether it went through, say so before trying again — never silently re-send.
- When you report on messages from other people, report what they said faithfully. Do not soften, summarize away, or editorialize the parts you think I won't like.
```

## Why it works

- **The draft/send line is bright.** Most AI messaging accidents happen in the blurry zone — "I thought you wanted me to just handle it." This rule removes the blur.
- **Approval covers exact text, not vibes.** A draft you approved and a draft the AI "improved" afterwards are two different messages. Only one of them has your name on it in every sense.
- **Thread-level precision.** Direct message vs. group chat vs. public post have wildly different blast radii. The rule forces the assistant to treat them as separate decisions.
- **Verify in the thread.** Sends fail silently more often than you'd think. Checking the actual thread is the only proof that counts.

## Tuning it

- **Trusted low-stakes exceptions:** you can carve out narrow ones once trust is built — e.g. "You may send the weekly status post to my own private server without asking, using the approved template only." Keep exceptions specific: one destination, one template, one purpose.
- **Never carve out:** first contact with a new person, anything involving money, anything emotional, anything you haven't seen the final text of. Those stay gated forever.

## Notes

- This rule pairs with [Verify Before You Claim It's Done](prompt-verify-before-you-claim-done.md): approval decides *whether* to send, verification proves it *landed*.
- If your assistant supports per-action approval prompts, turn them on for sends — the prompt above is the policy, the approval card is the lock.
