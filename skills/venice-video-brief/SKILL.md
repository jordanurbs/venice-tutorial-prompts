---
name: venice-video-brief
description: Generate video production briefs for AI video commercials using Venice AI's Reference to Video (R2V) feature. Creates story arcs, reference image prompts, R2V video prompts, multi-shot storyboards, and soundtrack prompts. Use when the user wants to plan a video commercial, create a multi-scene narrative, build a video production brief, or mentions "R2V," "reference to video," "video brief," "video commercial," or "multi-shot storyboard."
---

# Venice Video Production Brief Generator

Complete workflow for creating AI video commercials using Venice AI's Reference to Video feature. Produces all assets needed for a multi-scene narrative where characters, objects, and environments stay visually consistent across every shot.

**Mega-prompt template:** [reference-to-video-prompt-generator.md](../../reference-to-video-prompt-generator.md) — paste into any frontier model with your project details to get all prompts back.

## Inputs Required

Before starting, collect from the user:

| Input | Required | Description |
|-------|----------|-------------|
| Story idea | Yes | Core concept / narrative premise |
| Characters | Yes | Name, appearance, wardrobe for each |
| Product/Object | If commercial | The hero product or key prop |
| Environments | Yes | 1-3 distinct locations |
| Audio needed | No | Whether to generate soundtrack prompt |
| Demo deck | No | Whether to build an HTML presentation |

## Workflow

### Step 1 — Story Arc (5 Beats)

Define a narrative arc with these beats:

1. **Opening / Inciting moment** — Establish world, introduce protagonist
2. **Development / Journey** — Character moves through environment
3. **Encounter** (if multi-character) — Characters meet, interact
4. **Climax** (multi-shot storyboard) — 2-4 shots within one generation, ≤15s total
5. **Resolution / Reveal** — Product hero shot or emotional payoff

Write a 2-3 sentence description for each beat before moving to image generation.

### Step 2 — Generate Reference Images

For each element, generate images via Venice image API using identical descriptions across all angles. Both characters and objects need 4 reference angles for reliable identity lock:

| Element | Images | Angles |
|---------|--------|--------|
| Character | 4 per character | Frontal, 45°, side profile, rear |
| Object/Product | 4 per object | Frontal, 45°, side profile, rear/underside |
| Environment | 1 per location | Clean scene, no people |
| Start frame | 1 (optional) | Character + environment composed together |

**Identity lock rule:** Use the *exact same description verbatim* for all 4 angles of each element. Only change the angle instruction. This applies to both characters AND objects.

**Character prompt template:**

```
[Character description with wardrobe, hair, build, age range], [angle: frontal view / 45-degree angle / side profile / rear view], [lighting style], [background], photorealistic, editorial photograph quality
```

**Object prompt template:**

Objects require **rigid geometric descriptions** — shape, dimensions, structural features. Without this, each angle will produce a different form (e.g., a key in one, a stamp in another, a plaque in a third). Lock the silhouette:

```
[Exact 3D form: shape, dimensions, thickness, handle/attachment type], [relief/surface details: motifs, engravings, insets], [materials with aging/condition], [angle: frontal view / 45-degree angle / side profile / rear view], [surface/setting], [lighting style], photorealistic, editorial product photography quality
```

**Example (locked geometry):**
```
A round brass disc medallion, approximately 8cm in diameter and 1cm thick, with a raised beveled rim and a small ring loop handle at the bottom. The face features a relief-carved winged lion holding an open book. A 1cm inset cabochon orb of translucent blue glass is positioned at the center of the lion's chest...
```

### Step 2b — Quality Assurance: Consistency Check

After generating all reference images, **visually analyze every set** before proceeding. This is mandatory — inconsistent references break identity lock in video generation.

**For each element (characters and objects), check all 4 angles against these criteria:**

| Check | What to Look For | Action if Failed |
|-------|-----------------|------------------|
| **Face/form consistency** | Same facial structure, nose shape, jawline, eye spacing (characters); same silhouette, proportions, distinguishing marks (objects) | Regenerate the outlier angle |
| **Wardrobe/material match** | Same clothing, fabric colors, embroidery details, accessories (characters); same surface material, patina level, color (objects) | Regenerate the outlier angle |
| **Key features present** | Critical identifiers appear in every angle — earrings, circuit traces, scars (characters); motifs, orbs, engravings (objects) | Regenerate any angle missing features |
| **Style coherence** | Consistent lighting temperature, background treatment, photographic quality across all 4 | Regenerate outliers that break the set |
| **Scale/proportion** | Element occupies similar frame proportion across angles; no sudden size shifts | Regenerate the off-scale angle |

