# 🤖 AI Agent Skills

A curated collection of **Skills** for Claude AI agents — each one extending Claude's capabilities with a specific, well-defined workflow backed by real tools and integrations.

Skills follow the [Anthropic Skills format](https://github.com/anthropics/anthropic-skills), making them portable and reusable across Claude environments (Claude.ai, Claude Code, etc.).

---

## 📦 Skills

### [`company-sheet`](./company-sheet/)

> Create premium company profile pages in Notion from a single prompt.

The `company-sheet` skill automates the research and creation of detailed, beautifully structured company "cheat sheets" directly in your Notion workspace. It uses web search to gather real data and the Notion MCP to build the page — no manual copy-pasting.

**What it does:**
- 🔍 Researches revenue, market position, key clients, competitors, Glassdoor reviews, and employee benefits
- 📄 Creates a structured Notion page following a premium template
- 🎨 Uses advanced Notion blocks: column lists, callouts, dividers, quotes, and clickable links
- 🌍 Supports any language (creates the page in the language of your request)

**Notion page structure:**
| Section | Notion Block |
|---|---|
| Dashboard | 3-column layout (Revenue · Category · Market Position) |
| About | Callout (résumé) + Key Metrics + Products |
| Key Clients | Bulleted list |
| Employee Benefits | Bulleted list |
| Competitors | Bulleted list with context |
| Glassdoor | Star callout + review quotes |
| Links | Clickable hyperlinks |

**Requires:** `notion-mcp-server` configured in your Claude environment.

**Trigger examples:**
- *"Create a company sheet for Stripe in Notion"*
- *"Fais une fiche entreprise sur Withings"*
- *"I need a company overview for Airbnb"*

---

## 🗂️ Repository Structure

```
Skills/
├── company-sheet/           # Company profile Notion pages
│   ├── SKILL.md             # Main skill instructions
│   ├── assets/
│   │   └── template.md      # Notion page layout spec
│   └── evals/
│       └── evals.json       # Test cases
├── company-sheet-workspace/ # Eval results from skill testing
└── README.md
```

---

## 🚀 Getting Started

Skills in this repo are designed to be used with Claude agents that support the Skills format.

1. Point your Claude agent to a skill directory (e.g. `company-sheet/`)
2. Claude will read `SKILL.md` on trigger
3. Ensure any required MCP servers (e.g. `notion-mcp-server`) are configured

---

## 📋 Roadmap

- [ ] `job-tracker` — Track job applications in Notion
- [ ] `competitor-radar` — Weekly competitive intelligence digest
- [ ] `meeting-notes` — Structure meeting notes into Notion pages
- [ ] `person-sheet` — Profile pages for contacts and leads

---

## 🤝 Contributing

Skills are self-contained directories. To add a new one:

1. Create a new folder at the root: `my-skill/`
2. Add a `SKILL.md` with proper YAML frontmatter (`name`, `description`)
3. Add any assets, scripts, or references under subdirectories
4. Update this README

---

*Built with [Claude](https://anthropic.com) · Skills format by [Anthropic](https://github.com/anthropics/anthropic-skills)*
