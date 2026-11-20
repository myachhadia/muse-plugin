# Privacy

Muse stores notes for the signed-in person only. This package does not contain a wardrobe, a catalog, retailer photos, or secrets.

## MCP server

The hosted server is `https://muse-mcp.mya-chhadia.workers.dev/mcp`. A person connects by signing in with their own Muse account over OAuth. There is nothing to self-host. Do not put a token, key, or password in `.mcp.json` or `mcp.json`.

## What the tools may store

When a client calls the Muse MCP server, the signed-in person can store:

- a short taste summary they wrote
- brand names and style names they added
- items they added, each with a page URL and title, and a price or image URL only when they supplied one
- a save, or a dismissal with their reason
- a purchase approval note
- closet items they added, with a title and an optional page URL or note

Unknown price, stock, reviews, and ratings stay unknown. The server does not look up a catalog or download a photo.

## What this package refuses

- No payment card, bank, address, or account credentials.
- `record_purchase` records an approval note. It does not place an order, reserve stock, or take payment. `order_placed` and `payment_captured` stay false. Checkout happens on the retailer site.
- Opening a retailer page is not a purchase.
- This directory is safe to publish on its own. The private Muse repo keeps the rack, reference photos, catalog files, and local secrets.
