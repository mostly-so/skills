---
name: mostly-product-photoshoot
description: |
  Product photography with Mostly via the `mostly` CLI: studio packshots,
  lifestyle scenes, close-ups, conceptual/splash shots, hero banners, and
  coordinated ad sets, from a product photo or a saved brand product.
  Use when: "product photos", "photoshoot", "packshot", "white background",
  "lifestyle shot", "Shopify/Amazon listing images", "product ads", "ad set",
  "photos of my product".
  NOT for: non-product visuals or video (use mostly-generate), carousels
  (use mostly-slides).
argument-hint: "[product photo path or product name] [style]"
allowed-tools: Bash
---

# Mostly Product Photoshoot

Shoot products with `mostly generate` using an image model and the product as a reference. This skill tells you what to write in the prompt and which options to pass.

## Step 0 — Bootstrap

Same as mostly-generate: `mostly` on `$PATH` (`npm i -g mostly`), then `mostly auth status`. If not logged in, ask the user to run `mostly auth login` themselves.

## 1. Get the product

1. **User gave a photo** → pass it with `--image ./photo.png` (repeat `--image` for more angles).
2. **User named a product** → `mostly tools call list_brand_products`, match it, pass `--product <id>`. Its photos lock packaging/labels and its facts are added for you.
3. **Neither** → ask once: "Which product? Send a photo path or name one from your brand." Don't invent a product unless they say so.

## 2. Pick the shot

Write the prompt as a photographer's brief: subject → surface/scene → lighting → lens/angle → mood.

| User wants | Prompt focus | `--aspect-ratio` |
|---|---|---|
| Studio / packshot / white background / listing | Product alone, seamless backdrop or pedestal, softbox key + rim light, clean reflections, label facing camera | `1:1` listing, `4:5` feed |
| Lifestyle / in use | Believable environment (kitchen counter, vanity, desk, gym bag), natural window light, audience-matched props, hands optional | `4:5` feed, `9:16` stories |
| Close-up / texture | Macro on material, drip, cap mechanism; shallow depth of field | `1:1` or `4:5` |
| Conceptual / splash / levitating | Floating product or splash, frozen motion, bold brand-color backdrop | `1:1` or `4:5` |
| Hero banner / website header | Wide composition, product off-center, empty space for a headline | `16:9` |

Lighting and lens vocabulary: [references/lighting.md](references/lighting.md), [references/optics.md](references/optics.md).

- **Ad set / "a few different shots":** run one `mostly generate` per angle with *different* prompts (studio hero, lifestyle in use, texture close-up, conceptual). Keep the aspect ratio and palette the same so the set looks coordinated. Run them in parallel (`&` then `wait`).
- **"More options of this one":** same prompt with `--count 3`.
- Use `--resolution 2K` for anything going on a store or an ad account.

```bash
mostly generate <imageModel> \
  --prompt "Amber glass serum bottle on a travertine pedestal, seamless warm-grey backdrop, overhead softbox at 45°, subtle rim light, 85mm f/2.8, label facing camera" \
  --product <productId> --aspect-ratio 1:1 --resolution 2K --wait
```

## 3. Ask little

- Product and use are clear → generate immediately.
- Otherwise ask at most 2 short questions with options, e.g. "Style? Studio / Lifestyle / Conceptual" and "Where will it run? Listing / Instagram / Ads / Website".
- Brand colors and mood come from the brand (`mostly tools call get_brand_kit`); don't ask for them.

## 4. Deliver

- List the URLs with a few words each ("studio hero", "lifestyle, kitchen").
- Offer the next step: more variants, another scene, animate one (`mostly generate <videoModel> --start-image <url> …`, see mostly-generate), or a carousel (mostly-slides).
