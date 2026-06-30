# mcp-warden

Vet a third-party MCP server **before** you enable it in Claude Code. Produces a security & compatibility sheet, statically scans the server as hostile data, and returns an ALLOW / REVIEW / BLOCK verdict with file:line evidence. The MCP sibling of `skill-security-scan`.

## Why

An MCP server is untrusted code with network access and tool privileges: it can read your data, hit the network, and mutate state. Tool misuse / malformed tool calls are ~31% of agent production failures, and the community has been asking for a per-MCP "security & compatibility sheet" (permissions, scopes, env, network, tool I/O, rollback) instead of trusting a README. mcp-warden produces exactly that, plus a static scan for injection, exfiltration, dangerous execution, over-broad scope, and bad secret handling.

## What you get

`/mcp-warden` (skill): the hostile-data rule, the sheet template, the scan checklist, and the verdict logic. Skill-only, no per-session cost.

## Install (Claude Code, local directory marketplace)

```jsonc
// ~/.claude/settings.json
"extraKnownMarketplaces": {
  "mcp-warden": { "source": { "source": "directory", "path": "C:\\Users\\<you>\\mcp-warden" } }
},
"enabledPlugins": { "mcp-warden@mcp-warden": true }
```

Or after publishing: `"source": { "source": "github", "repo": "<you>/mcp-warden" }`.

## Usage

Run `/mcp-warden` (or "vet this MCP server") before adding any third-party MCP. Enable only on ALLOW, or after explicitly overriding a REVIEW/BLOCK.

## Limits

Static review catches obvious malice and sloppiness, not a determined supply-chain attack behind a clean published version. Pin versions; re-scan on update. Runtime behavior is out of scope.

## License

MIT

---

Part of the **[claude-code-skills](https://github.com/Zavelinski/claude-code-skills)** collection: a one-line [Claude Code](https://claude.com/claude-code) plugin marketplace of focused skills, plugins, and MCP servers.

```
/plugin marketplace add Zavelinski/claude-code-skills
```
