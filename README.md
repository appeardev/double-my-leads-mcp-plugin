# Double My Leads

This repo is the Open Plugins package for the Double My Leads remote MCP server. The public connect URL is `https://api.chatconnector.app/mcp`. Nothing here reimplements those tools.

Public listing name is **Double My Leads**. The machine name in `plugin.json` is `double-my-leads` because Agent Plugins only allows lowercase `a-z0-9-.`.

`https://panel.wasndr.com/mcp` is a legacy alias on the same Coolify API app. Leave it up. Do not list it as the primary connect URL.

The connect host is `api.chatconnector.app`. The apex `chatconnector.app` is a different site.

## Install from cursor.directory

This repo *is* the package. It is not listed on cursor.directory until Jorge submits it.

After that listing exists, install Double My Leads from [cursor.directory](https://cursor.directory). Until then, add the server by hand in Cursor.

Jorge submits at [cursor.directory/plugins/new](https://cursor.directory/plugins/new): sign in, paste `https://github.com/appeardev/double-my-leads-mcp-plugin`, set the listing name to Double My Leads, submit.

## Mint a key

1. Sign in to the dashboard.
2. Open Developer → API (`/api-settings`).
3. Create a key. It starts with `wsndr_`.

Put the key in your environment as `WASNDR_API_KEY`. Do not commit it. Do not paste it into chat.

## Manual Cursor setup

Cursor → Customize → MCP, or edit `~/.cursor/mcp.json` / `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "double-my-leads": {
      "url": "https://api.chatconnector.app/mcp",
      "headers": {
        "Authorization": "Bearer ${env:WASNDR_API_KEY}"
      }
    }
  }
}
```

The packaged `mcp.json` and `.mcp.json` in this repo carry the URL only. Agent Plugins forbids secrets in package headers, so the Bearer header lives in your local Cursor config.

## Transactional, not bulk

This is a notification API. Order confirmations, reminders, agent replies. Not a bulk broadcast pipe. If you need mass outreach, this is the wrong product.

## Tools

24 tools. Titles and `readOnlyHint` / `destructiveHint` come from WAsndr #41 (`e2196c47`).

### Read-only

`readOnlyHint: true`

| Tool | Title |
| --- | --- |
| `check_whatsapp_number` | Check WhatsApp Number |
| `list_groups` | List Groups |
| `get_group_info` | Get Group Info |
| `get_group_participants` | Get Group Participants |
| `export_group_members` | Export Group Members |
| `list_sessions` | List Sessions |
| `get_session_status` | Get Session Status |
| `get_usage` | Get Usage |
| `get_message_history` | Get Message History |
| `list_api_accounts` | List API Accounts |
| `workspaces` | List Workspaces |

### Writes

`readOnlyHint: false`, `destructiveHint: false`

| Tool | Title |
| --- | --- |
| `send_whatsapp_message` | Send WhatsApp Message |
| `send_whatsapp_media` | Send WhatsApp Media |
| `send_group_message` | Send Group Message |
| `send_group_media` | Send Group Media |
| `send_poll` | Send Poll |
| `create_group` | Create Group |
| `add_group_participants` | Add Group Participants |
| `create_api_account` | Create API Account |
| `crm` | CRM Read And Write |
| `inbox` | Inbox Read And Write |
| `send` | Send Message |

`crm` and `inbox` mix reads and writes, so they are not marked read-only.

### Destructive

`destructiveHint: true`

| Tool | Title |
| --- | --- |
| `remove_group_participants` | Remove Group Participants |
| `archive_api_account` | Archive API Account |

## Package layout

| File | Why |
| --- | --- |
| `plugin.json` | Agent Plugins 1.0 manifest |
| `mcp.json` | Agent Plugins MCP config (Streamable HTTP) |
| `.mcp.json` | Same payload. cursor.directory also looks for the dotted name |
| `LICENSE` | MIT |
| `icon.svg` | DML stacked-rectangle mark from [appeardev/dml-web](https://github.com/appeardev/dml-web) (`public/brand/mark.svg`). Not a WhatsApp glyph |

No OAuth. Auth is a customer-minted `wsndr_` Bearer key.

## Links

- API docs: https://doublemyleads.com/api
- Privacy: https://doublemyleads.com/privacy (still a migration stub from the old WordPress site, not a finished policy)

## License

MIT. See `LICENSE`.
