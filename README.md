# Flatland MCP

**Financial reasoning infrastructure for AI agents.**  
Typed models. Deterministic compilation. Cryptographic receipts.

---

## What This Is

Flatland is a financial modeling engine that connects to AI agents via MCP. Your agent describes a business, calls Flatland's tools, and gets back a compiled financial model — typed, verifiable, and reproducible.

The agent brings language. Flatland brings structure.

```
┌─────────────────────────────────────────────────────────────────┐
│  Your AI agent  (Claude Code / Cursor / Codex / any harness)    │
│  ↓  MCP tools                                                   │
│  Flatland Engine  (api.flatlandfi.com)                          │
│  ↓  typed IR → compiled outputs + signed receipt                │
│  Your machine  (client-owned receipt chain)                     │
└─────────────────────────────────────────────────────────────────┘
```

Every number is **compiled**, not narrated. Every output ships with a cryptographic receipt your client holds — Flatland retains nothing server-side.

---

## Quick Connect

### Claude Code

Add to `~/.claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "flatland": {
      "command": "npx",
      "args": ["-y", "flatland-setup"],
      "env": {
        "FLATLAND_API_KEY": "your-key-here"
      }
    }
  }
}
```

### Cursor / Windsurf

Add to `.cursor/mcp.json` (or equivalent):

```json
{
  "mcpServers": {
    "flatland": {
      "command": "npx",
      "args": ["-y", "flatland-setup"],
      "env": {
        "FLATLAND_API_KEY": "your-key-here"
      }
    }
  }
}
```

### Any MCP-compatible harness

```bash
FLATLAND_API_KEY=your-key npx flatland-setup
```

→ Get your API key at **[flatlandfi.com](https://flatlandfi.com)**

---

## Tool Catalog

### Model Lifecycle — FREE

| Tool | Description |
|------|-------------|
| `flatland_init` | Initialize and load server-side domain skills |
| `flatland_create_model` | Create a model (name, grain, period range, currency) |
| `flatland_load_model` | Load a saved model from local durable storage |
| `flatland_save_model` | Persist the active model to disk |
| `flatland_list_models` | List all locally saved models |
| `flatland_explain` | Trace the upstream compute chain for any driver |
| `flatland_diff_scenarios` | Compare two named scenarios |
| `flatland_list_decisions` | Retrieve the decision trace log for a model |
| `flatland_verify` | **Stateless verifier** — verify a signed receipt against inputs (no API key required) |

### Build — FREE

| Tool | Description |
|------|-------------|
| `flatland_add_driver` | Add a typed assumption driver (constant, growth rate, ratio, etc.) |
| `flatland_add_computed` | Add a computed driver with a formula |
| `flatland_bulk_add` | Add 3+ drivers atomically |
| `flatland_update_driver` | Update a driver's value, formula, or metadata |
| `flatland_remove_driver` | Remove a driver (cascade to dependents) |

### Compute — Metered ($0.10/answer, 50 free/month)

| Tool | Description |
|------|-------------|
| `flatland_compile` | Compile the active model; returns all computed values |
| `flatland_sensitivity` | Rank assumptions by impact on a target driver |
| `flatland_impact_preview` | Preview downstream impact of proposed changes |
| `flatland_create_scenario` | Create a named scenario with driver overrides |

### Export

| Tool | Description |
|------|-------------|
| `flatland_export` | Export as HTML (institutional audit artifact), Excel, JSON, or Markdown |

**Total: 37 MCP tools.** See [full tool reference →](https://flatlandfi.com/docs/tools)

---

## Why Flatland, Not a Spreadsheet or a Chat Model

| Capability | Flatland | Spreadsheet | LLM-generated model |
|---|---|---|---|
| Typed driver graph (no anonymous cells) | ✅ | ❌ | ❌ |
| Deterministic, reproducible compilation | ✅ | partial | ❌ |
| Cryptographic receipt chain | ✅ | ❌ | ❌ |
| Client-owned custody (server retains nothing) | ✅ | n/a | ❌ |
| Stateless, offline-verifiable outputs | ✅ | ❌ | ❌ |
| Agent-native / MCP-first | ✅ | ❌ | ❌ |
| Acyclic DAG — no circular dependencies | ✅ enforced | ❌ | ❌ |

**The engine never calls an LLM.** The LLM calls the engine. Computation is deterministic and independent of which AI model your agent uses — today Claude Code, tomorrow Gemini CLI, same compiled numbers.

---

## Architecture

Flatland uses a **per-call IR model**. The Intermediate Representation (IR) is a typed, declarative JSON-serializable DAG of drivers. It lives on your machine. Each compile call sends the IR to Flatland's engine, receives results plus a signed receipt, and the server discards the request.

```
flatland_create_model → flatland_add_driver(s) → flatland_compile
                                                        ↓
                                            compiled values + signed receipt
                                                        ↓
                                            your machine (server retains nothing)
```

**Receipt chain (Flatland Institutional):** Every compiled output ships with an HMAC-signed receipt that includes a `parent_hash` binding it to the prior receipt, forming a tamper-evident chain. `flatland_verify` is free and stateless — pass the receipt and the original IR, the server recomputes and verifies the HMAC. No API key required. Verifiable offline.

---

## Pricing

| Plan | Compiled answers | Price |
|------|-----------------|-------|
| Free | 50 / month | $0 |
| Metered | Beyond 50 | $0.10 / answer |
| Institutional | Signed receipt chain, audit HTML, decision trace | [Contact us](https://flatlandfi.com/enterprise) |

Free includes all model build tools, `flatland_verify`, `flatland_diff_scenarios`, `flatland_explain`, and `flatland_list_decisions`. Only `flatland_compile`, `flatland_sensitivity`, and `flatland_impact_preview` are metered.

---

## Flatland Agent

For a self-contained decision session in your terminal:

```bash
npx flatland-agent
```

Six-stage Structured Decision Session → compiled model → signed HTML export with GO / NO-GO / UNCERTAIN verdict. Bring your own Anthropic or OpenAI key.

---

## Links

| Resource | URL |
|----------|-----|
| Docs & quickstart | [flatlandfi.com/docs](https://flatlandfi.com/docs) |
| Get an API key | [flatlandfi.com](https://flatlandfi.com) |
| Flatland Agent CLI | `npx flatland-agent` |
| Status | [status.flatlandfi.com](https://status.flatlandfi.com) |

---

## License

MIT — see [LICENSE](LICENSE).
