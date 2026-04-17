---
name: inbox-autopilot
description: Put the user's connected inboxes (Outlook + Gmail) on autopilot — review recent mail, prioritize what actually needs a response, and draft replies in the user's own voice so they just review and send. Categorizes mail into URGENT / IMPORTANT / FYI / SKIP, surfaces unanswered follow-ups from Sent Mail, and ghostwrites replies by first sampling the user's recent sent messages for voice match. Use this skill whenever the user asks to scan, triage, review, prioritize, summarize, or "deal with" their inbox, wants a morning/EOD email digest, mentions "inbox zero", "catch me up on email", "what needs a reply", "draft replies to the urgent stuff", or asks for any hands-off inbox handling. Also trigger when the user says things like "anyone I've left hanging?", "what did I miss overnight", or "go through my email" — even if they don't name a specific provider. Never send without explicit approval — the user is still the pilot.
---

# Inbox Autopilot

Put the user's inbox on autopilot: review the backlog, sort by urgency, surface threads waiting on a reply, and have drafts ready in the user's own voice so they just review and approve. Autopilot flies the plane — the user is still the pilot who decides what goes out. Always draft, never send, until the user explicitly approves.

## When to use this skill

Trigger on any of these intents:
- Triage / inbox zero ("go through my email", "what needs a reply", "catch me up on email")
- Morning briefings / EOD digests ("what came in overnight", "daily inbox summary")
- Follow-up audits ("who have I left hanging", "any threads I should nudge")
- Reply drafting ("help me respond to Jordan's email", "draft replies to the urgent stuff")

## Providers

This skill works across whichever mail MCPs are connected. The common ones for this user are:

- **Outlook / Microsoft 365** — use `outlook_email_search` for reads. For sent items filter on `folder:sent`. Use `read_resource` to open a specific message when the search preview isn't enough.
- **Gmail / Google Workspace** — use the Gmail MCP tool names available in the session (e.g. a `gmail_search_messages` / `gmail_get_message` pair). If no Gmail tool is present, tell the user Gmail isn't connected and offer to continue with Outlook only.

At the start of every run, list which providers you can actually see and confirm the scope before querying. Don't silently skip a provider the user expected — call it out.

## Workflow

Run the five steps in order. Do not skip Step 0 (voice sampling) — it is what makes the drafts sound like the user rather than like a generic assistant.

### Step 0 — Sample the user's voice (live)

Before drafting anything, pull 10–20 recent sent messages from each connected provider (last 14 days is usually enough). Skim them for:

- **Greeting pattern** — do they open with "Hi X," / "Hey X" / no greeting at all?
- **Sign-off** — "Thanks," / "— [name]" / nothing?
- **Sentence length** — terse 1–2 sentence replies, or fuller paragraphs?
- **Filler words** — do they use "just wanted to check", "hope you're well", or skip straight to the point?
- **Formatting** — do they use bullets, or always prose? Do they bold anything?
- **Register** — casual / formal / mixed-by-recipient?

Keep these observations as a short in-memory style card for this run. Reuse it for every draft below. If the user has fewer than ~5 sent messages to sample from, say so and ask whether to proceed with a conservative neutral style.

### Step 1 — Read the inbox

Read emails from the last 24 hours (or whatever window the user specified) across every connected provider. Extract for each message:

- sender (name + email)
- subject
- received timestamp
- read / unread status
- thread / conversation id (so replies can be grouped)
- body — first ~2000 characters is enough for triage

If the provider returns a preview-only result, open the full message only when categorization is ambiguous. Don't burn tool calls opening newsletters in full.

### Step 2 — Categorize

Place every message into exactly one tier:

- **URGENT** — action needed today. Deadlines, money moves, direct asks from leadership/customers/vendors with a clock on them.
- **IMPORTANT** — reply within 48h. Real opportunities, warm contacts, decisions you own but that can wait a day.
- **FYI** — no reply needed but worth knowing. Status updates, CC'd threads, notifications from systems the user cares about.
- **SKIP** — auto-skip. No-reply addresses, promotional blasts, cold outbound, anything that looks like mailing-list chatter the user hasn't engaged with before.

Heuristics that help:

- Direct "To:" with a question mark or imperative verb → likely URGENT or IMPORTANT.
- "CC:" only, and the user isn't named in the body → usually FYI.
- Sender domain matches a newsletter pattern (`news.`, `updates.`, `no-reply@`, `mailer-daemon`) → SKIP.
- If uncertain between tiers, round **up** toward URGENT for known key contacts and **down** toward FYI for unknown senders.

### Step 3 — Check follow-ups

Scan each provider's Sent folder for messages the user sent in the last 7 days that have had no inbound reply on the same thread. Surface them as a "Follow-ups" list separate from the inbox triage, with the original recipient, subject, date sent, and days since.

Don't include auto-responders or internal distribution lists as "no reply" — check whether any same-thread message came back from the same person or a delegate.

### Step 4 — Generate the summary

Output in this exact structure so it's scannable:

```
# Inbox Triage — <date> (window: last <N> hours)
Providers checked: <list>

## URGENT (<count>)
- <sender> — <subject> — <one-line context / ask> — <received time>
- ...

## IMPORTANT (<count>)
- ...

## FYI (<count>)
- ...

## Follow-ups I'm waiting on (<count>)
- <recipient> — <subject> — sent <N> days ago — <one-line context>

## Skipped (<count>)
<one-line tally by category, no per-message detail>
```

Keep the one-line context honest and specific ("approving the Q2 budget" beats "important business topic"). If nothing is urgent, say so plainly — don't pad the list.

### Step 5 — Draft replies

For every URGENT and IMPORTANT item, draft a reply using the voice card from Step 0. Rules:

- Brief by default — 1–3 sentences unless the thread genuinely needs more.
- Match the user's greeting + sign-off patterns from Step 0.
- Strip filler phrases ("just wanted to circle back", "hope this finds you well") unless the user's own sent mail uses them.
- When a question can't be answered without info the user hasn't given you, draft a version that asks the clarifying question — don't invent facts or commitments.
- For calendar / scheduling asks, draft the reply but flag that a specific time slot still needs the user's OK (or suggest pulling from the calendar tool if available in the session).

Present drafts under the summary, grouped by tier:

```
## Drafted replies

### URGENT
**To: <sender> — Re: <subject>**
<draft body>

---
### IMPORTANT
**To: <sender> — Re: <subject>**
<draft body>
```

**Never send a reply.** End the response with a short explicit note: "Drafts only — say the word and I'll send, edit, or redraft any of these."

## Safety rails

- Do not mark messages read, archive, delete, move, or send anything. This skill is read-and-draft only unless the user explicitly says "send it" / "archive those" / "mark read".
- If you can't access a provider the user expects, surface the failure up front. Don't silently degrade to a partial run.
- Never include body content from messages flagged as confidential, legal-privileged, or HR-sensitive in the summary — reference them by subject and sender only, and note that full content was withheld.
- If the voice sample suggests the user writes very differently to different audiences (e.g., terse to internal, warmer to customers), segment the style card by audience rather than averaging it into mush.

## Output format notes

- Default to markdown. If the user asks for a plain-text email or a Slack-ready blurb, adapt.
- Don't wrap the whole thing in a code fence — the structural headers above are the structure.
- If the user asks for "just the urgent stuff" or "one-liner version", collapse to a single-tier list — don't force the full template.
