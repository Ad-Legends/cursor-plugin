# Ad Legends Cursor plugin

Official [Ad Legends](https://www.adlegends.ai/mcp) plugin for Cursor and Grok Bot. It connects the hosted brands MCP so an agent can create a brand from a URL, import a design system, and generate finished on-brand ads — written by advertising legends, not generic AI.

Homepage: [https://www.adlegends.ai/mcp](https://www.adlegends.ai/mcp)

MCP URL: `https://www.adlegends.ai/api/mcp/brands`

This repo is URL-only. It ships no API keys, tokens, or secrets.

## Install

1. In Cursor, open **Customize → Plugins** (or add a custom MCP connector).
2. Point Cursor at this repository, or add the MCP server URL above.
3. Sign in with Ad Legends (OAuth in chat apps; a scoped key from [Settings → MCP](https://www.adlegends.ai/settings/mcp) in developer tools).
4. Ask in plain language: “Make an ad for https://example.com.”

cursor.directory can ingest this public tree as-is. The plugin name is `ad-legends`.

## What the agent should do

Just connected? Call **`get_started`**. Do not scan the catalog or invent a tool name.

Default path for “make an ad”:

1. Website URL, no `brandId` → `create_brand_from_url` (free). It returns a `brandId`.
2. Existing brand → `get_credit_status` (`requiredCredits: 9`) → `create_ads` → poll `get_ad_session`.
3. Optional craft: `generate_strategies` → `generate_strategic_brief` → `generate_creative_ideas` → `create_ads`.

Full catalog and setup: [adlegends.ai/mcp](https://www.adlegends.ai/mcp).

## Skills

| Skill | When to use |
| --- | --- |
| `make-an-ad` | User wants a finished ad. Always starts with `get_started`. |
| `brand-from-url` | Cold-start a brand from a website URL. |
| `import-design-system` | Import a W3C DTCG / Claude Design token document into Brand Memory. |

## Layout

```
.cursor-plugin/plugin.json
mcp.json
README.md
LICENSE
PUBLISH.md
.gitignore
assets/logo.png
assets/logo.svg
skills/make-an-ad/SKILL.md
skills/brand-from-url/SKILL.md
skills/import-design-system/SKILL.md
```

`mcp.json` is URL-only:

```json
{
  "mcpServers": {
    "Ad Legends": {
      "url": "https://www.adlegends.ai/api/mcp/brands"
    }
  }
}
```

## Credits

Paid generation is metered in Legend Credits. `create_ads` costs 9 (refunded on failure). Preflight with `get_credit_status` before spending. If a run is blocked, call `recommend_credit_upgrade` — it returns billing links and does not charge a card from MCP.

This server cannot cancel subscriptions, issue refunds, or run admin/staff tools.

## License

MIT. See [LICENSE](./LICENSE).
