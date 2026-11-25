---
name: ad-library-teardown
description: Tear down a competitor's or a category's active Facebook and Instagram ads from the Meta Ad Library - which ads have run longest and been scaled into variations, their hooks, offers, CTAs, landing pages and creative formats - and turn it into ad ideas to test. Use when the user asks "what ads is X running", "show me competitor ads", "Meta / Facebook ad library", "what ads are working for brands like mine", or wants ad angles to test.
---

# Ad library teardown

An ad that is still running after weeks is one that is paying off: brands kill losers fast. Mostly searches the Meta Ad Library and puts the longest-running ads first.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup and credits: the `mostly` skill.

## 1. Search

`search_meta_ads` with `query`: an advertiser's name ("Liquid Death"), a product ("collagen powder") or a claim people would put in ad copy ("sleep better"). 1 credit per search; repeats within 24 hours are free. For several competitors, run one search each and say the total cost first.

Each ad comes with `advertiser`, `body` (copy), `title`, `ctaText`, `linkUrl` (landing page), `mediaType`, `startDate`, `daysRunning`, `variationCount`, `publisherPlatforms` and `adLibraryUrl`.

## 2. Read the signals

- **`daysRunning`**: 30+ days on an active ad is a strong sign it works; 90+ is a proven winner.
- **`variationCount`**: many ads sharing one creative means it is being scaled.
- Keyword searches return other advertisers too; filter by `advertiser` when the user wants one brand.

## 3. Study the best 3-5

`import_creative` with the ad's `adResult` object (free) → `creativeId`. Then:
- Video ads: `video_breakdown` (shot by shot, spoken lines, on-screen text) or `transcribe`.
- Image and carousel ads: `slides_breakdown`, or `describe_thumbnail` for a single image.
- `get_creative_blueprint` for the reusable recipe.

## Output

1. **Ad table**: advertiser, format, days running, variations, hook (first line of copy), offer, CTA, landing page, Ad Library link. Longest running first.
2. **Angles**: the 3-5 messages that keep showing up (price, pain, social proof, founder story, before/after…), with the ads behind each.
3. **Hooks and offers**: verbatim, then as reusable patterns.
4. **Formats**: UGC, static, carousel, demo; which ones the long-runners use.
5. **Test plan**: 3-5 ads for the user's brand to test, each tied to the evidence: angle, hook, format, offer.

Offer to make them: `remix-winning-post` for a carousel, `product-photoshoot` for static ad sets, `ugc-video` for a UGC ad. The Ad Library shows active ads, not spend or results; say so.
