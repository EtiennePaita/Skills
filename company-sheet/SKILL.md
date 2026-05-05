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
3. **Template**: Always follow the structure defined in `assets/template.md`. Read it before creating the page.
4. **Links**: Clickable links in Notion REQUIRE the `link` property inside the `text` object. Plain text URLs are NOT clickable.
5. **Language**: Create the page in the same language the user asked in.

---

## Step 1 — Read the Template

Before doing anything, read `assets/template.md` to understand the full page structure. This file is the authoritative reference for what sections to include and in what order.

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

### 4a. Create the page with `post-page`

Set the following when creating the page:

- **`parent`**: `{ "page_id": "<target_parent_id>" }`
- **`properties.title`**: Company name
- **`icon`**: Use the company logo via Clearbit:
  ```json
  {
    "type": "external",
    "external": { "url": "https://logo.clearbit.com/<company-domain.com>" }
  }
  ```
  If Clearbit fails (logo not found), fall back to a relevant emoji.

### 4b. Populate the page with `patch-block-children`

Build all blocks in a **single call** (or at most 2 calls if content is large). Follow this exact block sequence:

---

### 📐 Block Structure Reference

#### SECTION 1 — Dashboard (Column List)

Use a `column_list` with **3 columns** side by side. Each column contains a single `callout`:

```json
{
  "type": "column_list",
  "column_list": {
    "children": [
      {
        "type": "column",
        "column": {
          "children": [{
            "type": "callout",
            "callout": {
              "icon": { "emoji": "💰" },
              "color": "blue_background",
              "rich_text": [{ "type": "text", "text": { "content": "Revenue (FY20XX)\n$X Billion" } }]
            }
          }]
        }
      },
      {
        "type": "column",
        "column": {
          "children": [{
            "type": "callout",
            "callout": {
              "icon": { "emoji": "🏢" },
              "color": "green_background",
              "rich_text": [{ "type": "text", "text": { "content": "Category\nFintech · Payments" } }]
            }
          }]
        }
      },
      {
        "type": "column",
        "column": {
          "children": [{
            "type": "callout",
            "callout": {
              "icon": { "emoji": "🏆" },
              "color": "yellow_background",
              "rich_text": [{ "type": "text", "text": { "content": "Market Position\n#1 in X" } }]
            }
          }]
        }
      }
    ]
  }
}
```

#### SECTION 2 — About

```
heading_1: "About"
callout (gray_background, icon ℹ️): Company résumé (2–3 sentences)
divider
heading_2: "Key Metrics"
bulleted_list_item: "📅 Founded: YEAR"
bulleted_list_item: "👥 Headcount: X employees"
bulleted_list_item: "📍 Headquarters: City, Country"
divider
heading_2: "Products & Services"
bulleted_list_item: Product 1
bulleted_list_item: Product 2
...
```

#### SECTION 3 — Key Clients

```
heading_2: "Key Clients"
bulleted_list_item: Client + short description
... (5–10 items)
```

#### SECTION 4 — Employee Benefits

```
heading_2: "Employee Benefits"
bulleted_list_item: Benefit 1
bulleted_list_item: Benefit 2
...
```

#### SECTION 5 — Competitors

```
heading_2: "Competitors"
bulleted_list_item: Competitor + niche note
...
```

#### SECTION 6 — Glassdoor

```
heading_2: "Glassdoor Insights"
callout (red_background, icon ⭐): "Rating: X.X/5 — based on N reviews"
quote: "Review text" — Current/Former Employee
quote: "Review text" — Current/Former Employee
```

#### SECTION 7 — Links

```
heading_2: "Links"
paragraph with CLICKABLE link:
  {
    "type": "text",
    "text": {
      "content": "Careers Page",
      "link": { "url": "https://company.com/careers" }
    }
  }
```

> **Why this matters**: Notion only renders hyperlinks when `text.link.url` is set. A plain string like `"[text](url)"` is NOT rendered as a clickable link by the API — it appears as raw text.

---

## Step 5 — Confirm to the User

After the page is created, share the Notion page URL with the user and briefly confirm what was included.

---

## Assets Reference

- `assets/template.md` — Visual template showing the full page layout. **Read this first.**
