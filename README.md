<p align="center">
  <img src="assets/logo.svg" width="120" alt="What to Use When logo" />
</p>

<h1 align="center">What to Use When</h1>

<p align="center">
  <strong>A Microsoft 365 Copilot Cowork skill that routes each task to the right Microsoft AI tool —
  before you spend Cowork consumption.</strong>
</p>

<p align="center">
  <img alt="Skill health score" src="https://img.shields.io/badge/skill%20health-98%2F100%20Excellent-2ea44f" />
  <img alt="Trigger reliability" src="https://img.shields.io/badge/trigger%20reliability-100%25%20(4%20judges)-2563eb" />
  <img alt="Platform" src="https://img.shields.io/badge/platform-M365%20Copilot%20Cowork-7c3aed" />
  <img alt="License" src="https://img.shields.io/badge/license-MIT-blue" />
</p>

---

## Table of contents

- [What it does](#what-it-does)
- [Why it exists](#why-it-exists)
- [See it in action](#see-it-in-action)
- [How it works](#how-it-works)
- [What it routes (and what it doesn't)](#what-it-routes-and-what-it-doesnt)
- [Deploy it — end users](#deploy-it--end-users-personal-skill)
- [Deploy it — organizations](#deploy-it--organizations-share--publish)
- [Repository structure](#repository-structure)
- [Validation & test reports](#validation--test-reports)
- [Configuration](#configuration)
- [FAQ](#faq)
- [Contributing](#contributing)
- [Disclaimer](#disclaimer)
- [License](#license)

---

## What it does

**What to Use When** is a skill for **Microsoft 365 Copilot Cowork**. Whenever you ask Cowork to do
something a *free* Microsoft 1P (first-party) agent could already do — summarize your inbox, recap a
meeting, draft a document, build a few slides, research a topic, analyze a dataset, or answer a quick
question — this skill steps in **first**, recommends the included tool, and asks whether you'd like to
use it instead of spending Cowork consumption.

It is, in effect, an interactive version of Microsoft's *"what to use when"* guidance for the Copilot
family — turning that decision into an in-product nudge that also **trains users** to reach for the
right tool next time.

> It is **not** one-directional. When a task genuinely needs Cowork — a multi-step job that chains
> several sources into two or more finished deliverables — the skill stays out of the way and lets
> Cowork run.

## Why it exists

Microsoft 365 Copilot **Cowork** runs on **usage-based consumption**. Meanwhile, a large share of
everyday tasks can be completed by capabilities that are **already included** in a Microsoft 365
Copilot license at no extra cost:

| Included capability | Great for |
|---|---|
| **Microsoft 365 Copilot Chat** | Quick questions, find/summarize email · meetings · Teams, brainstorming |
| **Copilot in Word / Excel / PowerPoint** ("Edit with Copilot") | Creating or editing **one** document, workbook, or deck |
| **Researcher** (included, shared monthly cap) | Deep, multi-source, cited research |
| **Analyst** (included, shared monthly cap) | Data analysis — trends, anomalies, running the numbers |
| **Specialized 1P agents** (Sales, Service, Finance) | Domain workflows (entitlement varies) |

The skill's job is to **guide users to the included tool first**, so organizations get the value of
Cowork for the heavy, multi-output work it's built for — and don't spend consumption on tasks a free
agent already covers.

## See it in action

> **📸 Screenshots below are placeholders.** Drop the images you captured into `docs/screenshots/`
> using the filenames shown, and they'll render here automatically. (See
> [`docs/screenshots/README.md`](docs/screenshots/README.md) for the full list.)

**1. The skill intercepts a request and recommends the free tool**

![What to Use When recommending Copilot Chat](docs/screenshots/skill-in-action-1.png)

**2. The confirmation gate — use the included agent, or continue in Cowork**

![Confirmation gate](docs/screenshots/skill-in-action-2.png)

**3. Hand-off with a one-click link to Microsoft 365 Copilot Chat**

![Hand-off to Copilot Chat](docs/screenshots/skill-in-action-3.png)

## How it works

The skill follows a strict **precedence-first** flow so it fires *before* any retrieval, task
creation, or file generation:

1. **Precedence check** — runs *before* any thinking, data retrieval, `TaskCreate`, or invoking a
   doc/deck/spreadsheet builder. If action-bias would push Cowork to start building, it stops first.
2. **Exclusion check** — direct M365 *actions* (send an email, schedule a meeting, post to Teams,
   create an event) are handed straight back to the normal action path. They are never gated.
3. **Phase 1 — Classify** the task: how many finished outputs? how many apps/files? does it chain
   web + work sources? One output / one app / one question → a free 1P capability almost always fits.
4. **Phase 2 — Recommend** the included capability, in 2–3 crisp sentences, with a one-line "how to
   use it."
5. **Phase 3 — Confirm** via a two-option gate: *Use the included agent* or *Do it here in Cowork*.
6. **Phase 4 — Proceed** in Cowork **only** if the user explicitly chooses Cowork.

**What the end user sees is deliberately short** — a one-line **Classification**, a one-line
**Recommendation**, and the confirmation gate. No pricing, no credits, no cost figures.

## What it routes (and what it doesn't)

**✅ Fires (routes to a free 1P agent):**
- Summarize email / inbox / unread → **Copilot Chat**
- Summarize meetings, recap the standup → **Copilot Chat**
- Summarize Teams messages / chats / channels, over **any** window (e.g. "the last 5 weeks") → **Copilot Chat**
- "Catch me up" / "what did I miss" → **Copilot Chat**
- Single questions & lookups — *how / why / when / what / who / where*, plus calendar, contact, people, and billing/licensing questions → **Copilot Chat**
- Draft / rewrite one document → **Copilot in Word**
- Work on one workbook → **Copilot in Excel**
- Build a few slides → **Copilot in PowerPoint**
- Deep, cited research → **Researcher**
- Analyze a dataset → **Analyst**

**⛔ Does NOT fire (stays out of the way):**
- **Direct actions** — send/reply/forward email, schedule/cancel/decline a meeting, post to Teams, create an event *(these just execute)*
- **Genuinely multi-step, multi-output projects** *(Cowork is the right tool — it proceeds)*
- **Managing skills** *(handled by the skills tooling)*

## Deploy it — end users (personal skill)

Use this if you want the skill for **yourself**.

1. **Download** `skill/what-to-use-when/SKILL.md` from this repository.
2. In your OneDrive, open (or create) the folder:
   `Documents / Cowork / skills / what-to-use-when /`
3. **Place `SKILL.md`** inside that `what-to-use-when` folder. Keep the folder name and the `name:`
   field in the file **identical** (`what-to-use-when`).
4. Wait ~35 seconds for OneDrive to sync, then start (or refresh) a Cowork session. The skill appears
   in your skills list as **What to Use When** and triggers automatically on matching requests.
5. **Test it:** ask Cowork *"summarize my Teams messages from the last 5 weeks"* — the skill should
   recommend Copilot Chat and ask you to confirm.

## Deploy it — organizations (share / publish)

Use this to roll the skill out to a **team or the whole tenant**.

1. Add the skill to your own Cowork skills folder first (see the end-user steps above) and confirm it
   works.
2. In Cowork, open the skill and choose **Share**.
3. Scope the share to the intended **users or groups** (the share becomes available to recipients as a
   **plugin** — installed and auto-triggering, no manual import).
4. Cowork **validates** the skill on share (including the description length limit — see
   [Configuration](#configuration)). Resolve any validation error, then complete the share.
5. **Governance notes for admins:**
   - Recipients receive the **same validated version**; distribution is scoped and revocable.
   - Re-share after any edit to push the updated version to recipients.
   - The skill shows **no pricing** to end users, which makes it safe to share with customers.
   - Pair the rollout with a short note on *why* (use included Copilot capabilities first; reserve
     Cowork for multi-output work).

## Repository structure

```
what-to-use-when/
├── README.md                      ← you are here
├── LICENSE                        ← MIT
├── CHANGELOG.md                   ← version history
├── CONTRIBUTING.md                ← how to propose changes
├── .gitignore
├── assets/
│   └── logo.svg                   ← skill logo
├── skill/
│   └── what-to-use-when/
│       └── SKILL.md               ← the skill itself (deploy this)
├── docs/
│   └── screenshots/
│       └── README.md              ← screenshot filenames used by this README
└── reports/                       ← validation & test evidence (open in a browser)
    ├── skill-quality-report.html
    ├── precedence-test-report.html
    ├── trigger-reliability-report.html
    ├── behavioral-test-report.html
    ├── trigger-test-customer-share.html
    └── optimization-report.html
```

## Validation & test reports

The `reports/` folder documents how the skill was evaluated. Open any file in a browser.

| Report | What it shows |
|---|---|
| `skill-quality-report.html` | Static quality score (98/100, Excellent) across trigger clarity, instruction specificity, scope, and robustness |
| `precedence-test-report.html` | Independent-judge test that the skill fires **before** action-bias / build-immediately behavior |
| `trigger-reliability-report.html` | Multi-judge reliability run — recall / precision / flaky-trigger check |
| `trigger-test-customer-share.html` | Trigger test of the customer-share (no-pricing) version |
| `behavioral-test-report.html` | Behavioral runs — trigger correctness, workflow adherence, guardrails |
| `optimization-report.html` | Before/after of a validation-gated optimization pass |

> **Note on methodology:** the trigger/precedence results come from **independent-judge simulations**
> (multiple fresh agents each acting as the router, seeing only the description plus realistic
> competition). They are a strong signal of consistent triggering, **not** a live-router guarantee.
> Validate in a real Cowork session before wide rollout.

## Configuration

Everything the skill needs lives in the frontmatter of `skill/what-to-use-when/SKILL.md`:

```yaml
---
name: what-to-use-when          # must match the folder name
title: What to Use When         # friendly display name
description: >-                  # the routing signal — see the length limit below
  Run this FIRST, before ANY thinking, retrieval, task creation ...
cowork:
  category: automation
  icon: Compass                 # Fluent UI icon shown as the skill's logo in Cowork
  title: What to Use When
---
```

- **The `description` is what triggers the skill** — the router reads it to decide whether to invoke
  the skill. The body ("When to Use", etc.) is only read *after* it's selected. Keep trigger phrases
  in the description; keep long detail in the body.
- **Description length limit:** Cowork enforces a **1,024-character** limit on the description, counted
  in its **JSON-escaped** form (quotes, newlines, and non-ASCII characters each cost extra). This
  skill's description is written as a **folded scalar** (`>-`) with plain ASCII to stay safely under
  the limit (~990 escaped characters). If you extend it, keep it under 1,024 escaped.
- **Icon:** change `icon:` to any Fluent UI icon name to re-brand the skill's logo.

## FAQ

**Does it show customers any pricing?**
No. The skill deliberately shows **no** credit counts, dollar amounts, or estimates — only that the
recommended tool is "included at no extra cost." This makes it safe for customer-facing sharing.

**Will it block me when Cowork is genuinely the right tool?**
No. Multi-step, multi-output jobs are explicitly excluded — the skill proceeds without friction.

**Can it auto-open Microsoft 365 Copilot Chat with my prompt pre-filled?**
It provides a one-click link to open Copilot Chat, but Microsoft does not currently support
pre-filling a prompt via URL, so you paste the prompt after it opens. The skill never promises
auto-fill.

**The skill won't trigger — what do I check?**
Confirm the folder name and the `name:` field match exactly (`what-to-use-when`), that `SKILL.md` is
directly inside that folder, and that OneDrive has finished syncing. Then start a fresh Cowork session.

## Contributing

Issues and pull requests are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md). The most valuable
contributions are **new trigger scenarios** (with should-fire / should-not-fire examples) and routing
corrections.

## Disclaimer

This is a **community skill**, not an official Microsoft product. Microsoft product names,
capabilities, entitlements, and Cowork consumption/pricing are **subject to change** — verify current
details against official Microsoft documentation for your tenant. The author is not responsible for
consumption incurred; the skill is a guidance aid, not a billing control. Admins should continue to use
tenant-level controls for spend governance.

## License

Released under the [MIT License](LICENSE).
