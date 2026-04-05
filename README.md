# Awesome Claude Skills for Product Managers

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated collection of [Claude](https://claude.ai) skills built for Product Managers. Drop these into your Claude setup and unlock PM superpowers — from writing Amazon-style press releases to running experiments and crafting PRDs.

## What Are Claude Skills?

Claude skills are reusable prompt templates that teach Claude how to perform specific tasks with expert-level quality. Think of them as playbooks — when you trigger a skill, Claude follows a battle-tested workflow instead of winging it.

## Available Skills

| Skill | Description | Trigger Phrases |
|---|---|---|
| [**amazon-style-pr**](./skills/amazon-style-pr/) | Write Amazon-style Working Backwards press releases as polished Word documents | "PR/FAQ", "working backwards", "press release", "I have a product idea" |

> More skills coming soon: PRD Writer, Experiment Framework, Competitor Analysis, User Interview Synthesizer

## Quick Start

### Option 1: Claude Desktop (Cowork Mode)

```bash
# Clone the repo
git clone https://github.com/prabhukonchada/awesome-claude-skills-product-managers.git

# Copy the skill you want
cp -r awesome-claude-skills-product-managers/skills/amazon-style-pr ~/.claude/skills/
```

### Option 2: Claude Code (Project-Level)

```bash
# From your project root
cp -r awesome-claude-skills-product-managers/skills/amazon-style-pr .claude/skills/
```

### Option 3: Manual

Just tell Claude what you need. If the skill is installed, it auto-triggers:

> "Help me write a PR/FAQ for my new feature"

## Why This Exists

Product managers spend too much time on repetitive writing tasks that follow known frameworks. Amazon PRs, PRDs, experiment docs — these all have a structure. Claude is great at following structure, but only if you teach it well.

These skills encode years of PM experience into reusable Claude prompts so you can focus on thinking, not formatting.

## Contributing

Have a PM skill that's helped you ship better products? PRs welcome!

Each skill needs:
- A `SKILL.md` file with the full skill definition (this is what Claude reads)
- A `README.md` explaining what the skill does and how to use it

See [skills/amazon-style-pr](./skills/amazon-style-pr/) for the template to follow.

## Star This Repo

If these skills help you ship better products, give this repo a star. It helps other PMs discover these tools.

## Author

Built by [Prabhu Konchada](https://github.com/prabhukonchada) — Head of Product with 10 years of B2B SaaS experience, scaled Apxor Nudges from 0 to $5M ARR. Currently building the world's best AI counsellor at [EdNxt.ai](https://ednxt.ai).

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/prabhukonchada) [![Website](https://img.shields.io/badge/Website-000000?style=flat&logo=safari&logoColor=white)](http://www.prabhukonchada.com)

---

*These skills are open-source and free to use. If they save you even one hour, that's a win.*
