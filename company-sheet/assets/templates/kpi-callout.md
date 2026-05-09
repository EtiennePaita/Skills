# Template: KPI Callout Banner

A top-level `callout` block appended directly to the page.
It holds KPI summary using 3 columns (Revenue · Market Position · Headcount).

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
    "rich_text": [],
    "color": "default_background",
    "icon": {
      "type": "icon",
      "icon": {
        "name": "chart donut",
        "color": "white"
      }
    }
  },
  "children": [
    {
      "type": "column_list",
      "column_list": {},
      "children": [
        {
          "type": "column",
          "column": {},
          "children": [
            {
              "type": "equation",
              "equation": {
                "expression": "\\huge\\texttt{\\textsf{💵}} \\\\ \\LARGE\\textbf{\\textsf{{{REVENUE}}}}"
              }
            }
          ]
        },
        {
          "type": "column",
          "column": {},
          "children": [
            {
              "type": "equation",
              "equation": {
                "expression": "\\huge\\texttt{\\textsf{🏆}} \\\\ \\LARGE\\textbf{\\textsf{{{MARKET_POSITION}}}}"
              }
            }
          ]
        },
        {
          "type": "column",
          "column": {},
          "children": [
            {
              "type": "equation",
              "equation": {
                "expression": "\\huge\\texttt{\\textsf{👥}} \\\\ \\LARGE\\textbf{\\textsf{{{HEADCOUNT}}}}"
              }
            }
          ]
        }
      ]
    }
  ]
}
```