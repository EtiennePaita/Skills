# Template: Tab — Clients

Children to append to the **"Clients"** paragraph block ID.
Call `patch-block-children` with `block_id = <CLIENTS_PARAGRAPH_ID>`.

> **Format convention**: Start each client entry with a relevant emoji followed
> by two spaces for alignment, then a short description.
> Examples: `👨`, `🏥`, `🏩`, `🥼`, `🏪`, `🛒`, `🏢`

## Placeholders

| Token | Format | Example |
|---|---|---|
| `{{CLIENT_1}}` | `EMOJI  Description` | `👨  Particuliers soucieux de leur santé (B2C — principal marché)` |
| `{{CLIENT_2}}` | `EMOJI  Description` | `🏥  Hôpitaux et cliniques (suivi à distance des patients chroniques)` |
| `{{CLIENT_3}}` | `EMOJI  Description` | `🏩  Compagnies d'assurance santé (programmes de prévention)` |
| `{{CLIENT_4}}` | `EMOJI  Description` | `🥼  Chercheurs et centres d'essais cliniques` |
| `{{CLIENT_5}}` | `EMOJI  Description` | `🏪  Revendeurs premium (Apple Store, FNAC, Darty, Amazon)` |

> Add or remove `paragraph` blocks as needed (3–7 items recommended).

## JSON Children Array

```json
[
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
  }
]
```
