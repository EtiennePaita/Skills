# Template: Tab — Avis

Children to append to the **"Avis"** paragraph block ID.
Call `patch-block-children` with `block_id = <AVIS_PARAGRAPH_ID>`.

## Placeholders

| Token | Description | Example |
|---|---|---|
| `{{GLASSDOOR_RATING}}` | Numeric score (as text) | `~3,5` |
| `{{GLASSDOOR_SUMMARY}}` | One-line culture snapshot | `PME reconnue pour ses produits innovants, culture parfois critique sur la croissance interne` |
| `{{GLASSDOOR_REVIEW_1}}` | Full quote + attribution | `"Produits passionnants…" — Employé(e) actuel(le)` |
| `{{GLASSDOOR_REVIEW_2}}` | Full quote + attribution | `"Super environnement…" — Ancien(ne) employé(e)` |

## JSON Children Array

```json
[
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
          "annotations": {
            "bold": true, "italic": false, "strikethrough": false,
            "underline": false, "code": false, "color": "default"
          }
        },
        {
          "type": "text",
          "text": { "content": " " },
          "annotations": {
            "bold": true, "italic": false, "strikethrough": false,
            "underline": false, "code": false, "color": "yellow"
          }
        },
        {
          "type": "text",
          "text": { "content": "{{GLASSDOOR_RATING}} / 5 " },
          "annotations": {
            "bold": false, "italic": false, "strikethrough": false,
            "underline": false, "code": false, "color": "yellow"
          }
        },
        {
          "type": "text",
          "text": { "content": "\n{{GLASSDOOR_SUMMARY}}" },
          "annotations": {
            "bold": false, "italic": false, "strikethrough": false,
            "underline": false, "code": false, "color": "default"
          }
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
          "annotations": {
            "bold": false, "italic": false, "strikethrough": false,
            "underline": false, "code": false, "color": "default"
          }
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
          "annotations": {
            "bold": false, "italic": false, "strikethrough": false,
            "underline": false, "code": false, "color": "default"
          }
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
```
