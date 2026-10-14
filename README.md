# Mise for Claude, ChatGPT and Codex

[Mise](https://mise.modevshop.com) is the event system for restaurants and venues.
This connector lets your AI assistant work with your Mise account: what's on
the calendar, adding events, which leads still need a reply, your active
proposals, your rooms, and whether a room is free.

**Server address:** `https://mise.modevshop.com/mcp`

An owner or manager signs in with their Mise account and picks the venue. There
are no keys to copy. The assistant can add events (it asks first), but it can't
delete anything or send messages.

## Install

### Claude (web, desktop and mobile)

On your phone? Follow the three-step guide at
[mise.modevshop.com/ai](https://mise.modevshop.com/ai).

[**Add Mise to Claude**](https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=Mise&connectorUrl=https%3A%2F%2Fmise.modevshop.com%2Fmcp),
then click **Connect**, sign in to Mise and click **Allow**.

Or by hand: **Settings → Connectors → Add custom connector**, name `Mise`, URL
`https://mise.modevshop.com/mcp`, leave the advanced settings blank. On Team
and Enterprise plans an owner adds it under **Admin settings → Connectors**.

### ChatGPT

Open **Plugins**, choose **+ → Add custom MCP server**, and enter
`https://mise.modevshop.com/mcp` with OAuth sign-in. Sign in to Mise and click
**Allow**. Your workspace admin may need to allow custom servers.

### Claude Code

```bash
claude plugin install mise --marketplace TheModevShop/mise-mcp
```

Then run `/mcp`, pick **mise** and choose **Authenticate**. Without the plugin:
`claude mcp add --transport http mise https://mise.modevshop.com/mcp`.

### Codex

```bash
codex plugin marketplace add TheModevShop/mise-mcp
codex plugin add mise@mise
codex mcp login mise
```

Without the plugin: `codex mcp add mise --url https://mise.modevshop.com/mcp`.

### Other assistants

Any MCP client that supports remote servers (Streamable HTTP) with OAuth can
connect to `https://mise.modevshop.com/mcp`. Clients that only take a fixed
token can use a key from Mise → **Settings → AI assistants**, sent as
`Authorization: Bearer <key>`. Those keys are read-only. Keep keys out of chats, files and URLs.

## Try it

- "What's on this week?"
- "Add a jazz night next Friday at 7."
- "Which Mise leads still need a reply?"
- "List my active proposals in Mise."
- "Is our private dining room free next Saturday evening?"

## Tools

| Tool | What it returns |
| --- | --- |
| `list_leads_needing_reply` | Leads with open follow-ups or unsent reply drafts: contact name and email, a short summary, last update |
| `list_active_proposals` | Recent proposals that aren't withdrawn or expired, with status and views |
| `list_rooms` | Your active rooms and their IDs |
| `get_room_availability` | Events that overlap a room and a time window |
| `list_events` | Events between two dates: type, time, room, performer, guests, budget |
| `get_event_options` | Event types, rooms, performers with their last booking, and recent events, so the assistant can suggest the usual room, time and guests |
| `create_event` | Adds one event. It asks what kind of event, then only what's missing, and won't double-book a room unless you say so |

Lists are bounded (up to 50 items), not complete reports. An availability answer
marked incomplete doesn't prove a room is free.

## Permissions and privacy

- Only owners and managers can connect an assistant. The connection only sees
  the venue picked during sign-in.
- Every connection is listed in Mise under **Settings → AI assistants**, with
  when it was last used. Disconnect it there anytime and access stops right
  away.
- Mise shares data with the assistant only when someone using it asks. The
  assistant's provider handles it under its own terms.
- [Privacy policy](https://mise.modevshop.com/privacy) ·
  [Terms](https://mise.modevshop.com/terms)

## Troubleshooting

- **"Unauthorized" or "Forbidden":** the connection was removed or the key was
  revoked. Reconnect from your assistant's connector settings.
- **"Service unavailable":** assistant access is turned off for Mise right now.
- **Wrong venue:** disconnect, then connect again and pick the other venue.

## Support

[Open an issue](https://github.com/TheModevShop/mise-mcp/issues) or email
[mise@modevshop.com](mailto:mise@modevshop.com).

This repository holds the install files only. The server itself runs at
`mise.modevshop.com`.
