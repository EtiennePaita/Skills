# Notion Template — Company Sheet (Index)

This file is the **entry point** for the `company-sheet` skill.
Each section of the Notion page lives in its own file under `templates/`.
Read this index first, then open the specific template files as needed.

---

## 📂 Template Files

| File | API Call | Description |
|---|---|---|
| [`templates/page-metadata.md`](templates/page-metadata.md) | `post-page` | Page title, icon (Hunter.io logo), cover |
| [`templates/kpi-callout.md`](templates/kpi-callout.md) | `patch-block-children` on page | KPI banner (Revenue · Position · Headcount) |
| [`templates/company-categories.md`](templates/company-categories.md) | `patch-block-children` on page | 1-3 Categories with icons in columns |
| [`templates/tabs-skeleton.md`](templates/tabs-skeleton.md) | `patch-block-children` on page | `tab` block + 5 tab header paragraphs |
| [`templates/tab-a-propos.md`](templates/tab-a-propos.md) | `patch-block-children` on tab paragraph | Bookmark, résumé, benefits, HQ, careers link |
| [`templates/tab-produits-services.md`](templates/tab-produits-services.md) | `patch-block-children` on tab paragraph | Bulleted product/service list |
| [`templates/tab-clients.md`](templates/tab-clients.md) | `patch-block-children` on tab paragraph | Emoji-prefixed client segments |
| [`templates/tab-concurrents.md`](templates/tab-concurrents.md) | `patch-block-children` on tab paragraph | Bulleted competitor list |
| [`templates/tab-avis.md`](templates/tab-avis.md) | `patch-block-children` on tab paragraph | Glassdoor rating callout + 2 quote blocks |

---

## 🗺️ Page Architecture

```
PAGE: {{COMPANY_NAME}}
│   icon : https://logos.hunter.io/{{COMPANY_DOMAIN}}
│   cover: gradients_11.jpg
│
├── [callout]  ← kpi-callout.md
│       "💵 CA : {{REVENUE}}  🏆 {{MARKET_POSITION}}  👥 {{HEADCOUNT}}"
│
├── [columns]  ← company-categories.md
│       "{{CATEGORY_1}} | {{CATEGORY_2}} | {{CATEGORY_3}}"
│
└── [tab]  ← tabs-skeleton.md
    ├── paragraph "A propos"          ← tab-a-propos.md
    ├── paragraph "Produits & Services" ← tab-produits-services.md
    ├── paragraph "Clients"           ← tab-clients.md
    ├── paragraph "Concurrents"       ← tab-concurrents.md
    └── paragraph "Avis"              ← tab-avis.md
```

---

## 🔑 All Placeholders

| Placeholder | Template File | Description |
|---|---|---|
| `{{PARENT_PAGE_ID}}` | page-metadata | Notion ID of the parent page |
| `{{COMPANY_NAME}}` | page-metadata, tab-a-propos | Company display name |
| `{{COMPANY_DOMAIN}}` | page-metadata | Domain for Hunter.io logo (e.g. `withings.com`) |
| `{{REVENUE}}` | kpi-callout | Last known revenue (e.g. `~400 M€`) |
| `{{MARKET_POSITION}}` | kpi-callout | Market rank or label (e.g. `Leader`, `#17 France`) |
| `{{HEADCOUNT}}` | kpi-callout | Employee count (e.g. `+400`, `~300`) |
| `{{CATEGORY_1..3}}` | company-categories | Company activity categories (max 14 chars) |
| `{{CATEGORY_1..3_ICON}}` | company-categories | Notion native icon names (e.g., `bank`, `heart`) |
| `{{CATEGORY_1..3_COLOR}}` | company-categories | Notion native icon colors (e.g., `blue`, `red`) |
| `{{COMPANY_WEBSITE_URL}}` | tab-a-propos | Official homepage URL |
| `{{COMPANY_RESUME}}` | tab-a-propos | 2–3 sentence history + mission |
| `{{BENEFIT_1..4}}` | tab-a-propos | Employee benefit bullet points |
| `{{HEADQUARTERS}}` | tab-a-propos | HQ city, country (+ satellite offices) |
| `{{CAREERS_URL}}` | tab-a-propos | Direct URL to careers/jobs page |
| `{{PRODUCT_1..5}}` | tab-produits-services | `Name — short description` format |
| `{{CLIENT_1..5}}` | tab-clients | `EMOJI  Description` format |
| `{{COMPETITOR_1..5}}` | tab-concurrents | `Name — what they compete on` format |
| `{{GLASSDOOR_RATING}}` | tab-avis | Numeric score (e.g. `~3,5`) |
| `{{GLASSDOOR_SUMMARY}}` | tab-avis | One-line culture snapshot |
| `{{GLASSDOOR_REVIEW_1}}` | tab-avis | Full quote + attribution (current employee) |
| `{{GLASSDOOR_REVIEW_2}}` | tab-avis | Full quote + attribution (former employee) |

---

## 📋 Creation Checklist

- [ ] Research all `{{PLACEHOLDER}}` values (see `SKILL.md` Step 2)
- [ ] Read `templates/page-metadata.md` → call `post-page` → save returned page ID
- [ ] Read `templates/kpi-callout.md` + `templates/company-categories.md` + `templates/tabs-skeleton.md` → call `patch-block-children` on the page
- [ ] Call `get-block-children` on the `tab` block → collect the 5 paragraph IDs
- [ ] Read `templates/tab-a-propos.md` → call `patch-block-children` on paragraph #1
- [ ] Read `templates/tab-produits-services.md` → call `patch-block-children` on paragraph #2
- [ ] Read `templates/tab-clients.md` → call `patch-block-children` on paragraph #3
- [ ] Read `templates/tab-concurrents.md` → call `patch-block-children` on paragraph #4
- [ ] Read `templates/tab-avis.md` → call `patch-block-children` on paragraph #5
- [ ] Verify all clickable links use `text.link.url` (not plain URL strings)
- [ ] Share the final Notion page URL with the user

---

## ⚠️ Known API Constraints

| Constraint | Detail |
|---|---|
| `child_database` not allowed | Cannot be added as a child of a `paragraph` or inside a `tab` via REST API. Use `bulleted_list_item` instead. |
| `column_list` not allowed in `callout` | Use inline rich_text with emoji separators for KPI data. |
| `callout.icon` must not be `null` | Always provide an emoji or external icon object — never `null`. |
| Tab body = children of paragraph | Tab content is appended to the *paragraph* block (the tab header), not the `tab` block itself. |
