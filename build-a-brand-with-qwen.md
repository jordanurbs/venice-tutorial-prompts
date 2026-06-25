# Build your brand with Qwen 3.7 + Qwen Image 2 Pro — prompt pack

Copy-paste prompts to build a full brand on [Venice](https://venice.ai): a world, a product, an explainer, and a launch — all visually consistent. Fill in anything in `[BRACKETS]`, then run top to bottom.

**Three tools you'll use:**
- **`qwen-3-7-plus`** — writes your copy, and can *see* images (your art director)
- **`qwen-image-2-pro`** — generates an image
- **`qwen-image-2-pro-edit`** — edits an existing image to match it (your consistency engine)

> **The two consistency levers:** (1) paste the same **style token** into every image prompt, and (2) use the **edit** tool with a reference image to keep characters, layouts, and palettes identical. Master these two and everything looks like one brand.

---

## Step 0 — Set up once

**Fill in your brand basics** (keep this handy; you'll paste it a few times):

```
- Brand name: [YOUR BRAND NAME]
- Category: [WHAT YOU SELL / DO]
- Vibe in 3 words: [e.g. bold, playful, premium]
- Audience: [WHO IT'S FOR]
```

**Build your style token** (your visual fingerprint — paste into every image prompt):

```
[ILLUSTRATION OR PHOTO STYLE, e.g. flat editorial illustration], limited [3–5]-color palette ([HEX], [HEX], [HEX]), [TEXTURE, e.g. subtle grain], [SHAPE LANGUAGE, e.g. clean geometric shapes], [LIGHTING], no gradients, consistent look
```

> Tip: don't have a palette yet? Ask `qwen-3-7-plus`: "Suggest a 5-color hex palette for a [VIBE] [CATEGORY] brand and explain each color in a few words." Then lock those hex codes into your style token.

---

## Step 1 — Build your brand world

### 1.1 Brand bible — `qwen-3-7-plus`

```
You are a senior brand strategist. Create a complete brand bible. Be specific and decisive — no hedging.

Brand input:
[PASTE YOUR BRAND BASICS FROM STEP 0]

Deliver, with clear headers:
1. Positioning — one sentence on who it's for and why it's different.
2. Voice — 3 adjectives, then 3 "we say / we don't say" pairs.
3. World & lore — a short paragraph establishing the brand's world (place, mood, ritual).
4. Visual language — palette as hex, illustration/photo style in one line, and 3 recurring motifs.
5. Mascot or icon character sheet — name, what it is, personality (3 traits), a description detailed enough to redraw consistently, palette (hex), and 3 visual do's / 3 don'ts.

Keep it tight and usable.
```

### 1.2 Launch thread — `qwen-3-7-plus` (same chat)

```
Using the brand bible above, write a 10-part launch thread introducing the brand's world.
- Each part its own post, under 280 characters, numbered 1/10 … 10/10.
- Part 1 is a scroll-stopping hook; part 10 ends on a CTA.
- Stay in the brand voice throughout. Introduce the mascot/icon by part 3.
- No hashtags, minimal emoji.
```

### 1.3 Generate your mascot/icon — `qwen-image-2-pro`

```
[DESCRIBE YOUR MASCOT OR ICON from the character sheet], centered, plain background, full subject visible, generous margins.
Style: [PASTE YOUR STYLE TOKEN]
```

### 1.4 Build a matching set — `qwen-image-2-pro-edit`

Use the image from 1.3 as the **reference**, then run each as a separate edit:

```
Keep this exact character — same subject, proportions, line weight, and palette. New pose/scene: [DESCRIBE]. Same background treatment and margins.
```

Repeat with different `[DESCRIBE]` values for as many poses/scenes as you need. For a scene with no character: "Environment only (no character): [DESCRIBE], same palette, texture, and style."

---

## Step 2 — Spin up a product

### 2.1 Product brief — `qwen-3-7-plus`

```
Here is my brand bible: [PASTE THE BIBLE FROM 1.1].

Write a product brief for a new product that fits this world.
Product: [WHAT YOU'RE LAUNCHING].
Deliver:
1. Product/line name + 3 variant names (each with a one-line story in brand voice).
2. Target customer + the core value proposition (one sentence).
3. Packaging/landing copy — headline, product name, 1-line descriptor, and a 40-word story.
4. A one-line art-direction note for the product visual that matches our visual language.
```

### 2.2 Generate hero + packaging visuals — `qwen-image-2-pro`

Hero shot:
```
Product hero shot of [YOUR PRODUCT] for the brand "[BRAND NAME]", in [SETTING]. Premium, clean, lots of negative space.
Style: [PASTE YOUR STYLE TOKEN]
```

Packaging/label (quote exact text so it spells correctly):
```
Flat packaging/label design for [PRODUCT]. Exact text, spelled correctly:
- Top: "[BRAND NAME]"
- Center (large): "[PRODUCT NAME]"
- Small line: "[ONE-LINE DESCRIPTOR]"
- Bottom: "[SIZE / DETAIL]"
Include [A BRAND MOTIF]. Clean layout with clear hierarchy.
Style: [PASTE YOUR STYLE TOKEN]
```

### 2.3 Lock product shots to your brand — `qwen-image-2-pro-edit`

Reference a Step-1 illustration, then:
```
Match the palette, texture, and style of this reference exactly. Apply it to the attached product image so it belongs to the same brand world. Keep any text unchanged.
```

---

## Step 3 — Teach something (build authority)

### 3.1 Five-part explainer — `qwen-3-7-plus`

```
In my brand voice, write a 5-part thread explaining [A TOPIC YOUR AUDIENCE CARES ABOUT] — clear for a beginner, accurate enough to earn respect.
- One key idea per part.
- Each part under 280 characters, numbered 1/5 … 5/5.
- End each part with a one-line caption I can use for a diagram, prefixed "DIAGRAM:".
```

### 3.2 One diagram per part — `qwen-image-2-pro`

```
A clean labeled infographic diagram explaining "[PASTE THE DIAGRAM CAPTION]".
Show [THE CONCEPT VISUALLY]. Include 3–4 short callout labels with correctly spelled text. Horizontal layout, lots of whitespace.
Style: [PASTE YOUR STYLE TOKEN]
```

### 3.3 Lock the diagram style across all five — `qwen-image-2-pro-edit`

Reference diagram #1, then for diagrams 2–5:
```
Match this reference's layout, label style, palette, and texture exactly. Same visual language, new content: [DESCRIBE THIS DIAGRAM]. Keep labels clean and correctly spelled.
```

---

## Step 4 — Launch it (campaign kit)

### 4.1 Headline + carousel copy — `qwen-3-7-plus`

```
Using my brand bible and product, write a launch campaign kit.
Deliver:
1. Campaign concept — one line.
2. Headline — under 8 words, in brand voice.
3. Five carousel slides — each with a 2–4 word on-image title and a one-line caption.
   Arc: hook → problem → product → benefit/proof → CTA.
4. One closing CTA line.
```

### 4.2 Generate hero + 5 carousel images — `qwen-image-2-pro`

Hero:
```
Launch hero image for "[BRAND NAME]". Headline text on image, spelled exactly: "[PASTE HEADLINE]". [SCENE], with a small brand motif. Strong negative space for the headline.
Style: [PASTE YOUR STYLE TOKEN]
```

Each slide (run 5×):
```
Social carousel slide, square 1:1. On-image title, spelled exactly: "[PASTE SLIDE TITLE]". Simple supporting illustration for: [SLIDE CONCEPT]. Consistent margins so all 5 slides line up as a set.
Style: [PASTE YOUR STYLE TOKEN]
```

### 4.3 Lock the carousel to your brand — `qwen-image-2-pro-edit`

Reference a Step-1 illustration, then per slide:
```
Match this reference's palette, texture, and style exactly. Apply to the attached slide so the whole set is unmistakably one brand. Keep the on-image text unchanged.
```

---

## Bonus — let Qwen 3.7 art-direct itself

`qwen-3-7-plus` can see images, so it can review its own artwork. Paste any generated image in:

```
Here is an asset for my brand [ATTACH IMAGE]. Here is my brand bible [PASTE RELEVANT BITS].
Critique it like an art director:
1. Does it match our palette, style, and mood? Be specific about what's off.
2. Is any text misspelled or poorly placed?
3. Give me one concrete edit instruction I can paste into an image-edit model to fix the biggest issue.
```

Then run that instruction through `qwen-image-2-pro-edit` on the same image.

---

## Quick tips

- **Quote your text in image prompts** ("...") — that's what makes Qwen Image 2 Pro spell it correctly.
- **Reuse one style token** across every image, and **always edit from a reference** to stay consistent.
- Start with the **edit** step if you only try one thing — turning one good image into a matching set is the highest-leverage move.
- Everything runs privately on **[Venice](https://venice.ai)** — your brand ideas aren't used to train anyone's model.
