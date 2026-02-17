# AGENTS.md

> Project instructions for AI coding agents. This file is automatically picked up by compatible AI IDEs and agents.

## Project Identity

- **Repo**: `ai-agent-skills`
- **Description**: An agnostic collection of AI Agent Skills
- **Standard**: [Agent Skills open standard](https://agentskills.io)
- **Scope**: Platform-agnostic, vendor-neutral skill collection
- **Audience**: Developers and teams using any AI agent platform

## Core Rules

1. This is NOT a Claude-specific project. Do not assume Claude as the only runtime.
2. This is NOT a fork of any vendor's repo. It is an independent collection.
3. All skills must follow the `SKILL.md` standard with YAML frontmatter.
4. All content must be portable across Agent Skills-compatible platforms.
5. Use "AI agent" or "agent" as the default subject — not any specific product name.
6. Write in simple, clear English — the audience includes non-native speakers.
7. Be practical and direct — no hype, no filler, no marketing language.

## Excluded Content — Do NOT Reintroduce

The following content was intentionally removed from this project. Do not add it back in any form.

### Vendor SDK / API Code

- No vendor-specific SDK imports, API calls, or client patterns
- No Anthropic SDK (`client.messages.create`, `container={"skills": [...]}`, beta headers)
- No OpenAI SDK, Google AI SDK, or any other vendor-locked code
- No model strings tied to specific providers
- No Files API or vendor-specific file handling code

### Platform-Specific UI / Installation Flows

- No "upload via Settings > Capabilities" or similar UI-bound instructions
- No Cowork, Claude Desktop, or any desktop app references as primary paths
- No Jupyter notebook structure or notebook-based tutorials
- No CLI commands specific to a single tool (e.g., Claude Code only)
- Platform-specific instructions belong in `docs/platforms/` if needed, not in skill files

### Document Format Skills (xlsx, pptx, pdf, docx)

- These are vendor built-in skills, not part of this collection
- Do not add document creation/manipulation skills as core features
- Do not position Excel, PowerPoint, PDF, or Word generation as key repo capabilities
- Document skills may be referenced as examples of what skills CAN do, not what this repo provides

### Vendor-Locked Connector Tables

- No per-role connector lists (e.g., "Sales: Slack, HubSpot, Close, Clay...")
- No `.mcp.json` as the only connector pattern
- Connectors are referenced as a concept but kept platform-agnostic

### Financial / Domain-Specific Sample Data

- No `financial_statements.csv`, `portfolio_holdings.json`, or similar bundled datasets
- The repo is general-purpose — use domain-neutral examples when possible

### Branding and Framing

- No "Claude Skills Cookbook", "Claude Capabilities", or vendor-branded naming
- No "X company is open-sourcing..." framing
- No vendor acknowledgment sections
- No emojis in section headers
- Do not position this project as a product or extension of any vendor

## Architecture Principles

### Skill Structure

Every skill is a folder containing at minimum a `SKILL.md` file:

```
skill-name/
├── SKILL.md              # Required: YAML frontmatter + instructions
├── scripts/              # Optional: executable code
├── templates/            # Optional: output templates
├── references/           # Optional: supplemental docs
├── examples/             # Optional: sample inputs/outputs
└── resources/            # Optional: assets, data files
```

### SKILL.md Standard

```yaml
---
name: skill-name # Required, max 64 chars, lowercase-with-hyphens
description: > # Required, max 200 chars
  What this skill does and when
  an agent should activate it.
---
# Skill Name

## When to use this skill
## Instructions
## Examples
## Guidelines
```

### Progressive Disclosure

Skills load in layers to minimize token usage:

1. **Frontmatter only** — Agent scans `name` + `description` to decide relevance
2. **SKILL.md body** — Full instructions load only when the skill activates
3. **Supporting files** — Scripts, references, templates load on demand during execution

### Modularity

- One skill = one job
- Skills must be self-contained — no hard dependencies on other skills
- For multi-workflow skills, use a menu pattern: describe options in SKILL.md, reference separate files for each path
- Multiple skills can activate together, so design for composability

## Folder Structure

```
ai-agent-skills/
├── skills/
│   ├── roles/                    # Role-based skill packs
│   │   ├── productivity/
│   │   ├── sales/
│   │   ├── customer-support/
│   │   ├── product-management/
│   │   ├── marketing/
│   │   ├── legal/
│   │   ├── finance/
│   │   └── data/
│   └── domain/                   # Domain-specific skills
│       ├── brand-guidelines/
│       ├── code-review/
│       └── ...
├── templates/
│   └── skill-template/
│       └── SKILL.md
├── docs/
│   └── platforms/                # Platform-specific setup guides (if needed)
├── AGENTS.md                     # This file
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

## When Adding New Skills

1. Follow the `SKILL.md` frontmatter standard — `name` and `description` are required
2. Keep descriptions under 200 characters — they determine auto-activation
3. Use the menu/modular pattern for skills covering multiple workflows
4. Include examples of expected output
5. Test with multiple prompt variations before committing
6. Never hardcode API keys, passwords, or secrets in skill files
7. Place skills in the correct category: `roles/` for job-function packs, `domain/` for field-specific expertise
8. Keep supporting files (scripts, templates) referenced from SKILL.md so agents know when to load them

## Writing Style for Documentation

- Simple, clear English — avoid academic or uncommon terms
- Practical over theoretical
- Show, don't just describe — include examples
- When referencing platforms, list them as options, don't single one out
- Vendor docs can be linked as references, never as primary documentation

## Compatibility Notes

This file follows the `AGENTS.md` convention for AI coding agents. For platform-specific agent config:

| File                              | Platform             |
| --------------------------------- | -------------------- |
| `AGENTS.md`                       | Agnostic (this file) |
| `CLAUDE.md`                       | Claude Code          |
| `.cursorrules`                    | Cursor               |
| `.windsurfrules`                  | Windsurf             |
| `.github/copilot-instructions.md` | GitHub Copilot       |

If your IDE requires a different filename, symlink or copy this file accordingly.
