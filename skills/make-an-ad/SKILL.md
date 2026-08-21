---
name: make-an-ad
description: Generate a finished on-brand Fast Ad with Ad Legends. Use when the user asks to make an ad, create ads, or generate creative for a brand or URL. Always call get_started first. Never invent a tool name.
---

# Make an ad

This is the customer **brand** MCP (ads, brand memory, ideas, video). It is not a staff/support server.

## Always start here

Call **`get_started`** first (`intent: "make_an_ad"` plus any `brandUrl` or `brandId`). Follow `nextActions`. Do not scan the catalog or invent a name (`generate_ad`, `make_ad`, `create_campaign`, `refund`, `cancel`, admin).

Confirm the connection with `whoami` only if you need account/scopes. Then return to `get_started` for the next creative step.

## Default path

1. Website URL, no `brandId` → `create_brand_from_url` (free). It returns a `brandId` and `create_ads` invitations.
2. Existing brand → `list_brands` if you need to pick one, then `get_credit_status` (`requiredCredits: 9`) → `create_ads` (`brandId`, `targetAudience`, `keyMessage`, `tone`) → poll `get_ad_session` every ~20–30s until `completed`, `partial`, or `failed`.
3. Optional craft before pixels: `generate_strategies` → `generate_strategic_brief` → `generate_creative_ideas` → `create_ads`.

Tell the user the live `stage` while polling. Surface copy and Legend attribution from `get_ad_session`.

## Credits

Preflight every paid run with `get_credit_status`. If the run is blocked, call `recommend_credit_upgrade` (billing links only; it does not charge a card).

- `create_brand_from_url`: 0
- `create_ads`: 9 (refunded on failure)
- `generate_strategies` / `suggest_strategy_angles` / `generate_strategic_brief`: 1 each
- `generate_creative_ideas`: 3/legend legendary, 9/legend cannes-lion, +1/idea if imagery

This server cannot cancel subscriptions, issue refunds, or run admin/staff tools.

## When not to use (for one ad)

- Not `start_loop` — full autonomous marketing pass. Use `create_ads`.
- Not `list_campaigns` / `create_website_blueprint` — site/campaign workbench, not the ad pipeline.
- Not `create_media_plan` — budget/channel allocation, not the creative.
- Not `run_pulse_scan` for a cold URL — use `create_brand_from_url` (or `spot_trends_scan` for a name-only trend scan).
- Not `create_video` unless the user asked for a finished video ad. `animate_ad` only animates an existing Fast Ad still.

Prefer `nextActions` on each tool result over scanning the full catalog. Docs: https://www.adlegends.ai/mcp
