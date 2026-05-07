# Notion Template — Company Sheet

This template is used by the `company-sheet` skill to create new Notion pages.
It faithfully mirrors the Withings page structure and uses `{{PLACEHOLDER}}` tokens
that must be replaced at generation time. Sub-templates are provided for every
nested section to keep each `patch-block-children` call focused and readable.

---

## 📐 Page-level Metadata (used in `post-page`)

```json
{
  "parent": { "page_id": "{{PARENT_PAGE_ID}}" },
  "icon": {
    "type": "external",
    "external": { "url": "https://logos.hunter.io/{{COMPANY_DOMAIN}}" }
  },
  "cover": {
    "type": "external",
    "external": { "url": "https://www.notion.so/images/page-cover/gradients_11.jpg" }
  },
  "properties": {
    "title": {
      "title": [{ "type": "text", "text": { "content": "{{COMPANY_NAME}}" } }]
    }
  }
}
```

> **Fallback**: If Hunter logo fails (404), use an emoji icon instead:
> `{ "type": "emoji", "emoji": "🏢" }`

---

## 📦 Root Blocks (first `patch-block-children` call on the page)

Append these 3 blocks directly to the page. The `tab` block acts as a
navigation container whose children become the visible "tabs" (sub-sections).

```json
[
  "{{> block-kpi-columns}}",
  "{{> block-kpi-callout}}",
  "{{> block-tabs}}"
]
```

---

## Sub-template: `block-kpi-callout`

A top-level callout wrapper that holds a **3-column KPI strip** (Revenue,
Market Position, Headcount). This is rendered as the highlighted banner at the
top of the page, just below the action buttons.

```json
{
  "type": "callout",
  "callout": {
    "rich_text": [],
    "icon": null,
    "color": "default_background",
    "children": [
      {
        "type": "column_list",
        "column_list": {
          "children": [
            {
              "type": "column",
              "column": {
                "children": [
                  {
                    "type": "equation",
                    "equation": {
                      "expression": "\\huge\\texttt{\\textsf{💵}} \\\\ \\LARGE\\textbf{\\textsf{{{REVENUE}}}}"
                    }
                  }
                ]
              }
            },
            {
              "type": "column",
              "column": {
                "children": [
                  {
                    "type": "equation",
                    "equation": {
                      "expression": "\\huge\\texttt{\\textsf{🏆}} \\\\ \\LARGE\\textbf{\\textsf{{{MARKET_POSITION}}}}"
                    }
                  }
                ]
              }
            },
            {
              "type": "column",
              "column": {
                "children": [
                  {
                    "type": "equation",
                    "equation": {
                      "expression": "\\huge\\texttt{\\textsf{👥}} \\\\ \\LARGE\\textbf{\\textsf{{{HEADCOUNT}}}}"
                    }
                  }
                ]
              }
            }
          ]
        }
      }
    ]
  }
}
```

**Placeholders:**
| Token | Example |
|---|---|
| `{{REVENUE}}` | `~400 M€` |
| `{{MARKET_POSITION}}` | `Leader` |
| `{{HEADCOUNT}}` | `+400` |

---

## Sub-template: `block-tabs`

A `tab` block whose direct children act as the tab navigation labels.
Each child is a `paragraph` with an icon and a text label; its own children
form the tab body. Append tab bodies with a **second** `patch-block-children`
call targeting each paragraph's block ID.

```json
{
  "type": "tab",
  "tab": {
    "children": [
      "{{> tab-a-propos}}",
      "{{> tab-produits-services}}",
      "{{> tab-clients}}",
      "{{> tab-concurrents}}",
      "{{> tab-avis}}"
    ]
  }
}
```

> **Note**: The Notion API maps the `tab` type. Each direct child of `tab` is
> a `paragraph` rendered as a clickable tab header. The content lives as
> *children of that paragraph*.

---

## Sub-template: `tab-a-propos`

Tab label + full body for **"A propos"**.

