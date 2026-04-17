# Draft reply — anatomy of a voice match

This file walks through how the skill turns a raw inbox message into a draft that sounds like *you*, not like a generic assistant. Read it alongside `triage-report.md`.

## The incoming email

> **From:** Sarah Chen <sarah@acmeglobal.example>
> **To:** You <you@example.com>
> **Subject:** Q2 budget sign-off needed by 5pm today
> **Received:** 2026-04-17 08:12
>
> Hey — need your sign-off on the reallocation toward infra (cloud migration line + additional storage). Procurement is blocked until you approve. Attaching the revised spend sheet; changes are highlighted on rows 12–18.
>
> Push back today if you see anything off. Otherwise a simple "approved" works.
>
> Sarah

## Voice card extracted from your Sent Mail (this run)

| Signal | Observation | Source |
|---|---|---|
| Greeting | None on internal threads; "Hi X," only external | 14 of 18 sampled messages |
| Sign-off | `— Alex` | 16 of 18 |
| Length | 2–3 sentences median on approvals | — |
| Hedges / filler | Avoids "just wanted to", "hope you're well", "circle back" | 0 occurrences |
| Recurring vocab | "loop in", "flag", "directionally", "tail issues" | 7 occurrences across 6 msgs |
| Structure | Prose, no bullets in reply emails | — |
| Conditional thinking | Frequently flags dependent risks ("if X slips, then Y") | 4 of 18 |

## The generated draft

> **To:** Sarah Chen — **Re:** Q2 budget sign-off needed by 5pm today
>
> Approved on the reallocation. One flag — the cloud line assumes the Sat migration lands clean; if it slips we'll need to revisit the compute split. Will loop you in either way by Mon morning.
>
> — Alex

## Why this draft, trait by trait

- **"Approved on the reallocation."** — Opens with the action Sarah asked for, in your internal-threads style (no greeting).
- **"One flag —"** — Your sampled sent mail uses "flag" as a verb five times in two weeks. Matches register.
- **"if it slips we'll need to revisit…"** — Conditional-risk framing, lifted straight from your observed pattern.
- **"Will loop you in…"** — "Loop in" is one of your recurring phrases.
- **"— Alex"** — Your default internal sign-off.
- **No hedges.** No "hope this helps", no "just wanted to confirm", no "let me know your thoughts". You don't write those.

## What the skill *didn't* do

- Didn't add a greeting. Internal thread, your sampled style skips it.
- Didn't restate the full context Sarah already knows. Your observed replies trust the recipient's memory of the thread.
- Didn't soften the conditional with "if it's not too much trouble" or similar. Not your voice.
- Didn't invent a specific Monday time — you hadn't committed to one, so the draft stays appropriately fuzzy ("Mon morning").

## What still needs your judgment

- Is "approved" actually the right call, or do you want to push back on any of rows 12–18? The skill approved because your thread history shows you generally greenlight Sarah's reallocations when the delta is <15%, but it can't see the spreadsheet rows — that's your call.
- Are you OK with the hedge about Saturday's migration? The skill added it because your sent mail pattern includes proactive risk flags; if you want a cleaner "approved" with no caveat, one word from you and it's gone.
