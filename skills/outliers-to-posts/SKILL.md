---
name: outliers-to-posts
description: The full loop - find posts that are beating their creator's usual numbers on TikTok, Instagram or YouTube, work out why they took off, make on-brand versions with Mostly, and schedule them as drafts. Use when the user wants "content that works", "copy what's going viral in my niche", "a week of posts based on what's working", "find outliers and make them for my brand", or a content plan grounded in real data. For research only, use outlier-post-finder; for one known post, clone-viral-carousel or remix-winning-post.
---

# Outliers to posts

Find what is working → understand why → make your version → schedule it. Every new post traces back to a real post that beat its creator's normal numbers.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup, brands and credits: the `mostly` skill.

## 1. Brief (one message, only if missing)

You need the brand, the niche and how many posts. Get the brand with `list_brands` and read its kit with `get_brand_kit` (voice, audience, products). If the user named competitors or creators, use them. Otherwise infer two or three search queries from the brand: how its audience would caption a post, not the brand's own category words ("iced coffee recipe", not "beverage brand").

Tell the user the research cost before running it: about 1 credit per platform per query, 1 per account.

## 2. Find outliers

- **Topic:** `search_social_posts` with `query`, and `platforms` limited to where the brand posts. Add `mediaType: "CAROUSEL"` when the user wants carousels. Results come ranked by how far each beat its creator's usual numbers.
- **Accounts:** `get_account_outliers` with `account` (handle or link), `platform` and `outliersOnly: true`.

Shortlist 3-8 posts. Read `signal`: `USUAL_VIEWS` with `times: 6.2` means 6.2× the creator's median views (the strongest evidence); `FOLLOWERS` means views per follower, used when no median is known. A carousel with no view count has no multiplier. Prefer posts from the last 90 days, formats the brand can actually make, and topics that fit its audience.

Show the shortlist as a table: link, account, views, multiplier, format, the hook (first line). Let the user cut it down if they want.

## 3. Understand each pick

1. `import_creative` with the result's `searchResult` object (free) → `creativeId`.
2. Carousel: `slides_breakdown`. Video: `video_breakdown` (shot by shot, with the spoken lines).
3. `get_creative_blueprint` for the reusable recipe: hook pattern, beats, pacing, why it worked.
4. For the best one or two, `get_post_comments` with `platform` and the `postUrl`: viewer questions and objections become angles and FAQ slides.

## 4. Make the brand's version

| Source | Want | Do |
|---|---|---|
| Carousel | Same look, new content | `clone_creative` (see the `clone-viral-carousel` skill) |
| Carousel or video | The structure, in the brand's own style | `remix_creative` with `creativeId`, `brandId`, an `angle`, `productIds` |
| Video | A talking-head UGC version | the `ugc-video` skill, using the blueprint's beats |

Remix and clone render straight away and spend credits; confirm the count first ("4 carousels, about N credits"). Take the creator's structure and pattern, never their photos, face or exact wording. Carousels render in 1-3 minutes: `get_slide_deck` (or `mostly slides get <id> --wait`) until every slide has an image.

## 5. Schedule

`list_integrations` to see connected accounts; if one is missing, `get_connect_link` and give the user the link. Then `create_post_draft` per post with `slideDeckId` (or `storyboardExportId` for a video), a native caption (hook in the first line, 3-5 hashtags), `platforms`, and `scheduledFor` as ISO 8601 with the user's UTC offset. Space posts out (one a day per platform is a good default). Drafts go live only after the user approves them in Mostly under **Publish**; say so.

## 6. Report

One table: source post (link, multiplier) → what was made (Studio link) → platforms and time. Then one line on what to check next week: `get_remix_results` shows how each remix did against the account's own median.