```json
{
  "type": "paragraph",
  "paragraph": {
    "rich_text": [{ "type": "text", "text": { "content": "A propos" } }],
    "icon": { "type": "icon", "icon": { "name": "info-alternate", "color": "gray" } },
    "color": "default",
    "children": [
      {
        "type": "bookmark",
        "bookmark": {
          "url": "{{COMPANY_WEBSITE_URL}}",
          "caption": []
        }
      },
      {
        "type": "paragraph",
        "paragraph": { "rich_text": [], "color": "default" }
      },
      {
        "type": "callout",
        "callout": {
          "rich_text": [
            {
              "type": "text",
              "text": { "content": "{{COMPANY_RESUME}}" },
              "annotations": {
                "bold": false, "italic": false, "strikethrough": false,
                "underline": false, "code": false, "color": "default"
              }
            }
          ],
          "icon": null,
          "color": "default_background"
        }
      },
      {
        "type": "heading_3",
        "heading_3": {
          "rich_text": [{ "type": "text", "text": { "content": "💰 Avantages Salariés" } }],
          "is_toggleable": false,
          "color": "default"
        }
      },
      {
        "type": "bulleted_list_item",
        "bulleted_list_item": {
          "rich_text": [{ "type": "text", "text": { "content": "{{BENEFIT_1}}" } }],
          "color": "default"
        }
      },
      {
        "type": "bulleted_list_item",
        "bulleted_list_item": {
          "rich_text": [{ "type": "text", "text": { "content": "{{BENEFIT_2}}" } }],
          "color": "default"
        }
      },
      {
        "type": "bulleted_list_item",
        "bulleted_list_item": {
          "rich_text": [{ "type": "text", "text": { "content": "{{BENEFIT_3}}" } }],
          "color": "default"
        }
      },
      {
        "type": "bulleted_list_item",
        "bulleted_list_item": {
          "rich_text": [{ "type": "text", "text": { "content": "{{BENEFIT_4}}" } }],
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": { "rich_text": [], "color": "default" }
      },
      {
        "type": "heading_3",
        "heading_3": {
          "rich_text": [{ "type": "text", "text": { "content": "📍 Siège social" } }],
          "is_toggleable": false,
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [
            { "type": "text", "text": { "content": "{{HEADQUARTERS}}" } }
          ],
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": { "rich_text": [], "color": "default" }
      },
      {
        "type": "heading_3",
        "heading_3": {
          "rich_text": [{ "type": "text", "text": { "content": "Liens" } }],
          "is_toggleable": false,
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [
            {
              "type": "text",
              "text": {
                "content": "💼 Offres d'emploi {{COMPANY_NAME}}",
                "link": { "url": "{{CAREERS_URL}}" }
              },
              "annotations": {
                "bold": false, "italic": false, "strikethrough": false,
                "underline": false, "code": false, "color": "default"
              }
            }
          ],
          "color": "default"
        }
      }
    ]
  }
}
```

**Placeholders:**
| Token | Description | Example |
|---|---|---|
| `{{COMPANY_WEBSITE_URL}}` | Official website URL | `https://www.withings.com` |
| `{{COMPANY_RESUME}}` | 2–3 sentence company history & mission | `Fondée en 2008…` |
| `{{BENEFIT_1..4}}` | Employee benefits (add more as needed) | `Politique de travail hybride` |
| `{{HEADQUARTERS}}` | City, Country (+ satellite offices) | `Issy-les-Moulineaux, France (+ Boston, Hong Kong)` |
| `{{CAREERS_URL}}` | Direct link to careers/jobs page | `https://www.withings.com/eu/fr/work-with-us` |

---

## Sub-template: `tab-produits-services`

Tab label for **"Produits & Services"**. The body contains a `child_database`
created separately via `create-a-data-source`, then referenced by ID.

