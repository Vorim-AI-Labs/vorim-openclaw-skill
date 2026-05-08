# Vorim AI — OpenClaw Skill

> Give your OpenClaw agent its own cryptographic identity, scoped permissions, and a tamper-evident audit trail.

This is the official **OpenClaw Skill** for [Vorim AI](https://vorim.ai), the identity and trust layer for autonomous AI agents.

Once installed, your OpenClaw agent will:

- Verify its own identity before acting
- Check permissions before destructive or external actions (shell, email, payments)
- Log every action with a hash-linked, tamper-evident audit trail
- Build a public trust score (0-100) over time that any third party can verify

## What is Vorim AI?

Vorim AI gives every AI agent its own Ed25519 keypair, time-bounded scoped permissions, and a publicly verifiable trust score. The protocol underneath (VAIP) is open, MIT-licensed, and submitted to IETF as `draft-nyantakyi-vaip-agent-identity-01`.

If you've ever asked "which agent did this?" after something went wrong — Vorim is what answers that question, instantly, with cryptographic proof.

## Repo Layout

```
vorim-openclaw-skill/
├── README.md
├── LICENSE
└── skills/
    └── vorim/
        └── SKILL.md   ← the skill manifest
```

## Install

### Option 1: Copy the skill

Copy `skills/vorim/SKILL.md` to your OpenClaw skills directory:

```bash
# Global (all workspaces)
mkdir -p ~/.openclaw/skills/vorim
cp skills/vorim/SKILL.md ~/.openclaw/skills/vorim/

# Or workspace-specific
mkdir -p ./skills/vorim
cp skills/vorim/SKILL.md ./skills/vorim/
```

### Option 2: Add the MCP server

Add Vorim's MCP server to your OpenClaw config:

```bash
mcporter add vorim --command "npx @vorim/mcp-server" --env VORIM_API_KEY=agid_sk_live_...
```

Or manually:

```json
{
  "mcpServers": {
    "vorim": {
      "command": "npx",
      "args": ["-y", "@vorim/mcp-server"],
      "env": {
        "VORIM_API_KEY": "agid_sk_live_..."
      }
    }
  }
}
```

## Setup

1. Sign up at [vorim.ai](https://vorim.ai) (free, no credit card)
2. Go to **Settings → API Keys** and create a key
3. Set `VORIM_API_KEY=agid_sk_live_...` in your environment
4. On first run, the skill registers your OpenClaw agent automatically and saves the agent ID

The free tier supports 3 agents and 10K events per month — enough for personal use and prototyping.

## 17 MCP Tools Available

| Category | Tools |
|---|---|
| **Health** | `vorim_ping` |
| **Identity** | `vorim_register_agent`, `vorim_register_ephemeral`, `vorim_get_agent`, `vorim_list_agents`, `vorim_update_agent`, `vorim_revoke_agent` |
| **Permissions** | `vorim_check_permission`, `vorim_grant_permission`, `vorim_list_permissions`, `vorim_revoke_permission` |
| **Credentials** | `vorim_delegate_credential`, `vorim_request_token`, `vorim_list_delegations` |
| **Audit** | `vorim_emit_event`, `vorim_export_audit` |
| **Trust** | `vorim_verify_trust` |

## Why This Matters

If you run OpenClaw agents that browse the web, run shell commands, send emails, or call APIs, those agents are acting in your name. Without an identity layer:

- You can't prove which agent did what
- You can't restrict permissions per agent
- A compromised marketplace skill has the same authority as any trusted action
- Your audit trail is "trust the database"

Vorim adds the missing layer. Every agent action is identified, scoped, and logged in a way that's verifiable by you, by your security team, or by a regulator — without trusting any single vendor's database.

## Links

- **Platform:** [vorim.ai](https://vorim.ai)
- **MCP Server:** [github.com/Kzino/vorim-mcp-server](https://github.com/Kzino/vorim-mcp-server)
- **Protocol Spec (VAIP):** [github.com/Kzino/vorim-protocol](https://github.com/Kzino/vorim-protocol)
- **TypeScript SDK:** [@vorim/sdk on npm](https://www.npmjs.com/package/@vorim/sdk)
- **Python SDK:** [vorim on PyPI](https://pypi.org/project/vorim/)
- **OpenClaw:** [openclaw.ai](https://openclaw.ai)
- **IETF Draft:** [draft-nyantakyi-vaip-agent-identity-01](https://datatracker.ietf.org/doc/draft-nyantakyi-vaip-agent-identity/)

## License

MIT — see [LICENSE](LICENSE) for details.

---

Built by [Vorim AI](https://vorim.ai). Questions or feedback: [kwame@vorim.ai](mailto:kwame@vorim.ai).
