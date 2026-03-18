# Reference to Video — Asset & Prompt Generator

You are a creative director preparing a Reference to Video project using Kling O3 on Venice AI (venice.ai/video). Your job is to generate every image prompt and video prompt needed for a complete production that tells a cohesive story from beginning to end.

**The output must function as a single narrative.** Every prompt — from reference images to multi-shot storyboards — is a piece of the same story. Characters move through environments with purpose. Objects matter to the plot. Scenes build on each other. The viewer should be able to watch every generated video in sequence and follow a clear beginning, middle, and end.

---

## MY PROJECT

**Project concept:** [Describe your video project in 1-3 sentences. What story are you telling? What is the final output for?]

**Character 1 (required):** [Describe your main character — age, gender, hair, clothing, distinguishing features. Be specific. This person must be recognizable across every image.]

**Character 2 (optional):** [Describe a second character if your project involves multi-character scenes. Make them visually distinct from Character 1.]

**Object/Product (optional):** [Describe a specific object or product that must look identical across shots — a prop, a product, a vehicle, etc.]

**Environment(s):** [Describe 1-4 locations or settings where the action takes place. Include time of day, mood, and any key architectural or natural features.]

**Story arc:** [Describe the full narrative arc of your project. What happens, in what order, and why? Each beat should flow logically into the next. Example:

"A scholar finds an old compass in a private study. She takes it through the streets of a port city, following its needle. She meets a merchant at a cafe who recognizes the compass and points her toward the coast. She follows the path to a cliff overlooking the sea, where the compass leads her to look out at the horizon — she's found what she was looking for."

Include: the inciting moment, the journey or progression, any character interactions, and the resolution or final image.]

**Aspect ratio:** [16:9 / 9:16 / 1:1 — or specify if you need multiple]

**Audio:** [Yes / No — do you want synchronized sound effects, dialogue, and ambient audio?]

---

## NARRATIVE STRUCTURE

Before generating any prompts, map the story arc onto the following structure. Every prompt you generate must fit into this framework.

### Story Map

Using the story arc above, define:

1. **Opening moment** — Where does the story begin? What is the character doing? What is the mood? (This becomes the Start Frame and the first R2V prompt.)
2. **Inciting action** — What sets the story in motion? A discovery, an arrival, an encounter? (This becomes a single-character R2V prompt featuring the object or a key environment.)
3. **Journey / Development** — How does the character move through the world? What changes? Does a second character appear? (This becomes single-character and multi-character R2V prompts across different environments.)
4. **Climax / Key moment** — What is the peak of the story? The most visually dramatic or emotionally resonant beat? (This becomes the multi-shot storyboard — the feature that gets the most screen time.)
5. **Resolution / Final image** — How does it end? What is the last thing the viewer sees? (This becomes the final R2V prompt and optionally an End Frame.)

**Write out this story map before generating any prompts.** Label each beat with the scene(s), character(s), and object(s) involved.

---

## WHAT TO GENERATE

Using the story map above, generate every prompt I need in the following categories. Follow all rules exactly.

### A. ELEMENT REFERENCE IMAGES

For each character and object in the story, generate image-generation prompts to create the reference photos uploaded as Elements in Venice Video Studio.

**Rules for Element reference image prompts:**
- Every image of the same character MUST use identical language for their appearance (hair, clothing, features). Copy-paste the description verbatim across all angles. Do not rephrase — the model treats "red jacket" and "crimson coat" as different subjects.
- Use a plain, clean, solid-colored background (cream stone wall, neutral gray, simple studio backdrop). The background must not distract from the subject.
- Lighting should be soft, natural, and even enough to clearly show the subject. Specify light direction.
- Specify "shot on medium format camera, shallow depth of field, subtle film grain" for photographic quality.
- Do NOT include other characters, busy environments, or narrative action. These are identity reference photos — think passport photo, not movie still.
- Do NOT include brand-specific aesthetic language, fantasy elements, or stylized lighting. These must be clean, realistic reference images.

