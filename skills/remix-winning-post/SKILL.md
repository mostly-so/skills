---
name: remix-winning-post
description: Turn a proven viral post into a new on-brand carousel with Mostly - the original's hook pattern, beat order and pacing, with the brand's voice, palette and products, and none of the creator's copy or photos. Use when the user says "do this but for my brand", "remix this post", "make our version of this", "adapt this format", or picks an outlier to build on. For the same visual look, use clone-viral-carousel.
---

# Remix a winning post

The source's blueprint (hook pattern, beats, pacing, style) becomes the structure; the brand kit supplies everything else. The result is a carousel that rendered straight away.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup and credits: the `mostly` skill.

## 1. Get the source and the brand

- Source: `import_creative` with the post's `url`, or the `searchResult` from a search or outlier result → `creativeId`. Videos and carousels both work; the remix is a carousel.
- Brand: `list_brands` → `brandId`. Products to feature: `list_brand_products` → ids.

## 2. Check the recipe (recommended)

`get_creative_blueprint` with the `creativeId` shows the hook pattern, the beats and why it worked (first call ~30 s, then cached). Use it to pick an `angle` that fits the pattern, e.g. the source "I tried 5 viral coffee hacks" becomes "I tried 5 ways to make cold brew at home" for a coffee brand.

## 3. Remix

`remix_creative` with:
- `creativeId`
- `brandId`
- `angle`: the topic for the new piece; leave it out to let the brand drive it
- `productIds`: products to feature
- `aspectRatio`: optional; `3:4` suits TikTok and Instagram carousels

It renders like a new slide deck and spends credits; confirm when doing several. The response has the `slideDeckId`.

## 4. Review and ship

`get_slide_deck` (CLI: `mostly slides get <id> --wait`) until every slide has an image. Fix single slides with `update_slide` or `generate_slide_content` (see `carousel-generator`). Share the Studio link and offer to schedule it (`schedule-posts`).

Later, `get_remix_results` shows how published remixes did against the account's own median, per source format: the feedback loop for what to remix next.
