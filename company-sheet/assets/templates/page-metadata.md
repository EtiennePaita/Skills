# Template: Page Metadata

Used in the **`post-page`** API call to create the Notion page shell.

## Placeholders

| Token | Description | Example |
|---|---|---|
| `{{PARENT_PAGE_ID}}` | Notion ID of the parent page | `35715bf7-d7ba-8008-9747-e28681f1b90c` |
| `{{COMPANY_NAME}}` | Company display name | `Withings` |
| `{{COMPANY_DOMAIN}}` | Domain for Hunter.io logo | `withings.com` |

> **Fallback**: If the Hunter logo URL returns 404, replace the `icon` object with:
> `{ "type": "emoji", "emoji": "🏢" }`

## JSON Payload

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