```json
{
  "type": "paragraph",
  "paragraph": {
    "rich_text": [{ "type": "text", "text": { "content": "Produits & Services" } }],
    "icon": { "type": "icon", "icon": { "name": "shopping-bag", "color": "gray" } },
    "color": "default",
    "children": [
      {
        "type": "child_database",
        "child_database": { "title": "Produits & Services" }
      },
      {
        "type": "paragraph",
        "paragraph": { "rich_text": [], "color": "default" }
      }
    ]
  }
}
```

> **How to populate the database**: After creating the page, call
> `query-data-source` on the returned `child_database` block ID, then use
> `post-page` with `parent.database_id` to insert each product/service as a row.

**Products database schema (recommended columns):**
| Property | Type | Description |
|---|---|---|
| `Nom` | `title` | Product / service name |
| `Catégorie` | `select` | Hardware / Software / Service / Platform |
| `Description` | `rich_text` | Short description |
| `URL` | `url` | Product page link |

---

## Sub-template: `tab-clients`

Tab label for **"Clients"**. Contains emoji-prefixed paragraphs for each client
segment, a spacer, and a `child_database` for tracked partners/clients.

```json
{
  "type": "paragraph",
  "paragraph": {
    "rich_text": [{ "type": "text", "text": { "content": "Clients" } }],
    "icon": { "type": "icon", "icon": { "name": "groups", "color": "gray" } },
    "color": "default",
    "children": [
      {
        "type": "heading_3",
        "heading_3": {
          "rich_text": [{ "type": "text", "text": { "content": "Clients" } }],
          "is_toggleable": false,
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [{ "type": "text", "text": { "content": "{{CLIENT_1}}" } }],
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [{ "type": "text", "text": { "content": "{{CLIENT_2}}" } }],
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [{ "type": "text", "text": { "content": "{{CLIENT_3}}" } }],
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [{ "type": "text", "text": { "content": "{{CLIENT_4}}" } }],
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [{ "type": "text", "text": { "content": "{{CLIENT_5}}" } }],
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": { "rich_text": [], "color": "default" }
      },
      {
        "type": "child_database",
        "child_database": { "title": "Partenaires" }
      },
      {
        "type": "paragraph",
        "paragraph": { "rich_text": [], "color": "default" }
      }
    ]
  }
}
```

**Placeholders:**
| Token | Format | Example |
|---|---|---|
| `{{CLIENT_1}}` | `EMOJI  Description` | `👨  Particuliers soucieux de leur santé (B2C — principal marché)` |
| `{{CLIENT_2..5}}` | Same pattern | `🏥  Hôpitaux et cliniques (suivi à distance des patients chroniques)` |

> Start each client entry with a relevant emoji followed by two spaces for
> alignment (e.g. `👨`, `🏥`, `🏩`, `🥼`, `🏪`).

---

## Sub-template: `tab-concurrents`

Tab label for **"Concurrents"**. Contains a single `child_database` block.

```json
{
  "type": "paragraph",
  "paragraph": {
    "rich_text": [{ "type": "text", "text": { "content": "Concurrents" } }],
    "icon": { "type": "icon", "icon": { "name": "city", "color": "gray" } },
    "color": "default",
    "children": [
      {
        "type": "child_database",
        "child_database": { "title": "Concurrents" }
      },
      {
        "type": "paragraph",
        "paragraph": { "rich_text": [], "color": "default" }
      }
    ]
  }
}
```

> **Competitors database schema (recommended columns):**
> | Property | Type | Description |
> |---|---|---|
> | `Nom` | `title` | Competitor name |
> | `Niche` | `rich_text` | What they specifically compete on |
> | `URL` | `url` | Competitor website |
> | `Taille` | `select` | Startup / PME / Grand groupe |

---

## Sub-template: `tab-avis`

Tab label for **"Avis"** (Glassdoor / reviews). Contains a `callout` with the
overall rating and two `quote` blocks for representative employee reviews.

