# inbox-autopilot

A Claude skill that puts your connected inboxes on autopilot — reviews the mail, prioritizes what actually needs a response, and has drafts ready in *your* voice so you just review and send.

Autopilot flies the plane. You're still the pilot — nothing goes out until you explicitly approve.

Built for PMs and operators who live in email, don't want to read newsletters, but absolutely cannot miss the one message from their CEO that landed at 6:42am — and definitely can't have an AI sending replies that sound like a chatbot.

## What it does

When triggered, the skill runs a five-step workflow:

0. **Samples your voice.** Pulls 10–20 of your recent sent messages before drafting anything, so replies sound like you wrote them — your greeting pattern, your sign-off, your sentence length, your vocabulary.
1. **Reads the inbox** from the last 24 hours (or a window you specify) across every mail provider connected in the current Claude session.
2. **Prioritizes** every message into `URGENT`, `IMPORTANT`, `FYI`, or `SKIP`.
3. **Checks follow-ups** — scans Sent Mail from the last 7 days for threads you're still waiting on.
4. **Generates a summary** in a clean scannable format.
5. **Drafts replies** for every URGENT and IMPORTANT item — but never sends.

## Supported providers

- Outlook / Microsoft 365 (via the Outlook MCP)
- Gmail / Google Workspace (via a Gmail MCP, when available in the session)

The autopilot is provider-aware: it tells you which inboxes it actually reached before summarizing, so a missing connection never silently produces a half-empty triage.

## Install

This is a Claude skill, not a standalone script. Drop the `inbox-autopilot/` folder into your Claude skills directory:

```
<your-claude-home>/skills/inbox-autopilot/
```

For Cowork users, that typically lives at `~/.claude/skills/`. For Claude Code, follow the normal skill install path for your environment.

Once installed, Claude will trigger the skill automatically on prompts like:

- "catch me up on my inbox"
- "what needs a reply today?"
- "anyone I've left hanging this week?"
- "review my email and draft responses to the urgent stuff"
- "what came in overnight?"

## Example output

See [`examples/triage-report.md`](examples/triage-report.md) for what a real run looks like, and [`examples/draft-reply.md`](examples/draft-reply.md) for a sample generated reply — with annotations showing which voice signals from your sent mail drove each phrase.

## Design notes

A few things this skill deliberately does, and why:

- **Samples voice live from Sent Mail instead of using a static rulebook.** Your writing changes over time and shifts with audience; a frozen "always be terse" rule produces drafts that read like every other LLM's. Reading your last 14 days of sent mail each run keeps the drafts current and audience-appropriate.
- **Never sends.** Every draft ends behind an explicit approval gate. Autopilot flies the plane; the pilot still chooses when the wheels go up. The cost of one wrong send is much higher than the cost of one extra "send it" keystroke.
- **Calls out missing providers.** If Gmail isn't connected but you asked for "all my inboxes", the skill says so up front instead of quietly returning an Outlook-only summary.
- **Rounds uncertain messages toward URGENT for known contacts and FYI for unknown ones.** False-urgent from a stranger wastes a minute; false-FYI from your CEO is a real problem. When in doubt, escalate by reputation.

## Contributing

Found a failure mode? Open an issue with:

- The prompt that triggered the skill
- The structure of the output that went wrong (redact bodies — subjects + senders are enough)
- What you expected instead

Style and voice feedback is especially useful — those are the hardest parts to tune generically.

## License

See the repo's top-level LICENSE.
