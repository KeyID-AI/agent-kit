# @keyid/agent-kit

**Give Claude, Cursor, or any MCP client a real email address. Free. No signup.**

27 email tools via Model Context Protocol (MCP): send, receive, reply, search inbox, manage contacts, set auto-reply, schedule delivery — everything an AI agent needs to handle email autonomously.

Powered by [KeyID.ai](https://keyid.ai) — free email infrastructure for AI agents. No human registration, no API keys to manage, no cost.

## Install

```bash
npm install @keyid/agent-kit
# or
yarn add @keyid/agent-kit
```

## Usage

### With Claude Desktop

Add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "keyid": {
      "command": "npx",
      "args": ["@keyid/agent-kit"],
      "env": {
        "KEYID_PUBLIC_KEY": "...hex...",
        "KEYID_PRIVATE_KEY": "...hex..."
      }
    }
  }
}
```

### With any MCP client

```bash
# Run directly
npx @keyid/agent-kit

# Or with existing keypair
KEYID_PUBLIC_KEY=abc123 KEYID_PRIVATE_KEY=def456 npx @keyid/agent-kit
```

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `KEYID_BASE_URL` | API base URL | `https://keyid.ai` |
| `KEYID_PUBLIC_KEY` | Ed25519 public key (hex) | Auto-generated |
| `KEYID_PRIVATE_KEY` | Ed25519 private key (hex) | Auto-generated |

## Tools (27)

### Identity & Auth
| Tool | Description |
|------|-------------|
| `keyid_provision` | Register agent, get email address |
| `keyid_get_email` | Get current active email |

### Messages
| Tool | Description |
|------|-------------|
| `keyid_get_inbox` | Fetch inbox (with search, filtering) |
| `keyid_send` | Send email (scheduled, display name, HTML) |
| `keyid_reply` | Reply to a message |
| `keyid_forward` | Forward a message |
| `keyid_update_message` | Update read/starred status |
| `keyid_get_unread_count` | Count unread messages |

### Threads & Drafts
| Tool | Description |
|------|-------------|
| `keyid_list_threads` | List conversation threads |
| `keyid_get_thread` | Get thread with messages |
| `keyid_create_draft` | Create a draft |
| `keyid_send_draft` | Send a draft |

### Settings
| Tool | Description |
|------|-------------|
| `keyid_get_auto_reply` | Get auto-reply settings |
| `keyid_set_auto_reply` | Configure vacation responder |
| `keyid_get_signature` | Get email signature |
| `keyid_set_signature` | Set email signature |
| `keyid_get_forwarding` | Get forwarding settings |
| `keyid_set_forwarding` | Configure forwarding |

### Contacts
| Tool | Description |
|------|-------------|
| `keyid_list_contacts` | List saved contacts |
| `keyid_create_contact` | Create a contact |
| `keyid_delete_contact` | Delete a contact |

### Webhooks
| Tool | Description |
|------|-------------|
| `keyid_list_webhooks` | List webhooks |
| `keyid_create_webhook` | Create webhook |
| `keyid_get_webhook_deliveries` | Delivery history |

### Lists & Metrics
| Tool | Description |
|------|-------------|
| `keyid_manage_list` | Add/remove from allow/blocklist |
| `keyid_get_metrics` | Query usage metrics |

## Example Conversation

```
User: Check my email

Agent: [calls keyid_get_inbox]
You have 3 new messages:
1. alice@company.com — "Q1 Report" (2 hours ago)
2. bob@partner.org — "Meeting tomorrow" (5 hours ago)
3. noreply@service.com — "Password reset" (1 day ago)

User: Reply to Alice saying I'll review it today

Agent: [calls keyid_reply with message_id and body]
Reply sent to alice@company.com.
```

## Protocol

Uses MCP JSON-RPC over stdio (protocol version 2024-11-05). Compatible with Claude Desktop, Cursor, and any MCP client.

## License

MIT
