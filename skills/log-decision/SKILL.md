---
name: log-decision
description: Read why the person saved, dismissed, liked, or approved a piece, and record a reason they just gave. Use before writing new recommendations. A save or purchase note is not an order.
---

# Log why I saved or dismissed something

Read the person's own reactions. Do not invent why they kept or passed on a piece, and do not contact a retailer.

## Before new recommendations

Call `list_feedback` before `add_recommendations`. Pass the previous `cursor` as `since` when you have one. Use the reasons, chips, and notes in the next picks. `get_taste_summary` also groups recent reasons by brand, category, and price.

## When to use

- You are about to write recommendations and need their latest reactions.
- They want to save a piece and say why.
- They want to dismiss a piece and say why.
- They want the list of saved items, including ones they later dismissed.

## Tools

- `list_feedback` returns events since an optional cursor. Actions are `save`, `unsave`, `dismiss`, `purchase`, `closet_add`, `like`, and `rating`. Each event includes `item_id`, `action`, `reason`, `reasons`, `note`, and `created_at`. Dismiss events carry the reason chips in `reasons` and any free-text note in `note`. A purchase event is an approval note. It does not place an order or take payment.
- `save_item` keeps an item they are adding. Required fields are `url` and `title`. Include `price` or `image_url` only when they supplied them. Omit `price` when it is unknown. Saving does not look up a price, stock, or reviews, and it does not fetch an image. Saving is not a purchase.
- `dismiss_item` requires `reason`, in their words, up to 500 characters. Also send `reasons` when they named chips, and `note` for any extra sentence. Send `item_id` from `get_storefront` or `list_feedback` when you have it, or `url` when you do not. The same id the bot wrote is the id a dismissal uses. The item leaves the storefront and stays in their history.
- `list_saved` lists saved items and whether each one was also dismissed, with `dismissal_reason` when they wrote one.

## How to log it

1. Use their words for the reason. Ask once if they dismissed something and did not say why.
2. Prefer `item_id` from `list_feedback` or `get_storefront` when the piece is already stored.
3. After a save, repeat the title and that it is saved, not purchased.
4. After a dismissal, repeat the reason you stored. Do not soften it into a different reason.
