# AI Agent Skills

An agnostic collection of AI Agent Skills — reusable expertise packages that make AI agents better at specialized tasks across any platform.

## What are Skills?

Skills are organized packages of instructions, executable code, and resources that give AI agents specialized capabilities. Think of them as expertise modules that agents can discover and load dynamically to:

- Follow domain-specific workflows and best practices
- Create professional documents and reports
- Perform complex data analysis and visualization
- Apply company-specific branding and standards
- Automate business processes with real domain knowledge

Skills follow the open [Agent Skills standard](https://agentskills.io), making them portable across platforms and tools — not locked to any single vendor.

## How Skills Work

Every skill follows the same core structure:

```
skill-name/
├── SKILL.md              # Required: metadata + instructions
├── scripts/              # Optional: executable code (Python, JS, Shell)
│   └── processor.py
├── templates/            # Optional: output templates
│   └── template.xlsx
├── references/           # Optional: documentation, guidelines
│   └── REFERENCE.md
├── examples/             # Optional: sample inputs/outputs
│   └── sample.md
└── resources/            # Optional: assets, data files
    └── logo.png
```

### The SKILL.md file

The only required file. It starts with YAML frontmatter (metadata) followed by markdown instructions:

```yaml
---
name: my-skill
description: >
  Clear description of what this skill does and when an agent
  should use it. This is the most critical part — it determines
  when the skill gets activated. (max 200 chars)
---

# My Skill

## When to use this skill
Explain the triggers and conditions.

## Instructions
Step-by-step workflow the agent should follow.

## Examples
Show what good output looks like.

## Guidelines
Constraints, edge cases, quality standards.
```

**The `name` and `description` are the only parts that influence auto-activation.** Agents read these to decide whether to load the skill. Everything below the frontmatter is the actual knowledge and instructions.

### Progressive Disclosure

Skills use a layered loading approach to keep things efficient:

1. **Frontmatter** — Agent scans name + description to decide if the skill is relevant
2. **SKILL.md body** — Full instructions load only when the skill is activated
3. **Supporting files** — Scripts, references, and templates load only when needed during execution

This means you can build deep, detailed skills without bloating every conversation.

## Skill Categories

### Role-Based Packs

Skills organized by job function — bundle the workflows, terminology, and best practices for a specific role.

| Pack                   | What it covers                                                           |
| ---------------------- | ------------------------------------------------------------------------ |
| **productivity**       | Task management, daily workflows, meeting prep, personal context         |
| **sales**              | Prospect research, call prep, pipeline review, outreach, battlecards     |
| **customer-support**   | Ticket triage, response drafting, escalation, knowledge base creation    |
| **product-management** | Specs, roadmaps, user research synthesis, stakeholder updates            |
| **marketing**          | Content drafting, campaign planning, brand voice, competitor briefs      |
| **legal**              | Contract review, NDA triage, compliance, risk assessment                 |
| **finance**            | Journal entries, reconciliation, financial statements, variance analysis |
| **data**               | SQL generation, statistical analysis, dashboards, data validation        |

### Domain Skills

Skills encoding expertise for specific fields — financial analysis, code review, brand guidelines, data pipelines, and more.

## Platform Compatibility

Skills are portable by design. The same `SKILL.md` works across:

| Platform         | How skills are loaded                                  |
| ---------------- | ------------------------------------------------------ |
| **Claude.ai**    | Upload as ZIP via Settings > Capabilities > Skills     |
| **Claude Code**  | Place in `.claude/skills/` directory (auto-discovered) |
| **Claude API**   | Upload via `/v1/skills` endpoint                       |
| **Other agents** | Any platform supporting the Agent Skills standard      |

### Claude Code discovery paths

```
~/.config/claude/skills/    # Personal (available in all projects)
.claude/skills/             # Project-level (committed to version control)
packages/*/. claude/skills/  # Monorepo subdirectory skills
```

Priority: enterprise > personal > project.

### Connectors

Skills can be paired with tool connectors (MCP servers, API integrations, etc.) to give agents access to external services — CRMs, project trackers, data warehouses, design tools. Connector configuration is platform-dependent, but the skills themselves remain portable.

## Building Your Own

### 1. Define the problem

Be specific. "Extract financial data from PDFs and format as CSV" beats "help with finance stuff." Ask yourself:

- What specific task does this skill handle?
- What should trigger it?
- What does good output look like?
- What are the edge cases?

### 2. Write the SKILL.md

Start with a strong description — it's the most important part. The description determines when an agent decides to activate your skill.

```yaml
---
name: invoice-generator
description: >
  Generate professional invoices from line items or timesheets.
  Use when user mentions invoices, billing, or payment documents.
---
```

### 3. Keep it modular

If your skill covers multiple workflows, use a menu approach — describe what's available in SKILL.md and reference separate files for each path:

```markdown
## Available workflows

- **Standard invoice** → see [templates/standard.md](templates/standard.md)
- **Recurring billing** → see [templates/recurring.md](templates/recurring.md)
- **Credit note** → see [templates/credit-note.md](templates/credit-note.md)
```

The agent reads only the relevant file, not everything.

### 4. Add executable code (optional)

Skills can bundle scripts that the agent runs during execution:

```
my-skill/
├── SKILL.md
└── scripts/
    ├── analyze.py
    └── validate.sh
```

Reference them from your SKILL.md so the agent knows when to use them.

### 5. Test and iterate

Test with different prompts and edge cases. Common issues:

- Description too generic → skill activates when it shouldn't
- Description too narrow → skill misses relevant requests
- Instructions too vague → inconsistent output quality
- Too much content loaded at once → slow, token-heavy execution

## Making Skills Your Own

The skills in this collection are starting points. They become much more useful when you customize them:

- **Add company context** — Drop your terminology, org structure, and processes into skill files so the agent understands your world.
- **Adjust workflows** — Modify instructions to match how your team actually does things, not how a textbook says to.
- **Swap connectors** — Point tool configurations at your specific stack.
- **Combine skills** — Multiple skills can activate together for complex tasks. Design them to work well alongside each other.

## Common Use Cases

**Reporting & Analysis** — Automated quarterly reports, budget variance analysis, KPI dashboards, portfolio reviews.

**Document Automation** — Branded presentations, cross-format conversion (CSV → Excel → PowerPoint → PDF), template-based generation.

**Workflow Standardization** — Code review processes, onboarding procedures, compliance checklists, content approval flows.

**Domain Expertise** — Financial modeling, legal document review, competitive analysis, data validation frameworks.

## Project Structure

```
ai-agent-skills/
├── skills/                       # Skill collection
│   ├── roles/                    # Role-based skill packs
│   │   ├── customer-support/
│   │   ├── data/
│   │   ├── finance/
│   │   ├── legal/
│   │   ├── marketing/
│   │   ├── product-management/
│   │   ├── productivity/
│   │   └── sales/
│   └── domain/                   # Domain-specific skills
│       ├── brand-guidelines/
│       ├── code-review/
│       └── ...
├── templates/                    # Starter templates
│   └── skill-template/
│       └── SKILL.md
├── docs/                         # Documentation
├── LICENSE
└── README.md
```

## Resources

- [Agent Skills Open Standard](https://agentskills.io) — Cross-platform specification
- [Anthropic Skills Repository](https://github.com/anthropics/skills) — Reference implementations
- [Skills Best Practices](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/best-practices) — Authoring guidelines
- [Equipping Agents with Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) — Engineering deep dive
- [Skills Explained](https://claude.com/blog/skills-explained) — How skills compare to prompts, projects, MCP, and subagents

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
