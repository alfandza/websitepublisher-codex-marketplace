# WebsitePublisher Codex Plugin — Local Test

This is a local Codex plugin wrapper for the hosted WebsitePublisher MCP server.

## Structure

- `.codex-plugin/plugin.json` — Codex plugin manifest
- `.mcp.json` — WebsitePublisher MCP connection
- `skills/websitepublisher/SKILL.md` — WebsitePublisher workflow instructions

## Test with the local marketplace

From the repository root, register this marketplace with Codex:

`codex plugin marketplace add .`

The repository already includes `.agents/plugins/marketplace.json`, whose plugin source points at `./plugins/websitepublisher`.

The relevant marketplace entry is:

```json
{
  "name": "local-websitepublisher",
  "interface": {
    "displayName": "Local WebsitePublisher"
  },
  "plugins": [
    {
      "name": "websitepublisher",
      "source": {
        "source": "local",
        "path": "./plugins/websitepublisher"
      },
      "policy": {
        "installation": "AVAILABLE",
        "authentication": "ON_INSTALL"
      },
      "category": "Developer Tools"
    }
  ]
}
```

The path above assumes this plugin folder is named `websitepublisher` inside the marketplace root.

If Codex shows another marketplace with the same name, remove the stale marketplace registration first or install explicitly with `websitepublisher@websitepublisher-local` after confirming the root is this repository.

## GitHub test later

Once Mike puts the plugin folder in a GitHub marketplace repository, Codex can add that marketplace with:

`codex plugin marketplace add owner/repo`

Then the WebsitePublisher plugin can be discovered from that marketplace.

The MCP server itself remains at:

`https://mcp.websitepublisher.ai/mcp/`

The endpoint requires OAuth2. Codex discovers the authorization server from the MCP `401` challenge; do not add access tokens or client secrets to `.mcp.json`.