**Process:**
1. Open all 4 angles for each element side by side
2. Score each check as PASS or FAIL
3. If any angle fails 2+ checks, regenerate it with the same prompt + model
4. After regeneration, re-run the consistency check on the new image
5. Only proceed to R2V prompts when all elements pass all checks

**Tip:** When regenerating a single outlier, keep the passing images and only replace the failing one. If 3+ angles fail, regenerate the entire set — the first image likely set a direction the others couldn't match.

### Step 3 — Write R2V Video Prompts

Each prompt follows this structure:

```
[subject @Element] + [action] + [environment @Image] + [camera] + [lighting]
```

**Rules:**
- 50-150 words per prompt
- One camera instruction, placed early in the prompt
- Simple camera language only (dolly, pan, tracking shot, static wide)
- Explicit spatial positioning for multi-character scenes ("on the left," "across the table")
- Duration in parentheses at the end: `(5s)`, `(8s)`, `(10s)`
- Reference elements with `@Element` syntax matching Venice Video Studio uploads

**Example:**

```
Medium tracking shot follows @Scholar as she walks through a narrow cobblestone alley @Mediterranean_Street, trailing her fingers along a sun-warmed stone wall. She holds @Compass in her right hand, glancing down at it intermittently. Afternoon light filters between terracotta buildings overhead, casting long diagonal shadows. Her linen dress catches a gentle breeze. Unhurried, contemplative pace. Warm natural lighting with golden hour tones. (8s)
```

### Step 4 — Multi-Shot Storyboard (Climax)

Break the climax beat into 2-4 shots within a single generation:

- Total duration ≤15 seconds
- All `@Element` and `@Image` references persist across shots
- Each shot gets its own camera + action description
- Separate shots with `CUT TO:` or `THEN:`

**Example:**

```
Shot 1: Close-up on @Merchant's hand pointing toward the coast, @Compass visible on the cafe table between them. Static camera. Warm interior light. (4s) CUT TO: Shot 2: Wide shot from behind @Scholar as she stands at @Cliff_Edge, Mediterranean sea stretching to the horizon. Wind in her hair. Slow push-in. Golden hour. (6s) CUT TO: Shot 3: Over-the-shoulder, @Scholar raises @Compass to eye level, the needle settling. Rack focus from her profile to the compass face. (5s)
```

### Step 5 — Product Reveal (Commercials)

Final shot features the object/product in isolation:

- Same `@Element` used throughout the story
- Studio or environmental hero shot
- Camera: slow rotation, push-in, or static glamour
- Include brand tagline as text overlay instruction if needed

**Example:**

```
@Compass rotates slowly on a dark marble surface under controlled studio lighting. Single warm spotlight from above left creates dramatic shadows. Brass details catch the light. Shallow depth of field. Ultra-slow clockwise rotation. Black background. (5s)
```

### Step 6 — Soundtrack Prompt

Single prompt covering full runtime:

```
[Genre/mood] track, [BPM range], [duration]. 
Opening: [instrumentation + feel]. 
Mid-section: [build/shift]. 
Climax: [peak instrumentation]. 
Resolution: [wind-down]. 
Sound design: [specific moments]. 
Reference artists: [2-3 names for style, not imitation].
```

## Assets Checklist

After completing the workflow, verify all assets:

| Asset | Count | Purpose |
|-------|-------|---------|
| Character reference images | 4 per character | Identity lock |
| Object reference images | 4 per object | Identity lock |
| Scene reference images | 1 per environment | World building |
| Start frame | 1 | Opening shot composition |
| R2V video prompts | 4-6 | The story |
| Soundtrack prompt | 1 | Music/sound design |

## Optional: Demo Presentation Deck

Build an HTML slide deck mapping inputs → prompts → outputs for screenshare/demo. Structure:

1. Title slide (concept + tagline)
2. Story arc overview (5 beats)
3. Character reference grid (4 angles)
4. Object reference grid (4 angles)
5. Environment reference
6. Video prompts with shot breakdowns
7. Soundtrack brief
8. Final product hero shot

## Image Compression

Before uploading reference images to Venice Video Studio, compress them:

```bash
for f in reference-images/*.png; do
  magick "$f" -resize '2048x2048>' -quality 85 "compressed/$(basename "$f" .png).jpg"
done
```

## Quick Start

1. Collect: story idea, characters, product (if commercial), environments, audio needs
2. Fill in the [mega-prompt template](../../reference-to-video-prompt-generator.md)
3. Generate reference images via Venice image API
4. Run QA consistency check on all reference sets
5. Compress images for Venice Video Studio upload
6. Write R2V prompts following the 5-beat story arc
7. Generate soundtrack prompt (if audio needed)
8. Optionally build presentation deck for walkthrough
