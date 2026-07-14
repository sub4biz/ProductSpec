# Install ProductSpec MCP

ProductSpec MCP lets Claude, Cursor, Codex, and other MCP-aware agents read Product Specs as structured intent instead of loose Markdown.

## Generate Config

Print a copy-pasteable config for Claude Desktop:

```bash
npx --yes -p @productspec/parser@latest productspec mcp-config claude
```

Print the same stdio server config for Cursor:

```bash
npx --yes -p @productspec/parser@latest productspec mcp-config cursor
```

Both commands output:

```json
{
  "mcpServers": {
    "productspec": {
      "command": "npx",
      "args": ["--yes", "--package", "@productspec/parser@latest", "productspec", "mcp"]
    }
  }
}
```

## Claude Desktop

Paste the generated `mcpServers` block into your Claude Desktop config.

Common config locations:

- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

Restart Claude Desktop after editing the file.

## Cursor

Paste the generated `mcpServers` block into Cursor's MCP settings. If your Cursor version uses project MCP files, place it in `.cursor/mcp.json`.

Restart Cursor or reload MCP servers after editing the config.

## Smoke Test

Ask the agent:

```text
Use ProductSpec MCP to list Product Specs in this repository. Then validate one of them and load its Product Summary, Scope, Acceptance Criteria, AI Evals, Success Metrics, and Related Artifacts.
```

For implementation work, start with the prompt in [`docs/agent-mcp.md`](agent-mcp.md).
