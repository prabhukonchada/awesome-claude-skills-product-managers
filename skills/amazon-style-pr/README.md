# Amazon-Style Press Release (Working Backwards)

Write Amazon-style internal press releases as polished Word documents — the kind Amazon PMs write *before* building a product.

## Why This Skill Exists

Amazon's Working Backwards methodology starts with a press release. Not a PRD, not a design doc — a press release. The idea is simple: if you can't write a compelling announcement for a product that doesn't exist yet, you probably shouldn't build it.

This skill automates that process with Claude. You describe your product idea, and Claude interviews you, writes the press release following Amazon's proven structure, and outputs a professionally formatted `.docx` file ready for stakeholder review.

## What It Does

1. **Interviews you** — Asks targeted questions about your customer, their problem, your solution, and what makes it different
2. **Writes the press release** — Follows the exact Amazon structure: heading, subheading, problem, solution, spokesperson quote, how-it-works, customer quote, and call to action
3. **Generates a .docx file** — Clean, executive-ready formatting with proper typography, quote callouts, and professional layout

## The Amazon PR Structure

The press release follows this flow (sections are invisible to the reader — it reads as a narrative, not a form):

- **Heading** — Product name, instantly clear to the target customer
- **Subheading** — Who it's for + the single biggest benefit
- **Summary** — 2-3 sentences setting the scene
- **Problem** — The heart of the PR. Vivid, specific customer pain with concrete scenarios
- **Solution** — How the product solves the problem (customer experience, not architecture)
- **Spokesperson Quote** — Vision and commitment, not feature repetition
- **How It Works** — Step-by-step customer experience with a "wow moment"
- **Customer Quote** — Behavior change, not generic praise
- **Call to Action** — Where and how to get started

## Installation

Copy the `amazon-style-pr` folder into your Claude skills directory:

```bash
# For Claude Desktop / Cowork
cp -r amazon-style-pr ~/.claude/skills/

# For Claude Code (project-level)
cp -r amazon-style-pr .claude/skills/
```

## Usage

Just tell Claude what you're building. Any of these will trigger the skill:

- "I have a product idea I want to think through"
- "Write a PR/FAQ for our new feature"
- "Help me write an Amazon-style press release"
- "I want to use the working backwards method"

Claude will interview you, write the press release, and generate a `.docx` file.

## Writing Principles Baked In

This skill enforces the principles that separate great Amazon PRs from mediocre ones:

- **Problem > Solution** — Disproportionate effort on the problem paragraph
- **Numbers > Adjectives** — "Fast" becomes "under 60 seconds"
- **General audience** — No jargon, no acronyms
- **Customer quotes reveal behavior change** — Not "I love it" but "I used to spend 3 hours, now it's automatic"
- **Bold promises** — If the PR feels safe, the ambition is too low

## Example Triggers

| What You Say | What Claude Does |
|---|---|
| "I have an idea for an AI feature" | Interviews you, then writes a full PR |
| "Write a PR/FAQ for our new onboarding flow" | Skips questions you've already answered, writes the PR |
| "Help me think through this product concept" | Uses the PR format as a thinking tool |

## Credits

Based on Amazon's Working Backwards methodology, adapted for AI-assisted product management.

Built by [Prabhu Konchada](https://github.com/prabhukonchada).
