# ⚡ muse-ai — HOWTO Guides by Cyclones92

```
 ██████╗██╗   ██╗ ██████╗██╗      ██████╗ ███╗   ██╗███████╗███████╗ █████╗ ██████╗
██╔════╝╚██╗ ██╔╝██╔════╝██║     ██╔═══██╗████╗  ██║██╔════╝██╔════╝██╔══██╗╚════██║
██║      ╚████╔╝ ██║     ██║     ██║   ██║██╔██╗ ██║█████╗  ███████╗╚██████║ █████╔╝
██║       ╚██╔╝  ██║     ██║     ██║   ██║██║╚██╗██║██╔══╝  ╚════██║ ╚═══██║██╔═══╝
╚██████╗   ██║   ╚██████╗███████╗╚██████╔╝██║ ╚████║███████╗███████║ █████╔╝███████╗
 ╚═════╝   ╚═╝    ╚═════╝╚══════╝ ╚═════╝ ╚═╝  ╚═══╝╚══════╝╚══════╝ ╚═════╝ ╚══════╝
```

**Guides, blueprints, and paste-ready prompts from the lab.** Homelab, Linux, Windows, networking, security, automation — and a growing stack of Muse / AI builds you can steal and make your own. 🌪️

> Every guide runs on example gear — `example.com`, `192.0.2.x`, and a trusty sidekick named `Cyclones92`. Swap in your own values and ride.

## 🗂️ The map

```
guides/
  muse-ai/      # Muse Spaces, prompts & AI workflows 🤖
  linux/        # Linux setup, services, troubleshooting 🐧
  windows/      # Windows setup & administration 🪟
  networking/   # DNS, VPN, firewalls 🌐
  security/     # Hardening & best practices 🔐
  homelab/      # Self-hosted everything 🏠
  automation/   # Scripts, cron & scheduled magic ⏰
templates/
  howto-template.md   # The launchpad for every new guide 🚀
```

New topic? New folder under `guides/`. One topic, one folder, no mercy for clutter.

## 📚 Guides

| Guide | Category | What's inside |
|-------|----------|---------------|
| [Build Specs: Everything We're Working On + Usage](guides/muse-ai/build-specs-everything-were-working-on-and-usage.md) | Muse / AI 🤖 | Two Space blueprints — a static snapshot dashboard + a fullstack usage tracker, with paste-ready Prompts A & B |
| [Build Specs: All My Spaces + Daily Posts](guides/muse-ai/build-specs-all-my-spaces-and-daily-posts.md) | Muse / AI 🤖 | Two more blueprints — a hub where every card opens in a new tab, and a digest ledger that embeds HTML *inside* the Space, with paste-ready Prompts C & D |
| [How to Build Wonton Work](guides/muse-ai/howto-wonton-work.md) | Muse / AI 🤖 | Run a crew of dumpling bot jobs — Instructions / Memory / Skills, a shared Skill library, draft → Deploy, and one numbered list per run, with paste-ready Prompt E 🥟 |
| [Prompt: Forget a Topic — Full Delete & Forget](guides/muse-ai/prompt-forget-a-topic.md) | Muse / AI 🤖 | Make your assistant truly forget a topic — plan first, exact-yes gate, kill the jobs that would recreate it, verify with a fresh search 🧹 |
| [Prompt AI for Better Output](guides/muse-ai/prompt-ai-for-better-output.md) | Muse / AI 🤖 | The 5-part prompt anatomy (Role, Task, Context, Constraints, Format), a copy-verbatim master template, and repair phrases that rescue bad answers 🎯 |
| [Prompt: Sanitize Before You Share](guides/muse-ai/prompt-sanitize-before-you-share.md) | Muse / AI 🤖 | Scrub names, emails, IPs, and secrets out of a document before it goes public — with a change report, never a silent edit 🧼 |
| [Prompt: Verify Before You Claim It's Done](guides/muse-ai/prompt-verify-before-you-claim-done.md) | Muse / AI 🤖 | A standing rule that flips AI work to prove-it-first: real checks, result before explanation, estimates labeled ✅ |
| [Prompt: Draft-Only Messages](guides/muse-ai/prompt-draft-only-messages.md) | Muse / AI 🤖 | Nothing sends without your exact approval of the final wording — and the send gets verified in the actual thread ✉️ |
| [Prompt: The Weekly System Audit](guides/muse-ai/prompt-weekly-system-audit.md) | Muse / AI 🤖 | A weekly police-job audit for your AI setup: stuck jobs, backups, permissions, data flows — verdict on top, fixes split into Fixed vs. Needs your OK 🛡️ |
| [Template: Standing Instructions](guides/muse-ai/template-standing-instructions.md) | Muse / AI 🤖 | Give your AI a personality doc + an operating-rules doc, so it works your way every session 🧭 |
| [How to set up SSH key login](guides/linux/ssh-key-login.example.md) | Linux 🐧 | Ditch the password, keep the keys — a quick example guide in the house format |

## ✍️ Writing a guide?

Grab `templates/howto-template.md`, drop it in the right folder, name it `how-to-do-the-thing.md` (kebab-case or it didn't happen), and link it in the table above.

## License

MIT — see [LICENSE](LICENSE). Take it, build on it, ship something cool. ⚡
