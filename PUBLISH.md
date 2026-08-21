# Publish the Ad Legends Cursor plugin

Public source of truth for this plugin: [https://github.com/Ad-Legends/cursor-plugin](https://github.com/Ad-Legends/cursor-plugin).

Homepage / docs: [https://www.adlegends.ai/mcp](https://www.adlegends.ai/mcp)

MCP endpoint: `https://www.adlegends.ai/api/mcp/brands`

## Ingest checklist (cursor.directory)

cursor.directory reads a public GitHub tree. Keep the plugin at the **repository root** (do not nest another `cursor-plugin/` folder).

- [ ] `.cursor-plugin/plugin.json` exists
- [ ] `name` is `ad-legends` (lowercase kebab-case)
- [ ] `author.name` is `Ad Legends`
- [ ] `author.email` is `founders@adlegends.ai`
- [ ] `homepage` is `https://www.adlegends.ai/mcp`
- [ ] `repository` is `https://github.com/Ad-Legends/cursor-plugin`
- [ ] `logo` is the relative path `assets/logo.png`
- [ ] `skills` is `./skills/`
- [ ] Root `mcp.json` has a single HTTP server, URL only, no headers, no secrets
- [ ] Each skill is `skills/<name>/SKILL.md` with YAML `name` + `description`
- [ ] `README.md` documents install and the `get_started` rule
- [ ] `LICENSE` is present
- [ ] No `.env`, API keys, tokens, or `${VAR}` secrets in the tree

Submit the repo URL at [https://cursor.directory/plugins/new](https://cursor.directory/plugins/new).

## Cursor Marketplace (optional)

1. Confirm the checklist above.
2. Submit [https://github.com/Ad-Legends/cursor-plugin](https://github.com/Ad-Legends/cursor-plugin) at [https://cursor.com/marketplace/publish](https://cursor.com/marketplace/publish).
3. Cursor reviews listings before they appear under **Customize → Plugins**.

## Team Marketplace (optional)

Import this same GitHub URL from Cursor **Settings → Plugins → Team Marketplaces**. Single-plugin repos use root `.cursor-plugin/plugin.json` (no `marketplace.json` required).

## Do not

- Nest files under `cursor-plugin/cursor-plugin/`.
- Put API keys, OAuth secrets, or Authorization headers in `mcp.json`.
- Invent MCP tool names in skills. The live catalog is at [https://www.adlegends.ai/mcp](https://www.adlegends.ai/mcp). Always start ads with `get_started`.
- Use a unicode escape in `adlegends.ai`. Write the hostname with a normal ASCII `a`.
