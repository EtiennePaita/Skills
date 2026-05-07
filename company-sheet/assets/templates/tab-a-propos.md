# Template: Tab — A propos

Children to append to the **"A propos"** paragraph block ID.
Call `patch-block-children` with `block_id = <A_PROPOS_PARAGRAPH_ID>`.

## Placeholders

| Token | Description | Example |
|---|---|---|
| `{{COMPANY_WEBSITE_URL}}` | Official homepage URL | `https://www.withings.com` |
| `{{COMPANY_RESUME}}` | 2–3 sentence history + mission | `Fondée en 2008…` |
| `{{BENEFIT_1}}` | Employee benefit #1 | `Politique de travail hybride` |
| `{{BENEFIT_2}}` | Employee benefit #2 | `Culture d'innovation forte` |
| `{{BENEFIT_3}}` | Employee benefit #3 | `Exposition internationale` |
| `{{BENEFIT_4}}` | Employee benefit #4 | `Environnement centré sur le bien-être` |
| `{{HEADQUARTERS}}` | HQ city, country (+ satellite offices) | `Issy-les-Moulineaux, France (+ Boston, Hong Kong)` |
| `{{COMPANY_NAME}}` | Company name (used in link label) | `Withings` |
| `{{CAREERS_URL}}` | Direct URL to careers/jobs page | `https://www.withings.com/eu/fr/work-with-us` |

## JSON Children Array

```json
[
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
      "icon": { "type": "emoji", "emoji": "ℹ️" },
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
      "rich_text": [{ "type": "text", "text": { "content": "{{HEADQUARTERS}}" } }],
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
```
