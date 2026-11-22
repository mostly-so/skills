# Installing the Mostly MCP server

Mostly is a hosted (remote) MCP server. There is nothing to clone, build or run locally: you only add its URL to the client's MCP settings.

- URL: `https://mostly.so/api/mcp`
- Transport: Streamable HTTP
- Auth: OAuth (MCP sign-in), or an API key sent as a Bearer token

## Cline

Add this to `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "mostly": {
      "type": "streamableHttp",
      "url": "https://mostly.so/api/mcp"
    }
  }
}
```

On first use Cline opens the browser so the user can sign in to mostly.so and pick a workspace.

If the client can't do the OAuth sign-in, use an API key instead. The user creates one at mostly.so under **Settings → API & MCP** (keys start with `mst_live_`). Never invent or guess a key; ask the user for it.

```json
{
  "mcpServers": {
    "mostly": {
      "type": "streamableHttp",
      "url": "https://mostly.so/api/mcp",
      "headers": {
        "Authorization": "Bearer mst_live_..."
      }
    }
  }
}
```

## Check it works

Call the `list_brands` tool. It returns the brands in the user's workspace. An empty list is fine: the user can create a brand with `create_brand` or at mostly.so.

Setup for other clients: https://mostly.so/docs/mcp/setup
