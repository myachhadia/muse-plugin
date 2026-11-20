---
name: plan-outfit
description: Plan an outfit from closet items the person added, and record a purchase approval note when they already decided on a retailer site. Use when they ask what to wear from what they own. Never place an order or take payment.
---

# Plan an outfit from my closet

Use closet items the person added. Do not invent garments, pull a catalog, or treat a plan as an order.

## When to use

- They want an outfit from what they already own.
- They want to add something they own to the closet.
- They approved a purchase, or already bought on a retailer site, and want that noted.

## Tools

- `list_closet_items` lists closet items they added.
- `add_closet_item` adds something they own. Required field is `title`. Optional fields are `url`, `note`, `item_id`, and `purchase_record_id`. Adding a closet item does not buy it.
- `record_purchase` records an approval note, or a note that a purchase already happened on the retailer site. Send `item_id` or `url`, plus `title` when the URL is new, and `note` when they offered one. The result keeps `order_placed` false and `payment_captured` false.

## How to plan

1. Read `list_closet_items` before you suggest an outfit. If the closet is empty, say so and ask what they want to add. Do not fill the gap with catalog pieces.
2. Suggest combinations from those closet titles. Say when a piece is missing for the occasion instead of inventing one.
3. A retailer link, if they stored one, is only a page. Opening it is not a purchase.

## Purchase notes

Use `record_purchase` only after they say they approve a purchase or that they already bought it on the retailer site. Tell them the note does not place an order and does not take payment. Checkout stays on the retailer site. Do not ask for payment details.
