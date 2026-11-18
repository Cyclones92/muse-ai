# Prompt AI for Better Output — The 5-Part Anatomy 🎯⚡

> **Author:** Cyclones92
> **Category:** muse-ai
> **Last updated:** 2026-11-18
> **Works with:** Any AI assistant

## What this does

Most weak AI answers come from weak prompts, not a weak model. This guide gives you a five-part anatomy that fixes almost every prompt, a copy-verbatim master template, and the repair phrases that rescue a bad answer without starting over.

## The 5-part anatomy

Every strong prompt answers five questions:

| Part | Question it answers | Example |
|------|--------------------|---------|
| **1. Role** | Who should the AI act as? | "You are a patient teacher explaining this to a complete beginner." |
| **2. Task** | What exactly should it do? | "Write a one-page checklist for setting up a home router." |
| **3. Context** | What background matters? | "The reader has never changed a router setting before." |
| **4. Constraints** | What are the limits? | "Plain language, no jargon, under 400 words, no brand recommendations." |
| **5. Format** | What should the answer look like? | "Numbered steps, each step one or two sentences, with a short 'check it worked' line at the end." |

Miss a part and the AI guesses — and its guesses are where the weird answers come from.

## The master template

Copy this, fill in the brackets, send:

```
Role: You are [expert / teacher / editor / coach] for [audience].

Task: [The one thing you want done, as a verb phrase.]

Context: [Background the AI needs: what this is for, what already exists, what you already tried.]

Constraints:
- [Length, tone, reading level]
- [What to include]
- [What to leave out]
- Flag anything you are unsure about instead of guessing.

Format: [Bullets / numbered steps / table / short paragraphs], ending with [summary / checklist / next step].
```

That one line — **"Flag anything you are unsure about instead of guessing"** — is the highest-value sentence in this whole guide. It turns confident nonsense into an honest "I'm not sure about X," which you can actually work with.

## Seven techniques that stack

1. **Role prompting** — covered above; a role sets vocabulary, depth, and tone in one line.
2. **Few-shot examples** — show one or two examples of what you want ("here's a good one, match this style") instead of describing the style.
3. **Step-by-step reasoning** — "Work through this step by step before giving the final answer" for anything with logic or math.
4. **Delimiters** — wrap pasted material in triple backticks or `---` lines so the AI never confuses your source text with your instructions.
5. **Output scaffolding** — give the headings and let the AI fill them in. Structure in, structure out.
6. **Iterative refinement** — don't restart; reply to the draft: "Keep sections 1–2, shorten 3, make 4 funnier."
7. **Self-checks** — end with: "Before you finish, check your answer against my constraints and fix anything that doesn't fit."

## Before → after

**Before:** "Write something about password managers."

**After:** "You are a friendly security coach for non-technical readers. Write a short guide to choosing a first password manager. The reader currently reuses one password everywhere. Plain language, under 300 words, no brand names. Format: 3 short sections — Why it matters, What to look for, First steps this weekend. Flag anything you are unsure about instead of guessing."

Same model. Completely different answer.

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| Answer is generic mush | Add Context — the AI can't aim at a target it can't see |
| Answer is too long / too short | Add a length Constraint, in words or items, not vibes |
| Confident but wrong | Add the flag-unsure line + ask for sources or a self-check |
| Wrong shape entirely | Add Format with an example or headings to fill in |
| It ignored half the ask | Number your asks; ask it to confirm each one as it goes |

## Notes

- One task per prompt. Two tasks in one prompt gets you two half-answers.
- If a prompt works, save it. A small library of your own proven prompts beats re-typing (and re-guessing) every time.
