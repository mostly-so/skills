---
name: viral-post-breakdown
description: Take one TikTok, Instagram, YouTube post or Meta ad apart - hook, beats, shot-by-shot or slide-by-slide structure, transcript, pacing, on-screen text, CTA and why it worked - and turn it into a reusable template. Use when the user shares a post or ad link and asks "why did this go viral", "break this down", "analyse this video/carousel/ad", "transcribe this", or "give me the formula".
---

# Viral post breakdown

One post, understood well enough to make another like it.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup and credits: the `mostly` skill.

## 1. Bring the post in

`import_creative` with `url`: a TikTok post, an Instagram post or reel, or a Meta Ad Library ad (`facebook.com/ads/library/?id=…`). From a search result, pass its `searchResult` object instead (free). You get a `creativeId` and the media.

For context on how unusual the post is, `get_account_outliers` on its author shows the account's median views (1 credit).

## 2. Break it down

| Post | Call |
|---|---|
| Video or video ad | `video_breakdown` (shot-by-shot timeline: visuals, spoken lines, on-screen text, production notes); `transcribe` for the plain transcript |
| Carousel or image post | `slides_breakdown` (each slide's role, headline, visual, takeaway) |
| Either | `describe_thumbnail` for the cover or first frame |
| Either | `get_creative_blueprint`: hook verbatim plus a `{placeholder}` pattern, ordered beats, pacing, style, CTA, why it worked, how to remix it |

Each runs once per post and is cached after; the first run spends credits.

`get_post_comments` with the post link adds what viewers reacted to (1 credit).

## Output

1. **The hook**: verbatim, then as a reusable pattern, and why it stops the scroll.
2. **Structure**: the beats in order with timestamps or slide numbers and what each does (problem, proof, twist, payoff, CTA).
3. **Craft**: pacing, shot types, on-screen text style, sound, length or slide count.
4. **Why it worked**: 3-5 reasons, each tied to a moment in the post (and to comments, if read).
5. **Template**: the beat sheet with `{placeholders}`, ready to fill for another brand.

Offer to make one: `clone-viral-carousel` for the same look, `remix-winning-post` for an on-brand take, `ugc-video` for a video version.