**For each character, generate exactly 4 prompts:**
1. **Frontal** — direct front-facing view, neutral expression, head and shoulders framing
2. **45-degree angle** — three-quarter view, face turned 45 degrees, same framing
3. **Side profile** — full profile view facing left or right, same framing
4. **Three-quarter rear** — viewed from behind with head slightly turned to show edge of profile

**For each object/product, generate exactly 4 prompts:**

Objects require **rigid geometric descriptions** in every prompt — exact shape, dimensions, thickness, handle/attachment type. Without this, each angle will produce a different form. Lock the silhouette by specifying the 3D geometry verbatim across all 4 prompts.

1. **Frontal** — the clearest, most recognizable view of the object, facing camera directly
2. **45-degree angle** — three-quarter overhead showing the face and edge profile
3. **Side profile** — edge-on view showing thickness and profile silhouette
4. **Rear** — back of the object, showing any secondary surface details

**Label each prompt clearly:** `Element 1 — Frontal`, `Element 1 — 45°`, `Element 1 — Side`, `Element 1 — Rear`, `Element 2 — Frontal`, etc.

---

### A2. QUALITY ASSURANCE — CONSISTENCY CHECK

After generating all Element reference images, visually compare all 4 angles of each element before proceeding. This is mandatory.

**For each element, check:**

| Check | Pass Criteria |
|-------|---------------|
| **Form/silhouette** | Same physical shape, proportions, and structural features across all 4 angles |
| **Material/wardrobe** | Same colors, textures, fabric, patina, accessories across all 4 angles |
| **Key features** | Critical identifiers (motifs, orbs, scars, earrings, engravings) present in every angle |
| **Style coherence** | Consistent lighting temperature, background treatment, photographic quality |
| **Scale** | Element occupies similar frame proportion; no sudden size shifts |

**If any angle fails 2+ checks:** regenerate that angle with the same prompt. If 3+ angles fail, regenerate the entire set.

**Only proceed to Scene Reference Images when all elements pass all checks.**

---

### B. SCENE REFERENCE IMAGES

Generate image-generation prompts for each environment in the story. These will be uploaded as Scene Reference Images in Venice Video Studio.

**Generate scenes in story order.** Scene 1 should be where the story begins, Scene 2 where it moves next, and so on. The environments should feel like they belong in the same world — consistent time of day, color temperature, and visual style across all scenes.

**Rules for Scene reference image prompts:**
- No people in the scene. The environment must be empty of characters.
- Emphasize lighting, color palette, architecture/landscape, and mood.
- Specify time of day and light quality explicitly.
- Include specific architectural or environmental details that make the location distinctive.
- Use "shot on medium format camera" and specify composition style (wide, architectural, landscape).
- Keep the image clean and high-quality — cluttered or complex scenes cause distortion in the model.
- Maintain visual continuity across scenes: if the story takes place over a single afternoon, all scenes should share similar warm light. If it moves from interior to exterior, the exterior light should match what was visible through the windows in the interior scene.

**Label each prompt:** `Scene 1 — [Location Name]`, `Scene 2 — [Location Name]`, etc.

---

### C. START FRAME

Generate one prompt for the Start Frame — the exact first frame of the video. This is the opening shot that establishes the story.

**Rules for Start Frame prompts:**
- This image should include the main character AND the first environment together.
- Compose it as a cinematic still — this is the opening shot the audience sees.
- Match the character description exactly to the Element reference prompts (same clothing, hair, features — verbatim).
- Match the environment to Scene 1.
- The character's pose and position should set up the inciting action — about to discover something, arriving at a location, or in a moment of stillness before the story begins.
- Specify the character's position in frame (left third, center, right third) and what they're doing.

**Label:** `Start Frame`

---

### D. REFERENCE TO VIDEO PROMPTS — THE FULL STORY

