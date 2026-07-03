# VIRTUAL INFLUENCER — WORLD BIBLE STARTER TEMPLATE v1.0
*A reusable prompt sequence for building a virtual influencer with a locked
world bible, generation-ready seeds, and a content pipeline. Fill every
[BRACKET], delete the guidance notes, and paste into your AI assistant.*

---

## HOW THIS WORKS

The process runs in four prompts:

1. **PROMPT 1 — The Founding Brief:** you define the character, world, ethos,
   and aesthetic. The AI drafts a full world bible and asks clarifying
   questions.
2. **PROMPT 2 — Lock Canon:** you answer the questions. The AI delivers the
   locked bible as a saveable markdown artifact.
3. **PROMPT 3 — Reference Prompt Pack:** the AI converts the bible into a
   complete set of image-generation prompts for identity and world reference
   images.
4. **PROMPT 4 — Video Prompts:** the AI writes reference-to-video prompts for
   your first pieces of content.

**The golden rule:** be opinionated in Prompt 1. The more concrete your
constraints (especially the *prohibitions* — things that must NEVER appear),
the more coherent everything downstream becomes. A world is defined as much
by what it excludes as what it contains.

---

## PROMPT 1 — THE FOUNDING BRIEF

> Help me create a virtual influencer. I want it to be a [GENDER/PRESENTATION]
> that [CORE CONTENT MISSION — what they share and why it matters, in one or
> two sentences. Be specific: not "talks about fitness" but "shares insights
> into X and why Y matters in our relationship with Z"].
>
> [THEIR NAME OR "her"/"his"/"their"] "world" should be [SETTING CONCEPT — a
> place + a twist, e.g., "a serene cyberpunk version of Venice," "a solarpunk
> Appalachian rail town," "an art-deco lunar resort"]. The style is [AESTHETIC
> MOVEMENT MASH-UP — two or three reference styles that collide, e.g., "sci-fi
> Renaissance," "Bauhaus-meets-biotech"]. [ONE OR TWO SIGNATURE VISUAL MOTIFS —
> the details that make it yours, e.g., "baroque facades laced with soft
> holographic filigree," "marble statues infused with technology"].
>
> Technology in this world is "[TECH DESIGN LANGUAGE — name it in a compound
> word, e.g., "analog-cyber," "botanical-industrial"]" — [MATERIALS AND
> TEXTURES that express it, e.g., "brass, glass, and hand-worked detail over
> sleek screens"].
>
> Ethos: [2–4 SHORT VALUE PHRASES — the moral spine of the brand, e.g.,
> "dignity, not paranoia. Self-sovereignty." These will become the character's
> beliefs and the captions' backbone].
>
> Color palette: [3–5 COLORS in plain words, e.g., "deep blue, off-white, warm
> stucco"]. Lighting: [ONE PERPETUAL LIGHTING CONDITION, e.g., "perpetual
> golden hour," "eternal overcast dawn"]. [AT LEAST ONE ABSOLUTE PROHIBITION —
> this is the most important line in the brief, e.g., "no red at all," "no
> straight lines," "never nighttime"].
>
> Render style: [REALISM LEVEL, e.g., "photorealistic"], [LENS/DEPTH
> CHARACTER, e.g., "shallow depth of field"], [TEXTURE DOCTRINE, e.g.,
> "natural skin and material texture"].
>
> Now, help me create an entire world bible that includes settings and lore,
> visual canon, wardrobe, color palette, camera and render style, etc. We need
> an official world seed for media generations and a system prompt template.
>
> Ask me if you have any questions. Let's begin.

### Guidance for filling Prompt 1
- **Mission:** pair a topic with a stance. Topic alone makes a content
  channel; topic + worldview makes a character.
- **Setting:** real place + speculative twist beats pure invention — the AI
  (and image models) have deep priors on real places, so you get richness
  for free while the twist keeps it ownable.
- **Prohibitions:** every strong brand has a "never." A banned color, angle,
  or object gives your visuals instant recognizability and gives generators
  a hard rule to obey.
- **Ethos:** phrase values as tensions resolved ("dignity, not paranoia"),
  not single words ("privacy"). Tension is memorable and writable.

---

## PROMPT 2 — LOCK CANON

*The AI will come back with a draft bible and clarifying questions — usually
about name, human-vs-AI in fiction, platforms, sensuality level, real-world
engagement, and your generation tools. Answer decisively:*

> 1. [CHOSEN NAME]
> 2. [IS THE CHARACTER IN-FICTION A HUMAN, AN AI, OR OTHER? — if your theme
>    touches AI at all, "a self-sovereign AI" is thematically powerful, but a
>    human artisan is simpler to write. Pick one and commit.]
> 3. [PRIMARY FORMAT: vertical video / stills / long-form — this drives the
>    camera canon]
> 4. [SENSUALITY DIAL: elegant-only / tasteful allure / both — and rough
>    content ratio if both]
> 5. [REAL-WORLD ENGAGEMENT: fully fictional / comments on real news through
>    the world's lens / both]
> 6. [YOUR GENERATION STACK: list image and video tools/models so prompts can
>    be adapted to their quirks, e.g., negative-prompt support, reference-image
>    workflows]
>
> Provide me the full bible (and any other artifacts) in markdown format so I
> can save it.

### What the locked bible must contain (checklist — ask for anything missing)
- [ ] One-paragraph pitch
- [ ] World premise, core metaphor, and canonical ethos phrasing
- [ ] Lore: 5–8 named institutions/locations/traditions
- [ ] Character sheet: identity, origin story, locked physical canon with an
      "identity fingerprint" (3–5 never-drift features: a jewelry item, mark,
      hairstyle, prop)
- [ ] Personality, voice, metaphor vocabulary, signature sign-off
- [ ] Visual canon + HARD NEGATIVES list (things that never appear)
- [ ] Color palette with hex codes and the absolute prohibition restated
- [ ] Wardrobe: 4–6 named outfits as reusable modules
- [ ] Camera/light/render canon tuned to your primary format
- [ ] OFFICIAL WORLD SEED: a paste-ready block for every generation, plus a
      character seed block and a negative block
- [ ] System prompt for the character's LLM voice
- [ ] Content pillars and first 5 post concepts
- [ ] Canon governance: versioning rules + a seed/reference log table

---

## PROMPT 3 — REFERENCE PROMPT PACK

> In another markdown file, give me all the image generation prompts for
> creating our reference images for the world, including characters.

### What to expect / demand
- **Reusable blocks first** (world seed, character seed, wardrobe modules,
  negatives) with tokens, so prompts assemble by find-and-replace.
- **An identity board section (~12 shots) BEFORE anything else:** frontal,
  three-quarters both sides, profile, full body, and macro details of the
  identity-fingerprint features. You generate these across all candidate
  tools, pick ONE winning face, then anchor every later generation to it via
  image reference. Never generate world beauty-shots first — you'll be
  tempted to keep off-canon faces standing in pretty places.
- Sections for: wardrobe references, environments, institutions/locations,
  technology/props, secondary background characters, and **video anchor
  stills** (composed as stable first frames for image-to-video).
- An **acceptance checklist** to apply to every keeper (prohibitions honored,
  fingerprint features present, texture doctrine met, format crops safely).

---

## PROMPT 4 — VIDEO PROMPTS

> Now make the [VIDEO TOOL NAME] prompts for the first [N] pieces of content.
> Reference to video.

### What to expect / demand
- **Reference-to-video only** for shots containing the character —
  text-to-video identity drift is too high. Each shot names which reference
  still it anchors to.
- Per post: a timed voiceover script + 3–5 shots of 5–10 seconds, **one
  motion idea per shot**. The character moves slowly or not at all; the
  environment carries the life (dust, steam, water, fabric, light).
- A shared negative/avoid block covering your prohibitions plus video
  failure modes (face morphing, hand warping, fast camera moves).
- Edit notes syncing key visual beats to specific VO lines, and a
  production checklist per clip.
- **Record/generate the VO first, then trim shots to the read** — never the
  reverse.

---

## OPTIONAL PROMPT 5+ — CONTINUING THE PIPELINE

- "Write the full scripts and captions for the five launch posts."
- "Draft a 4-week content calendar across my pillars."
- "Write the character's replies to these 10 likely audience comments."
- "Amend the bible to v1.1: [change]. Provide a changelog entry."

---

## PRINCIPLES THAT MAKE THIS WORK (keep in mind throughout)

1. **Canon is law.** Once the bible is locked, every artifact must conform.
   Changes go through version bumps, not vibes.
2. **Exclusions define the brand.** Your "never" list (colors, objects,
   angles) does more for visual consistency than any positive description.
3. **Face first, world second.** Lock the identity anchor before generating
   anything else featuring the character.
4. **One motion idea per video shot.** Stillness reads as premium;
   generators reward restraint.
5. **The character needs a thesis, not just a look.** The ethos should be
   arguable in one sentence — that sentence is what turns pretty images
   into a following.
6. **Log everything.** Tool, version, seed, reference ID, prompt — the log
   is canon too.