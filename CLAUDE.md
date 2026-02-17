# AI Agent Skills — Project Guidelines

## Project Identity

- **Repo**: `ai-agent-skills`
- **Description**: An agnostic collection of AI Agent Skills
- **Scope**: Platform-agnostic skills following the open Agent Skills standard (agentskills.io)
- **Audience**: Developers and teams using any AI agent platform, not just Claude

## What This Project Is NOT

This is NOT a Claude-specific project. It is NOT a fork of Anthropic's repos. It is an independent, vendor-neutral collection. All content must reflect this.

## Excluded Content — Do NOT Reintroduce

### Anthropic SDK / API Code

- No `client.messages.create()` or Anthropic Python SDK patterns
- No `container={"skills": [...]}` API structures
- No beta headers (`anthropic-beta: skills-2025-10-02`)
- No Files API code (`client.beta.files.download`, `client.beta.files.retrieve_metadata`)
- No `anthropic` package imports or usage examples
- No Claude model strings (`claude-sonnet-4-5-20250929`, etc.)

### Platform-Specific Features

- No Cowork references or Desktop plugin installation flows
- No Claude.ai Settings UI instructions as primary guidance
- No Claude Code CLI-specific commands as the only path
- No Jupyter notebook structure or notebook-based tutorials
- No "Claude Desktop" or "Claude.ai" as the assumed environment

### Document Format Skills (xlsx, pptx, pdf, docx)

- These are Anthropic's built-in skills, not part of this collection
- Do not add document creation/manipulation skills as core features
- Do not reference Excel, PowerPoint, PDF, Word generation as key capabilities
- If document skills are mentioned, it should be as examples of what skills CAN do, not what THIS repo provides

### Vendor-Locked Connector Tables

- No per-role connector lists (e.g., "Sales: Slack, HubSpot, Close, Clay...")
- No `.mcp.json` as the only connector pattern
- Connectors are mentioned as a concept but kept platform-agnostic

### Financial Sample Data

- No `financial_statements.csv`, `portfolio_holdings.json`, `budget_template.csv`, `quarterly_metrics.json`
- The repo is general-purpose, not finance-focused
- Use domain-neutral examples when possible

### Branding and Framing

- No "Claude Skills Cookbook" naming
- No "Claude Capabilities" naming
- No "Anthropic is open-sourcing..." framing
- No Anthropic acknowledgments sections
- No emojis in headers (keep it professional)
- Do not position this as an Anthropic product or extension

## Writing Style

- Use "AI agent" or "agent" — not "Claude" as the default subject
- Use simple, clear English — the audience includes non-native speakers
- Keep it practical and direct — no hype, no filler
- When referencing platforms, list them as options (e.g., "works across Claude, OpenAI, and other Agent Skills-compatible platforms")
- Anthropic docs can be linked as **references**, not as primary documentation

## Architecture Principles

- Every skill follows the `SKILL.md` standard with YAML frontmatter
- Skills must be self-contained and portable
- Progressive disclosure: frontmatter → SKILL.md body → supporting files
- Skills should work independently — no hard dependencies on other skills
- Keep skills modular: one skill = one job

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
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

## When Adding New Skills

1. Follow the `SKILL.md` frontmatter standard (name + description required)
2. Keep descriptions under 200 characters — they determine auto-activation
3. Use the menu/modular pattern for multi-workflow skills
4. Include examples of expected output in the skill
5. Test with multiple prompt variations before committing
6. Do not hardcode API keys, passwords, or secrets in skill files
7. Place the skill in the correct category folder (`roles/` or `domain/`)
