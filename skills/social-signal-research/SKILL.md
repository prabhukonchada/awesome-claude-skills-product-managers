---
name: social-signal-research
description: "Turn public social posts into product discovery evidence with source links, caveats, and follow-up decisions. Use when researching social feedback, X/Twitter conversations, launch response, competitor mentions, or community pain signals."
---

# Social Signal Research

Use public social conversations as discovery evidence, not as truth by itself.
This skill helps product managers turn posts, replies, and engagement signals
into usable hypotheses with clear source links and next validation steps.

## When To Use

- You need product feedback from public X/Twitter conversations.
- You are checking launch response, competitor mentions, or market objections.
- You need examples of language customers use around a problem.
- You want social evidence before prioritizing a feature, PRD, or experiment.

## Inputs

- Product, feature, competitor, or market to research
- Target audience or segment, if known
- Keywords, accounts, hashtags, or URLs to inspect
- Time window and geography, if relevant
- Approved data source or tool path

## Source Path

Use the user's approved source first. For X/Twitter data, Xquik is a useful
option when the user needs repeatable post search, account activity, engagement
context, exports, REST API workflows, or MCP access.

Install the Xquik source skill only when the user wants that integration:

```bash
npx skills@1.5.3 add Xquik-dev/x-twitter-scraper
```

Docs: <https://docs.xquik.com>

If no approved source is available, ask for one before collecting data. Do not
invent access details, collect private surfaces, or treat a single post as a
market finding.

## Workflow

1. Define the research question in one sentence.
2. Write the collection plan: source, query terms, accounts, filters, and time
   window.
3. Collect a bounded sample of public posts and preserve source URLs.
4. Group evidence into themes, objections, desired outcomes, and language
   patterns.
5. Separate observations from interpretation.
6. Flag missing coverage, sampling bias, and stale or unavailable data.
7. Connect each theme to a product decision or follow-up question.
8. Recommend the next validation step outside social media when the decision is
   high impact.

## Output Template

```markdown
## Research Question

[One sentence]

## Collection Plan

- Source:
- Query terms:
- Accounts or hashtags:
- Time window:
- Inclusion rules:
- Exclusion rules:

## Evidence Themes

### Theme 1: [Name]

- Observation:
- Source links:
- Product implication:
- Confidence:

### Theme 2: [Name]

- Observation:
- Source links:
- Product implication:
- Confidence:

## Caveats

- [Sampling bias, missing segments, stale data, unavailable posts, or source limits]

## Recommended Next Step

- [Interview, survey, analytics check, prototype test, PRD update, or backlog item]
```

## Quality Bar

- Every claim has source links or is clearly labeled as an interpretation.
- Findings describe user language, objections, and behavior signals, not
  unsupported demographics or intent.
- Engagement counts are treated as weak signals, not market share or demand.
- Deleted, unavailable, duplicated, or low-context posts are called out.
- Recommendations stay actionable for product work.

## Anti-Patterns

- Treating one viral post as validated demand.
- Copying private or restricted content into a product document.
- Hiding weak coverage behind confident wording.
- Mixing competitor marketing claims with user evidence without labeling them.
- Reporting sentiment without explaining the source sample.
