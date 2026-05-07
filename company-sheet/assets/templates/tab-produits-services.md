# Template: Tab — Produits & Services

Children to append to the **"Produits & Services"** paragraph block ID.
Call `patch-block-children` with `block_id = <PRODUITS_PARAGRAPH_ID>`.

> **API constraint**: `child_database` blocks are **not** accepted as children
> of a paragraph/tab via the REST API. Products are listed as `bulleted_list_item`
> blocks instead.

## Placeholders

| Token | Description | Example |
|---|---|---|
| `{{PRODUCT_1}}` | Product name — short description | `Rakuten Marketplace — place de marché généraliste neuf & occasion` |
| `{{PRODUCT_2}}` | Product name — short description | `Rakuten Points — programme de cashback et de fidélité` |
| `{{PRODUCT_3}}` | Product name — short description | `Seconde main — héritage PriceMinister, forte croissance ESS` |
| `{{PRODUCT_4}}` | Product name — short description | `Rakuten TV — service de streaming VOD` |
| `{{PRODUCT_5}}` | Product name — short description | `Shops-in-the-shop — espaces dédiés aux enseignes partenaires` |

> Add or remove `bulleted_list_item` blocks as needed (3–6 items recommended).

## JSON Children Array

```json
[
  {
    "type": "heading_3",
    "heading_3": {
      "rich_text": [{ "type": "text", "text": { "content": "Produits & Services" } }],
      "is_toggleable": false,
      "color": "default"
    }
  },
  {
    "type": "bulleted_list_item",
    "bulleted_list_item": {
      "rich_text": [{ "type": "text", "text": { "content": "{{PRODUCT_1}}" } }],
      "color": "default"
    }
  },
  {
    "type": "bulleted_list_item",
    "bulleted_list_item": {
      "rich_text": [{ "type": "text", "text": { "content": "{{PRODUCT_2}}" } }],
      "color": "default"
    }
  },
  {
    "type": "bulleted_list_item",
    "bulleted_list_item": {
      "rich_text": [{ "type": "text", "text": { "content": "{{PRODUCT_3}}" } }],
      "color": "default"
    }
  },
  {
    "type": "bulleted_list_item",
    "bulleted_list_item": {
      "rich_text": [{ "type": "text", "text": { "content": "{{PRODUCT_4}}" } }],
      "color": "default"
    }
  },
  {
    "type": "bulleted_list_item",
    "bulleted_list_item": {
      "rich_text": [{ "type": "text", "text": { "content": "{{PRODUCT_5}}" } }],
      "color": "default"
    }
  },
  {
    "type": "paragraph",
    "paragraph": { "rich_text": [], "color": "default" }
  }
]
```