```json
{
  "type": "paragraph",
  "paragraph": {
    "rich_text": [{ "type": "text", "text": { "content": "Avis" } }],
    "icon": { "type": "icon", "icon": { "name": "star-half", "color": "yellow" } },
    "color": "default",
    "children": [
      {
        "type": "paragraph",
        "paragraph": { "rich_text": [], "color": "default" }
      },
      {
        "type": "callout",
        "callout": {
          "rich_text": [
            {
              "type": "text",
              "text": { "content": "Note globale : " },
              "annotations": { "bold": true, "color": "default" }
            },
            {
              "type": "text",
              "text": { "content": " " },
              "annotations": { "bold": true, "color": "yellow" }
            },
            {
              "type": "text",
              "text": { "content": "{{GLASSDOOR_RATING}} / 5 " },
              "annotations": { "bold": false, "color": "yellow" }
            },
            {
              "type": "text",
              "text": { "content": "\n{{GLASSDOOR_SUMMARY}}" },
              "annotations": { "bold": false, "color": "default" }
            }
          ],
          "icon": { "type": "emoji", "emoji": "⭐" },
          "color": "default_background"
        }
      },
      {
        "type": "paragraph",
        "paragraph": { "rich_text": [], "color": "default" }
      },
      {
        "type": "quote",
        "quote": {
          "rich_text": [
            {
              "type": "text",
              "text": { "content": "{{GLASSDOOR_REVIEW_1}}" },
              "annotations": { "color": "default" }
            }
          ],
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": { "rich_text": [], "color": "default" }
      },
      {
        "type": "quote",
        "quote": {
          "rich_text": [
            {
              "type": "text",
              "text": { "content": "{{GLASSDOOR_REVIEW_2}}" },
              "annotations": { "color": "default" }
            }
          ],
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": { "rich_text": [], "color": "default" }
      }
    ]
  }
}
```

**Placeholders:**
| Token | Description | Example |
|---|---|---|
| `{{GLASSDOOR_RATING}}` | Score as text | `~3,5` |
| `{{GLASSDOOR_SUMMARY}}` | One-line culture summary | `PME reconnue pour ses produits innovants…` |
| `{{GLASSDOOR_REVIEW_1}}` | Full quote + attribution | `"Super environnement…" — Employé(e) actuel(le)` |
| `{{GLASSDOOR_REVIEW_2}}` | Full quote + attribution | `"Charge de travail élevée…" — Ancien(ne) employé(e)` |

---

## 🗺️ Full Page Architecture (Visual Map)

