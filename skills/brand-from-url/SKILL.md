---
name: brand-from-url
description: Cold-start an Ad Legends brand from a website URL. Use when the user points at a site and there is no brandId yet. Calls create_brand_from_url; do not invent a discovery tool.
---

# Brand from URL

`create_brand_from_url` is the cold-start verb. Give a URL; the server reads the rendered site (colors, fonts, logo, voice), creates a brand, and returns a real `brandId` plus `nextActions` (`get_brand` / `create_ads` / `create_media_plan`).

If you just connected or are unsure, call `get_started` with `brandUrl` first and follow `nextActions`.

## Steps

1. Confirm the website URL with the user.
2. Call `create_brand_from_url` with `url` (e.g. `https://acme.com`).
   - Default `persist: true` saves to Brand Memory (needs `brands:write` and a key **without** a brand allowlist).
   - `persist: false` is a read-only preview (`brands:read` only).
3. On success, keep the `brandId`. Call `get_brand` if you need the overview before generating.
4. To make an ad next: `get_credit_status` (`requiredCredits: 9`) → `create_ads` → poll `get_ad_session`.

Takes ~20–90s. Keep the call alive if the client supports progress. The URL is SSRF-validated.

## Errors and limits

A success **always** returns a `brandId`, or a typed error (for example `payment_required` at the brand limit) — never a silent “no brand”. A brand-scoped key cannot create new brands.

Credits: `create_brand_from_url` is free. Later generation is metered; preflight with `get_credit_status`. If blocked, `recommend_credit_upgrade`.

Do not invent tools (`discover_brand`, `scrape_brand`, `analyze_website`). Docs: https://www.adlegends.ai/mcp