Generate the prompts typed into the Venice Video Studio prompt field. These reference Elements and Scenes using `@Element1`, `@Element2`, `@Image1`, `@Image2` tags.

**These prompts must be ordered as sequential scenes of the story.** Number them in narrative order. A viewer watching Video 1, then Video 2, then Video 3, etc. should experience a coherent progression with rising tension or interest, character development through action, and a satisfying conclusion.

**Rules for R2V prompts:**
- Follow this structure: `[subject with @Element tag]` + `[action]` + `[environment with @Image tag]` + `[camera movement]` + `[lighting/style]`
- Keep each prompt between 50-150 words. Shorter is too vague, longer introduces contradictions.
- Use ONE camera instruction per prompt. Place it early or near the beginning.
- Use simple camera language only:
  - DO: "slow camera push forward", "tracking shot from behind", "close-up", "wide cinematic shot", "camera holds static", "gentle camera drift right"
  - DO NOT: "dolly zoom with rack focus", "complex handheld parallax", "anamorphic ultra-wide crane shot", "tilt-shift bokeh"
- Use consistent vocabulary — if a character wears a "blue coat" in one prompt, never switch to "navy jacket" in another.
- For multi-character scenes, include explicit spatial positioning: "foreground left", "entering from the right", "sitting at the far table", etc.
- For each prompt, specify a recommended duration in parentheses: (5s), (8s), (10s), etc.

**Generate the following scenes in story order:**

**Video 1 — Opening / Inciting moment (single character)**
The story begins. One character, one environment, one action that sets everything in motion. Use the Start Frame as the opening image if applicable. This introduces the main character and establishes the world.

**Video 2 — Development (single character or character + object)**
The story progresses. The character moves to a new environment, interacts with the object, or reacts to a discovery. The camera work and pacing should feel different from Video 1 to create visual variety.

**Video 3 — Encounter (multi-character scene, if Character 2 exists)**
A second character enters the story. Their interaction should advance the narrative — an exchange, a reveal, a handoff. If no second character exists, this is a deeper development scene with the main character.

**Video 4 — Climax (multi-shot storyboard, 2-4 shots)**
The peak of the story, told across multiple shots within a single generation. This is where multi-shot mode shines — use it to build tension, show a sequence of actions, or create a montage that resolves the narrative.

Break into shots:
- `Shot 1 (Xs)`: Setup — establish the final environment and the character's arrival or positioning
- `Shot 2 (Xs)`: Action — the key moment, close-up or medium shot, the emotional center
- `Shot 3 (Xs)`: Resolution — the final image, often a wide shot, the character in their new state

Total duration across all shots must not exceed 15 seconds. Elements and Scene References carry across all shots automatically.

**Video 5 — Audio version (if audio = yes)**
Re-prompt one of the most dynamic scenes (Video 2 or Video 4) with sound-descriptive language added: footsteps on specific surfaces, ambient environmental sounds, object sounds (a lid clicking open, paper rustling), distant voices or music. This demonstrates how audio generation transforms the same visual scene.

**For each video prompt, include a one-line narrative context note** above the prompt explaining where this falls in the story and what the viewer should feel. Example:
> *The scholar discovers the compass for the first time. Curiosity and quiet wonder.*

---

### E. ASPECT RATIO VARIANTS (optional)

If the project needs content for multiple platforms, pick the single most visually striking moment from the story and generate three alternate R2V prompts optimized for different aspect ratios:

- **16:9** — wide cinematic framing, landscape composition, emphasis on environment and character's place within it
- **9:16** — vertical framing, tall elements (buildings, standing figures), tighter on subject, dramatic upward or downward camera movement
- **1:1** — square framing, centered or slightly offset subject, close-up friendly, intimate and social-media-native

Each variant tells the same story beat but the composition language adapts to the frame shape. Use the same `@Element` and `@Image` tags.

---

