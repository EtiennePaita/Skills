# Template: Tabs Skeleton

A `tab` block appended directly to the page after the KPI callout.
Its 5 direct `paragraph` children become the clickable tab headers in the Notion UI.

After appending this block, retrieve the block IDs of the 5 paragraphs via
`get-block-children` on the `tab` block ID, then populate each tab body
separately using the per-tab templates.

> **API note**: Each `paragraph` child of a `tab` acts as a tab label.
> Its content (the tab body) is appended as *children of that paragraph*
> via a subsequent `patch-block-children` call.

## JSON Block

```json
{
  "type": "tab",
  "tab": {
    "children": [
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [{ "type": "text", "text": { "content": "A propos" } }],
          "icon": { "type": "icon", "icon": { "name": "info-alternate", "color": "gray" } },
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [{ "type": "text", "text": { "content": "Produits & Services" } }],
          "icon": { "type": "icon", "icon": { "name": "shopping-bag", "color": "gray" } },
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [{ "type": "text", "text": { "content": "Clients" } }],
          "icon": { "type": "icon", "icon": { "name": "groups", "color": "gray" } },
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [{ "type": "text", "text": { "content": "Concurrents" } }],
          "icon": { "type": "icon", "icon": { "name": "city", "color": "gray" } },
          "color": "default"
        }
      },
      {
        "type": "paragraph",
        "paragraph": {
          "rich_text": [{ "type": "text", "text": { "content": "Avis" } }],
          "icon": { "type": "icon", "icon": { "name": "star-half", "color": "yellow" } },
          "color": "default"
        }
      }
    ]
  }
}
```

## After Creation: Retrieve Tab Paragraph IDs

```
GET /blocks/{TAB_BLOCK_ID}/children
→ results[0].id  →  "A propos"         paragraph ID
→ results[1].id  →  "Produits & Services" paragraph ID
→ results[2].id  →  "Clients"          paragraph ID
→ results[3].id  →  "Concurrents"      paragraph ID
→ results[4].id  →  "Avis"             paragraph ID
```

Pass each ID to the corresponding tab body template.
