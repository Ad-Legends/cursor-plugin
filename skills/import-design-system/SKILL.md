---
name: import-design-system
description: Import a W3C DTCG design-tokens document (for example a Claude Design export) into an Ad Legends brand. Use when the user has tokens, a design system JSON, or wants Claude Design colors/type in Brand Memory. Calls import_design_system; do not invent an import tool.
---

# Import a design system

`import_design_system` maps a W3C DTCG design-tokens document into the brand’s guidelines (color, font, typography, spacing, motion). Owner-only.

If you do not have a `brandId`, call `get_started` or `list_brands`, or cold-start with `create_brand_from_url`.

## Steps

1. Resolve `brandId` (`list_brands` / `get_brand`).
2. Load the user’s DTCG document (groups of `{ $type, $value }` tokens — the same shape Claude Design exports).
3. Call `import_design_system` with `brandId` and `designSystem`.
4. Verify with `export_design_system` and/or `get_brand_guidelines`.

To set type without a token file, use the real typography tools — do not invent names:

- `import_font_family` — one Google Fonts family into private storage
- `set_typography_roles` — one payload: optional `fontFamilies[]` plus locked `assignments[]` (headline, subhead, body, cta, eyebrow, legal, logo_text)
- `get_typography` — verify specimens and the role card
- `redetect_typography_roles` / `update_typography_role_assignment` — re-detect or edit one role

Companion story: https://www.adlegends.ai/use-with-claude-design

## After import

Ads stay on-brand automatically. Next creative step is still `get_started` → `get_credit_status` → `create_ads`, not an invented “generate from tokens” tool.

This server cannot cancel subscriptions, issue refunds, or run admin/staff tools. Docs: https://www.adlegends.ai/mcp
