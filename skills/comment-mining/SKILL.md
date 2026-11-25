---
name: comment-mining
description: Mine the comments on TikTok, Instagram and YouTube posts for what viewers ask, want, object to and roast, in their exact words, and turn it into content ideas, FAQs and ad angles. Use when the user asks "what are people saying about X", "read the comments on this", "voice of customer", "audience pain points", "objections", or wants hooks in the audience's own language.
---

# Comment mining

The comments under a winning post are free customer research: the questions nobody answered, the objections, the jokes, the "do one about…" requests.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup and credits: the `mostly` skill.

## 1. Pick the posts

- The user gave links → use them.
- The user gave a topic, product or competitor → find posts first with `search_social_posts` or `get_account_outliers` (see `outlier-post-finder`) and pick the 3-5 with the most comments relative to views. Posts that beat their creator's usual numbers have the most engaged comment sections.

Each post costs 1 credit; say how many you'll read.

## 2. Read them

`get_post_comments` with `platform` and `post` (the `postUrl`; TikTok and YouTube also take the video id). Comments come most-liked first, with their like counts.

## 3. Sort what people say

| Bucket | Look for |
|---|---|
| Questions | "how", "where", "does it work for", "what's the song/brand" |
| Objections | price, doubt, "doesn't work", "scam", side effects, "too much effort" |
| Desires and requests | "need this", "do one about", "part 2" |
| Praise | what exactly they loved (a moment, a line, a tip) |
| Roasts and jokes | what they mocked; often the most memorable hook material |
| Buying intent | "link?", "where to buy", tagging a friend to buy |

Count how often each theme shows up and weight by comment likes. Keep quotes **verbatim**, with the post they came from.

## Output

1. **Top themes**, ranked, each with 2-3 verbatim quotes, like counts and the post link.
2. **Unanswered questions** → FAQ list.
3. **Objections** → what content would answer each one.
4. **Content ideas**: 5-10, each answering a real comment ("Reply to @…: does it work on oily skin?" is a proven format).
5. **Hook lines in the audience's own words.**

Say which posts the report covers; a few posts' comments are signal, not a survey. Offer to turn the ideas into posts (`carousel-generator`, `outliers-to-posts`).
