---
name: clone-viral-carousel
description: Recreate a TikTok or Instagram carousel's look - layout, typography, colours, spacing - slide by slide, with the user's own content, using Mostly. Use when the user shares a carousel and says "make one like this", "same style but about X", "clone this carousel", "copy this layout for my brand", or wants slides that look like a specific post. For a looser on-brand take on a post's structure, use remix-winning-post.
---

# Clone a viral carousel

Each new slide is rendered with one original slide attached as its visual reference, from a prompt you write. The look carries over; the content is the user's.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup and credits: the `mostly` skill.

## 1. Bring in the original

`import_creative` with the carousel's `url` (TikTok or Instagram), or the `searchResult` from `search_social_posts` / `get_account_outliers`. Then `slides_breakdown` with the `creativeId`: you need to know what every original slide shows (layout, text blocks, images) before writing prompts.

## 2. Agree the content (one message)

Unless the user already gave it, propose the new slide-by-slide text: same number of slides and the same job per slide (hook, points, payoff, CTA), the user's topic. Ask "Good to render?" Rendering spends image credits per slide.

## 3. Write the slides

One entry per new slide, in order:

- `sourceSlide`: the 1-based number of the original slide whose look this one copies. One original can be the source for several new slides (the usual case: one layout for all the middle slides).
- `prompt`: say to **recreate the attached reference slide's layout, typography, colours and spacing**; then quote **every line of on-slide text** in double quotes; then describe the photo, logo or graphic that goes in it.
- `headline`: the slide's main line, for the deck outline.

Use the real people, companies, products and logos the topic is about, named exactly, and keep claims about them factual. Never reuse the original creator's face, photos or exact copy.

## 4. Clone

`clone_creative` with `creativeId` (or `url`), a 2-5 word `title` and `slides`. Leave `aspectRatio` out to match the original's shape.

```json
{
  "creativeId": "<id>",
  "title": "Cold brew mistakes",
  "slides": [
    {
      "sourceSlide": 1,
      "headline": "5 cold brew mistakes",
      "prompt": "Recreate the attached reference slide's layout, typography, colours and spacing. Headline: \"5 cold brew mistakes you're making\". Background: a sweating glass of cold brew on a kitchen counter, morning light."
    },
    {
      "sourceSlide": 2,
      "headline": "Grinding too fine",
      "prompt": "Recreate the attached reference slide's layout, typography, colours and spacing. Title: \"1. Grinding too fine\". Body: \"Use a coarse grind, like raw sugar.\" Photo: a hand holding coarse coffee grounds over a jar."
    }
  ]
}
```

On the CLI, save it as `clone.json` and run `mostly tools call clone_creative --args-file clone.json`.

## 5. Collect and hand over

Slides render in 1-3 minutes: `get_slide_deck` with the `slideDeckId` (CLI: `mostly slides get <id> --wait`). Compare each new slide with its source; fix one with `update_slide` (`generateAsset: true` re-renders it) or `generate_slide_asset`. Share the Studio link, then offer to schedule it (`schedule-posts`).
