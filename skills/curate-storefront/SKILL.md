---
name: curate-storefront
description: Curate one person's clothing storefront from recommendations their bot writes. Use when they want new picks, a taste check, or the current rack. Call list_feedback before writing recommendations.
---

# Curate my storefront

The storefront is only what you write for this signed-in person with `add_recommendations`. There is no shared catalog. When `get_storefront` is empty, they still need recommendations from you.

## Before you write recommendations

Call `list_feedback` before every `add_recommendations`. On the first run, omit `since`. After that, pass the `cursor` you received as `since` so you only fetch newer reactions. Also call `get_taste_summary` and use `learned`: recent reasons grouped by brand, category, and price.

Do not invent a price, stock status, review, rating, or size. Unknown stays unknown. Do not download a retailer photo. An image URL is stored only when you already have an http or https URL.

## When to use

- They want new pieces on the rack.
- They want to see or change how Muse describes their taste.
- They want a brand or style name added or removed.
- They want the current storefront.
- They found a piece and want it saved.

## Tools

- `list_feedback` returns this person's reactions: `save`, `unsave`, `dismiss`, `purchase`, `closet_add`, `like`, and `rating`. Each event has `item_id`, `action`, `reason`, `reasons` (chips), `note`, and `created_at`. Optional `since` is the previous cursor. A `purchase` event is an approval note. It does not mean an order was placed or payment was taken.
- `get_taste_summary` reads their short summary and `learned` reasons by brand, category, and price. The summary is empty when they have not written one.
- `update_taste_summary` replaces the whole summary. Call `get_taste_summary` first, then send the full replacement they agreed to. Send an empty string only when they ask to clear it. Do not invent taste.
- `list_brands`, `add_brand`, and `remove_brand` change brand names they added. `name` is the label. Adding a brand does not look up a catalog or download photos.
- `list_styles`, `add_style`, and `remove_style` work the same way for style names.
- `get_storefront` returns only this person's bot-written recommendations. Optional `limit` is an integer from 1 to 100. Dismissed and expired recommendations are left out. `empty` means there is nothing to show until you write some. A null price means unknown. Stock, reviews, and ratings are unknown. Nothing is buyable. A link is the retailer page. Opening it is not a purchase.
- `add_recommendations` writes a batch of 1 to 25 items. The same retailer URL keeps the same `id`, so a later dismissal maps back to that recommendation.
- `clear_recommendations` takes their current bot recommendations off the storefront. Ids stay so earlier feedback still matches.
- `save_item` saves one item they are adding. This is not a purchase.

## Writing recommendations

Send `add_recommendations` with `items`. Each item needs:

- `url`, the http or https retailer page
- `title`
- `category`
- `why_picked`, why this piece fits what you learned
- `source`, a short label for where the pick came from
- `brand` when you know it
- `price` only when you know it, as `{ "amount": "<decimal>", "currency": "<ISO code>" }`. Omit `price` when it is unknown.
- `image_url` only when you already have an http or https image URL. Do not fetch it.
- `expires_at` only when the pick should leave the rack at a known ISO-8601 time

Muse is free. Do not mention a paid tier. Do not place an order or take payment.