```
PAGE: {{COMPANY_NAME}}
│   icon: clearbit logo  /  emoji fallback
│   cover: gradients_11.jpg
│
├── [column_list]  ← 3 columns with action buttons (unsupported by API, skip)
│
├── [callout]  ← KPI banner (default_background)
│   └── [column_list]
│       ├── [column]  →  equation: 💵  {{REVENUE}}
│       ├── [column]  →  equation: 🏆  {{MARKET_POSITION}}
│       └── [column]  →  equation: 👥  {{HEADCOUNT}}
│
└── [tab]  ← navigation tabs container
    ├── [paragraph "A propos" | icon: info-alternate gray]
    │   ├── bookmark: {{COMPANY_WEBSITE_URL}}
    │   ├── paragraph (spacer)
    │   ├── callout: {{COMPANY_RESUME}}
    │   ├── heading_3: "💰 Avantages Salariés"
    │   ├── bulleted_list_item: {{BENEFIT_1}}
    │   ├── bulleted_list_item: {{BENEFIT_2}}
    │   ├── bulleted_list_item: {{BENEFIT_3}}
    │   ├── bulleted_list_item: {{BENEFIT_4}}
    │   ├── paragraph (spacer)
    │   ├── heading_3: "📍 Siège social"
    │   ├── paragraph: {{HEADQUARTERS}}
    │   ├── paragraph (spacer)
    │   ├── heading_3: "Liens"
    │   └── paragraph: [💼 Offres d'emploi {{COMPANY_NAME}}]({{CAREERS_URL}})
    │
    ├── [paragraph "Produits & Services" | icon: shopping-bag gray]
    │   ├── child_database: "Produits & Services"
    │   └── paragraph (spacer)
    │
    ├── [paragraph "Clients" | icon: groups gray]
    │   ├── heading_3: "Clients"
    │   ├── paragraph: {{CLIENT_1}}
    │   ├── paragraph: {{CLIENT_2}}
    │   ├── paragraph: {{CLIENT_3}}
    │   ├── paragraph: {{CLIENT_4}}
    │   ├── paragraph: {{CLIENT_5}}
    │   ├── paragraph (spacer)
    │   ├── child_database: "Partenaires"
    │   └── paragraph (spacer)
    │
    ├── [paragraph "Concurrents" | icon: city gray]
    │   ├── child_database: "Concurrents"
    │   └── paragraph (spacer)
    │
    └── [paragraph "Avis" | icon: star-half yellow]
        ├── paragraph (spacer)
        ├── callout ⭐: "Note globale : {{GLASSDOOR_RATING}} / 5  \n{{GLASSDOOR_SUMMARY}}"
        ├── paragraph (spacer)
        ├── quote: {{GLASSDOOR_REVIEW_1}}
        ├── paragraph (spacer)
        ├── quote: {{GLASSDOOR_REVIEW_2}}
        └── paragraph (spacer)
```

---

## 🔑 All Placeholders Reference

| Placeholder | Section | Description |
|---|---|---|
| `{{PARENT_PAGE_ID}}` | Page metadata | Notion ID of the parent page |
| `{{COMPANY_NAME}}` | Page metadata | Company name (also used in links) |
| `{{COMPANY_DOMAIN}}` | Page metadata | e.g. `withings.com` (for Clearbit logo) |
| `{{REVENUE}}` | KPI banner | Last known revenue, e.g. `~400 M€` |
| `{{MARKET_POSITION}}` | KPI banner | e.g. `Leader`, `#2 Europe` |
| `{{HEADCOUNT}}` | KPI banner | e.g. `+400`, `~1 200` |
| `{{COMPANY_WEBSITE_URL}}` | A propos tab | Official homepage URL |
| `{{COMPANY_RESUME}}` | A propos tab | 2–3 sentence history + mission |
| `{{BENEFIT_1..4}}` | A propos tab | Employee benefit bullet points |
| `{{HEADQUARTERS}}` | A propos tab | HQ city, country (+ satellite offices) |
| `{{CAREERS_URL}}` | A propos tab | Direct URL to careers/jobs page |
| `{{CLIENT_1..5}}` | Clients tab | Emoji-prefixed client segment descriptions |
| `{{GLASSDOOR_RATING}}` | Avis tab | Numeric score, e.g. `~3,5` |
| `{{GLASSDOOR_SUMMARY}}` | Avis tab | One-line culture snapshot |
| `{{GLASSDOOR_REVIEW_1}}` | Avis tab | Quote + attribution (current employee) |
| `{{GLASSDOOR_REVIEW_2}}` | Avis tab | Quote + attribution (former employee) |

---

## 📋 Creation Checklist

- [ ] Research all `{{PLACEHOLDER}}` values
- [ ] Create the page via `post-page` (icon + cover + title)
- [ ] Add KPI callout + tab block via `patch-block-children` on the page
- [ ] Add "A propos" tab body via `patch-block-children` on its paragraph block ID
- [ ] Add "Produits & Services" tab body (child_database auto-created)
- [ ] Add "Clients" tab body
- [ ] Add "Concurrents" tab body (child_database auto-created)
- [ ] Add "Avis" tab body
- [ ] Populate `child_database` entries for products, clients/partners, competitors
- [ ] Verify clickable links use `text.link.url`, NOT plain URL strings
- [ ] Share the final page URL with the user
