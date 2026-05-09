# Template: Company Categories

Appended between the KPI callout and the tabs skeleton.
It displays up to 3 columns. Each column contains a callout with the category name (e.g., Health, Bank) and an appropriate Notion native icon.

## Placeholders

| Token | Description | Example |
|---|---|---|
| `{{CATEGORY_1}}` | First category name (max 14 chars) | `Santé` |
| `{{CATEGORY_1_ICON}}` | Notion native icon name for category 1 | `heart` |
| `{{CATEGORY_1_COLOR}}` | Notion native icon color for category 1 | `red` |
| `{{CATEGORY_2}}` | Second category name (max 14 chars) | `Banque` |
| `{{CATEGORY_2_ICON}}` | Notion native icon name for category 2 | `bank` |
| `{{CATEGORY_2_COLOR}}` | Notion native icon color for category 2 | `blue` |
| `{{CATEGORY_3}}` | Third category name (max 14 chars) | `Assurance` |
| `{{CATEGORY_3_ICON}}` | Notion native icon name for category 3 | `shield` |
| `{{CATEGORY_3_COLOR}}` | Notion native icon color for category 3 | `green` |

## JSON Block

```json
{
  "type": "column_list",
  "column_list": {
    "children": [
      {
        "type": "column",
        "column": {},
        "children": [
            {
              "type": "callout",
              "callout": {
                "rich_text": [
                  {
                    "type": "text",
                    "text": {
                      "content": "{{CATEGORY_1}}"
                    },
                    "annotations": {
                      "bold": true
                    }
                  }
                ],
                "icon": {
                  "type": "icon",
                  "icon": {
                    "name": "{{CATEGORY_1_ICON}}",
                    "color": "{{CATEGORY_1_COLOR}}"
                  }
                },
                "color": "default_background"
              }
            }
          ]
        }
      },
      {
        "type": "column",
        "column": {},
        "children": [
            {
              "type": "callout",
              "callout": {
                "rich_text": [
                  {
                    "type": "text",
                    "text": {
                      "content": "{{CATEGORY_2}}"
                    },
                    "annotations": {
                      "bold": true
                    }
                  }
                ],
                "icon": {
                  "type": "icon",
                  "icon": {
                    "name": "{{CATEGORY_2_ICON}}",
                    "color": "{{CATEGORY_2_COLOR}}"
                  }
                },
                "color": "default_background"
              }
            }
          ]
        }
      },
      {
        "type": "column",
        "column": {},
        "children": [
            {
              "type": "callout",
              "callout": {
                "rich_text": [
                  {
                    "type": "text",
                    "text": {
                      "content": "{{CATEGORY_3}}"
                    },
                    "annotations": {
                      "bold": true
                    }
                  }
                ],
                "icon": {
                  "type": "icon",
                  "icon": {
                    "name": "{{CATEGORY_3_ICON}}",
                    "color": "{{CATEGORY_3_COLOR}}"
                  }
                },
                "color": "default_background"
              }
            }
          ]
        }
      }
    ]
  }
}
```
