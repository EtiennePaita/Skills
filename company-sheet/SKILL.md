---
name: company-sheet
description: Use this skill whenever you need to create a detailed company profile or "cheat sheet" in Notion. This skill automates the research and page creation process for any given company, ensuring a standardized, high-quality, premium-looking page. Trigger this skill when the user asks for a company overview, a research sheet, or mentions creating a company page in Notion.
---

# Company Sheet Creator

This skill researches a company and creates a comprehensive, premium-looking profile page in Notion using the official `notion-mcp-server` tools.

---

## ⚠️ Critical Rules

1. **Notion interaction**: Use ONLY `notion-mcp-server` tools to create/update pages. Never use a browser to navigate Notion.
2. **Research**: Use `search_web` and `read_url_content` ONLY for gathering company data.
3. **Template**: Always follow the structure defined in `assets/notion-template.md`. Read it before creating the page.
4. **Links**: Clickable links in Notion REQUIRE the `link` property inside the `text` object. Plain text URLs are NOT clickable.
5. **Language**: Create the page in the same language the user asked in.

---

## Step 1 — Read the Template Index

Before doing anything, read `assets/notion-template.md`. It lists all template
files, the full placeholder reference, the page architecture map, and the
creation checklist. Then open the specific template files as needed.

---

## Step 2 — Research the Company

Search the web for the following. Note everything you find — even partial data is useful.

| Field | What to Find |
|---|---|
| Revenue | Last fiscal year revenue (estimated if private) |
| Category | Industry (e.g. "Fintech", "AI & Semiconductors") |
| Activities | 2–4 activity tags (e.g. "Payments", "SaaS", "Healthcare") |
| Market Position | Rank among competitors (e.g. "#1 in X", "Top 5 in Y") |
| About | 2–3 sentence history and mission summary |
| Key Metrics | Founding year, headcount, headquarters |
| Products & Services | 3–5 key products, tools, or services |
| Key Clients | 5 to 10 notable clients |
| Employee Benefits | Benefits and perks (remote policy, health, equity, etc.) |
| Competitors | 3–5 direct competitors |
| Glassdoor | Overall rating, number of reviews, 2–3 representative quotes |
| Jobs Link | Direct URL to the careers/jobs page |

**Research tips:**
- Official website ("About" / "Investor Relations" pages) for history and products
- LinkedIn for headcount and growth
- Glassdoor.com for rating and review quotes
- Crunchbase, Yahoo Finance, or Macrotrends for revenue
- Google for market rank ("X company market share rank")

---

## Step 3 — Locate the Notion Destination

1. Use `search_by_title` to look for a page named "Companies" or "Company Sheets".
2. If found, use that page as the parent.
3. If not found, ask the user for a parent page ID, or create the page at workspace root.

---

## Step 4 — Create the Notion Page

Follow the template files in order. Each file contains the exact JSON block(s) to send and the placeholders to fill in.

### 4a. Create the page shell

Read `assets/templates/page-metadata.md` → call `post-page` → **save the returned page ID**.

### 4b. Append the KPI callout and tab skeleton

Read `assets/templates/kpi-callout.md` and `assets/templates/tabs-skeleton.md`.
Send **both blocks in a single `patch-block-children` call** on the page ID.

### 4c. Retrieve tab paragraph IDs

Call `get-block-children` on the **`tab` block ID** returned in step 4b.
The 5 results (in order) are the paragraph IDs for each tab:

| Index | Tab label |
|---|---|
| `results[0].id` | A propos |
| `results[1].id` | Produits & Services |
| `results[2].id` | Clients |
| `results[3].id` | Concurrents |
| `results[4].id` | Avis |

### 4d. Populate each tab body

For each tab, read the corresponding template file and call `patch-block-children`
with the matching paragraph ID as `block_id`:

| Template file | Target block ID |
|---|---|
| `assets/templates/tab-a-propos.md` | `results[0].id` |
| `assets/templates/tab-produits-services.md` | `results[1].id` |
| `assets/templates/tab-clients.md` | `results[2].id` |
| `assets/templates/tab-concurrents.md` | `results[3].id` |
| `assets/templates/tab-avis.md` | `results[4].id` |

### ⚠️ Known API Constraints

| Constraint | What to do |
|---|---|
| `child_database` not allowed as tab child | Use `bulleted_list_item` blocks instead |
| `column_list` not allowed inside `callout` | Use inline rich_text with emoji separators |
| `callout.icon` must not be `null` | Always pass an emoji or external icon object |
| Clickable links | Always set `text.link.url` — plain URL strings are NOT clickable |

---

## Step 5 — Confirm to the User

After the page is created, share the Notion page URL with the user and briefly confirm what was included.

---

## Assets Reference

- `assets/notion-template.md` — Index of all template files. **Read this first.**
- `assets/templates/page-metadata.md` — `post-page` payload (icon, cover, title)
- `assets/templates/kpi-callout.md` — KPI banner callout block
- `assets/templates/tabs-skeleton.md` — `tab` container + 5 tab header paragraphs
- `assets/templates/tab-a-propos.md` — "A propos" tab body
- `assets/templates/tab-produits-services.md` — "Produits & Services" tab body
- `assets/templates/tab-clients.md` — "Clients" tab body
- `assets/templates/tab-concurrents.md` — "Concurrents" tab body
- `assets/templates/tab-avis.md` — "Avis" tab body