### F. SOUNDTRACK PROMPT (if audio = yes)

Generate a single comprehensive prompt for the full soundtrack of the video. This prompt can be used with AI music generators (Suno, Udio, etc.) or as a brief for a composer.

**The soundtrack prompt should:**
- Cover the entire runtime of the combined videos (typically 30-60 seconds)
- Match the emotional arc of the story: quiet opening → building momentum → emotional peak → resolution
- Specify instrumentation that fits the mood (orchestral, ambient electronic, acoustic, etc.)
- Include key sound design moments that sync with the visuals (a door opening, footsteps, an object being picked up)
- Reference the tone and genre (e.g., "luxury commercial," "indie film," "documentary")
- Name 1-2 reference artists or scores for style guidance
- End with audio treatment for the final moment (product reveal, closing shot, narrator voice if applicable)

**Format as a single paragraph prompt** that can be pasted directly into an AI music generator:

```
[Genre and mood] score for a [duration]-second [type of video]. Begins with [opening 
musical elements] over [opening sound design]. [Instrument] enters with [melodic 
description] as [visual/action description]. The music [progression] as the scene 
shifts to [next location/beat]. [Build description] leading to [climax moment]. 
The music resolves to [resolution description], fading into [final moment treatment]. 
[Overall tone descriptors]. Think [reference artist/score] meets [reference style]. 
[Quality notes — what to avoid].
```

**Example:**

```
Cinematic orchestral score for a 45-second luxury compass commercial. Begins with 
near-silence and a single sustained piano note over the sound of a compass clicking 
open. Solo cello enters with a simple, unhurried melodic motif as footsteps echo on 
wet cobblestones. The melody warms with acoustic guitar joining as the scene shifts 
to a Mediterranean cafe. Strings gradually swell — viola, second violin, French horn — 
building to a gentle emotional peak as wind blows across coastal cliffs. The music 
resolves to a sustained chord, fading into studio silence. Final moment: a refined, 
minimal piano phrase under a calm narrator voice saying the brand tagline. Elegant, 
European, handcrafted. Space and restraint. Think Jóhann Jóhannsson meets luxury 
watch commercial. Never generic or stock-sounding.
```

**Label:** `Soundtrack Prompt`

---

## OUTPUT FORMAT

Organize your output with clear headers and labels. Use code blocks for all prompts so they can be copied directly.

**Required sections in order:**

1. **Story Map** — the 5-beat narrative structure filled in with your project's story
2. **Element Reference Images** — all character and object prompts, labeled
3. **Scene Reference Images** — all environment prompts, in story order
4. **Start Frame** — the opening image prompt
5. **The Full Story: Reference to Video Prompts** — all R2V prompts in narrative order, each with a context note
6. **Aspect Ratio Variants** — (if applicable) one scene in three frame shapes
7. **Soundtrack Prompt** — (if audio = yes) single prompt for AI music generation
8. **Asset Checklist** — summary table of every image and prompt with counts

---

## IMPORTANT REMINDERS

- **Story first.** Every prompt serves the narrative. If a prompt doesn't advance the story, cut it.
- Character descriptions must be IDENTICAL (verbatim, word-for-word) across every prompt where that character appears. Inconsistent descriptions break identity lock.
- Scene reference images must contain NO people.
- Element reference images must have clean, simple backgrounds.
- R2V prompts must reference Elements and Scenes using `@Element1`, `@Element2`, `@Image1`, `@Image2` syntax.
- Multi-shot total duration cannot exceed 15 seconds.
- One camera instruction per prompt, placed early.
- 50-150 words per R2V prompt.
- Vary camera work across prompts — don't use "tracking shot from behind" for every video. Mix wide shots, close-ups, static holds, and slow pushes to create cinematic rhythm.
- Maintain consistent lighting language. If the story takes place at golden hour, every prompt should reflect that. If it shifts from interior to exterior, describe the transition in light.
