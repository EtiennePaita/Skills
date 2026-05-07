# Template: KPI Callout Banner

A top-level `callout` block appended directly to the page.
It holds a single-line rich_text KPI summary (Revenue · Market Position · Headcount).

> **API constraint**: `column_list` cannot be nested inside a `callout` via the
> REST API. The KPI data is therefore rendered as an inline rich_text string
> using emoji separators. Use the `equation` block pattern only when appending
> columns directly to the page (not inside a callout).

## Placeholders

| Token | Description | Example |
|---|---|---|
| `{{REVENUE}}` | Last known revenue | `~400 M€` |
| `{{MARKET_POSITION}}` | Market rank or label | `Leader`, `#17 France` |
| `{{HEADCOUNT}}` | Employee count | `+400`, `~300` |

## JSON Block

```json
{
  "type": "callout",
  "callout": {
    "rich_text": [
      {
        "type": "text",
        "text": {
          "content": "💵 CA : {{REVENUE}}     🏆 Position : {{MARKET_POSITION}}     👥 Effectif : {{HEADCOUNT}}"
        },
        "annotations": {
          "bold": false, "italic": false, "strikethrough": false,
          "underline": false, "code": false, "color": "default"
        }
      }
    ],
    "icon": { "type": "emoji", "emoji": "📊" },
    "color": "default_background"
  }
}
```
