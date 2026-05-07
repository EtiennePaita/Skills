# Template: Tab — Concurrents

Children to append to the **"Concurrents"** paragraph block ID.
Call `patch-block-children` with `block_id = <CONCURRENTS_PARAGRAPH_ID>`.

## Placeholders

| Token | Description | Example |
|---|---|---|
| `{{COMPETITOR_1}}` | Name — what they compete on | `Amazon — leader incontesté du e-commerce France (+35 M visiteurs/mois)` |
| `{{COMPETITOR_2}}` | Name — what they compete on | `Leboncoin — #2 France, leader seconde main généraliste` |
| `{{COMPETITOR_3}}` | Name — what they compete on | `Vinted — leader habillement de seconde main, croissance mobile` |
| `{{COMPETITOR_4}}` | Name — what they compete on | `Cdiscount — marketplace généraliste française` |
| `{{COMPETITOR_5}}` | Name — what they compete on | `Temu / Shein — plateformes ultra low-cost en forte progression` |

> 3–5 competitors recommended. Add or remove `bulleted_list_item` blocks as needed.

## JSON Children Array

```json
[
  {
    "type": "heading_3",
    "heading_3": {
      "rich_text": [{ "type": "text", "text": { "content": "Concurrents" } }],
      "is_toggleable": false,
      "color": "default"
    }
  },
  {
    "type": "bulleted_list_item",
    "bulleted_list_item": {
      "rich_text": [{ "type": "text", "text": { "content": "{{COMPETITOR_1}}" } }],
      "color": "default"
    }
  },
  {
    "type": "bulleted_list_item",
    "bulleted_list_item": {
      "rich_text": [{ "type": "text", "text": { "content": "{{COMPETITOR_2}}" } }],
      "color": "default"
    }
  },
  {
    "type": "bulleted_list_item",
    "bulleted_list_item": {
      "rich_text": [{ "type": "text", "text": { "content": "{{COMPETITOR_3}}" } }],
      "color": "default"
    }
  },
  {
    "type": "bulleted_list_item",
    "bulleted_list_item": {
      "rich_text": [{ "type": "text", "text": { "content": "{{COMPETITOR_4}}" } }],
      "color": "default"
    }
  },
  {
    "type": "bulleted_list_item",
    "bulleted_list_item": {
      "rich_text": [{ "type": "text", "text": { "content": "{{COMPETITOR_5}}" } }],
      "color": "default"
    }
  },
  {
    "type": "paragraph",
    "paragraph": { "rich_text": [], "color": "default" }
  }
]
```
