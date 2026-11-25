---
name: carousel-generator
description: |
  Plan and render multi-slide carousels and slide decks with Mostly, edit or
  re-render single slides, and turn a finished deck into a TikTok / Instagram /
  LinkedIn / X / Facebook post.
  Use when: "carousel", "slide deck", "slides", "Instagram carousel",
  "TikTok photo post", "LinkedIn carousel", "turn this into slides",
  "post/schedule this carousel".
  NOT for: single images or video (use image-and-video-generation), product photo sets
  (use product-photoshoot).
---

# Carousel generator

**Calling Mostly:** the commands below use the `mostly` CLI. If the Mostly MCP tools are connected instead, call the same tool names directly (`mostly tools call X --args '{…}'` is the MCP tool `X` with those arguments). Setup, brands and credits: the `mostly` skill.

Plan and render a full carousel in one call; Mostly writes the slide copy, art-directs every slide and renders the images in the background. All calls go through `mostly tools call`, plus `mostly slides get --wait` to collect the result.

## Step 0 — Bootstrap (CLI only; skip with MCP)

`mostly` on `$PATH` (`npm i -g mostly`), then `mostly auth status`. If not logged in, ask the user to run `mostly auth login` themselves. For a branded deck, get the brand id with `mostly brands list`.

## 1. Agree the storyline first (one short message)

- **Brief request** ("make a carousel for my brand"): pitch one angle and a slide-by-slide outline (hook → problem → insight → proof → payoff/CTA), then ask "Good to generate?" Structural templates: [references/slide-templates.md](references/slide-templates.md).
- **Specific request** (topic, slide count, outline given): skip straight to generating.
- Don't run a questionnaire. Infer platform and tone from the request and the brand.

## 2. Generate the deck

Put the agreed outline in `prompt`, slide by slide, with the substance (facts, steps, examples). Let Mostly choose the visual style unless the user named one.

```bash
mostly tools call generate_slide_deck --args '{
  "prompt": "Topic: 5 onboarding mistakes killing SaaS retention\nSlide 1 (cover): …\nSlide 2: …\nSlide 5 (CTA): …",
  "aspectRatio": "3:4",
  "brandId": "<brandId or omit>",
  "brandUsage": "full",
  "productIds": ["<productId>"]
}'
```

- `aspectRatio`: `3:4` for TikTok/Instagram carousels (default), `1:1` square, `16:9` presentation decks. Supported ratios depend on the image model; before using anything else, check `mostly models get <modelId>` (the deck's default model is marked in `mostly tools get generate_slide_deck`).
- `style`: only if the user asked (e.g. "Risograph zine", "Technical blueprint").
- `referenceImages`: image URLs to feature or style from (upload a local file first with `mostly generate …` or pass an https URL).
- `brandUsage`: `full` (voice + products + palette), `voice_only`, or `none` for an unbranded topic.
- Omit `brandId`, `productIds` and `style` rather than sending empty values.

The response has `slideDeckId`. Then wait for rendering (usually 1–3 minutes):

```bash
mostly slides get <slideDeckId> --wait
```

It prints each slide's headline and image URL, plus a Studio link. Share the Studio link: the user can review and edit the slides there.

## 3. Edit slides

```bash
# Inspect (compact outline, or one slide in full)
mostly tools call get_slide_deck --args '{"slideDeckId":"<id>","targetSlideNumber":3}'

# Change copy/prompt directly; add "generateAsset": true to re-render it
mostly tools call update_slide --args '{"slideDeckId":"<id>","slideNumber":3,"headline":"…","generateAsset":true}'

# Let Mostly rewrite a slide's copy and art direction from deck context (no image credits)
mostly tools call generate_slide_content --args '{"slideDeckId":"<id>","slideNumber":3}'

# Re-roll one slide's image (spends credits)
mostly tools call generate_slide_asset --args '{"slideDeckId":"<id>","slideNumber":3}'

# Insert a slide: create the slot → write its content → render
mostly tools call create_slide --args '{"slideDeckId":"<id>","insertAfterSlideNumber":2,"headline":"…"}'
mostly tools call generate_slide_content --args '{"slideDeckId":"<id>","slideNumber":3}'
mostly tools call generate_slide_asset --args '{"slideDeckId":"<id>","slideNumber":3}'

# Remove a slide
mostly tools call delete_slide --args '{"slideDeckId":"<id>","slideNumber":4}'
```

After any re-render, `mostly slides get <id> --wait` again.

## 4. Turn it into a post

Posting to real accounts needs the user's approval in Mostly, so the CLI creates a **draft** only.

1. Make sure every slide has rendered (`mostly slides get <id>`).
2. `mostly tools call list_integrations` and check the platforms are connected. If one isn't: `mostly tools call get_connect_link --args '{"platform":"INSTAGRAM"}'` and give the user the link.
3. Write a native caption (hook in the first line, 3–5 relevant hashtags) and create the draft:
   ```bash
   mostly tools call create_post_draft --args '{
     "slideDeckId": "<id>",
     "platforms": ["TIKTOK", "INSTAGRAM"],
     "content": "…",
     "scheduledFor": "2026-10-27T09:00:00+08:00"
   }'
   ```
   Platforms: `TIKTOK`, `INSTAGRAM`, `TWITTER` (X), `LINKEDIN`, `FACEBOOK`. `scheduledFor` is ISO 8601 with the user's UTC offset; omit it to post right after approval.
4. Tell the user the draft is ready to review and approve in Mostly under **Publish → Drafts** (`<server>/publish`). Its response mentions `publish_post`: that tool isn't available from the CLI, so don't try to call it.

Slides post in deck order. Instagram shows 4:5 to 1.91:1, so taller slides get side bars there; mention this only if the user asks about cropping.
