---
name: ugc-video
description: Make a talking-head UGC video with Mostly - script, AI avatar takes with lip-synced voice, jump cuts, captions, a hook card, product overlays, music - exported as one MP4 and ready to post. Use when the user wants a UGC ad, a creator-style video about their product, "a TikTok of someone talking about my product", or wants to recreate a viral talking-head video for their brand. Not for carousels or single image-to-video clips (image-and-video-generation).
---

# UGC video

One person talking to camera about a product, edited the way creators edit: long takes, cut tight, captions on, product on screen when it's mentioned. Mostly renders the takes; you write and edit through the storyboard tools.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup and credits: the `mostly` skill.

**Price before every render or export.** Call `render_storyboard`, `generate_storyboard_preview` or `export_storyboard` with `maxCredits: null` to get the price, tell the user, and only on a yes call again with `maxCredits` set. Edits (cuts, trims, captions, overlays, music) are free.

## 1. Script (one message)

- From a viral video: `import_creative` + `video_breakdown` (see `viral-post-breakdown`) and keep its beat structure with the brand's product and words.
- From scratch: `get_brand_kit` and `list_brand_products`; hook in the first 2 seconds, one problem, the product as the fix, one proof point, a CTA.

Write the beats, each 8-12 seconds of speech with the line in quotes, and ask "Good to make?"

## 2. Cast

`list_avatars` for the brand's avatar (same face in every take). None → `list_avatars` with `source: "presets"` for ready-made people, or `generate_avatar` to design one.

## 3. Storyboard and render

`generate_storyboard` with `beats` (your agreed lines, word for word, in order, with seconds), `prompt` (product, audience, angle), `aspectRatio: "9:16"`, `productIds`, `avatars`. Writing scenes costs nothing; it takes about a minute.

Optional: `generate_storyboard_preview` for still frames first (a cheap check of the face and product before the big render).

`render_storyboard` (price first). Video takes a few minutes per shot. Render one long take per beat and cut it afterwards; never one clip per sentence.

## 4. Edit (free)

- `get_storyboard` with `transcripts: true` (or `words: true`) to see what was said and when.
- `cut_storyboard_shot` with `cuts` to drop pauses, fillers and fluffed lines; `update_storyboard_shot` with `trim` for dead air at the start and end.
- `update_storyboard` with `captionStyle` (presets such as `viral-pop`, `hype-highlight`) and `hook` (text on the first 2-3 seconds).
- `list_audio_library` → `update_storyboard_scene` `music` on the first scene (keep it quiet under speech); `sfx` on a few cuts.
- `find_overlay_media` → `update_storyboard_scene` `overlays` to show the product over the line that mentions it, at the top, 1.5-4 s.

## 5. Review, export, post

`review_storyboard`, then look at the frames yourself: same face throughout, the real product, no garbled text. Tell the user what you'd fix before re-rendering anything. Then `export_storyboard` (price first) and `get_storyboard_export` until it is done; share the link. To post, pass the `storyboardExportId` to `create_post_draft` (see `schedule-posts`).

## Rules

- Proof is real or absent: reviews, ratings and sales counts on screen come from the user's own screenshots, never generated or stock.
- Re-render only what changed: edits mark shots stale, and `render_storyboard` with `scope: "stale"` redoes just those.
