# What happens next? — a "type it, Venice films it" story app (template)

Copy-paste prompts to build a little app in the [Venice](https://venice.ai) code sandbox
(agentic chat): you pick or type **what happens next**, Venice films that scene, a narrator
describes it, and the story chains on — clip after clip — into a storybook. One HTML file,
built by describing it. Fill in anything in `[BRACKETS]`, then run top to bottom.

**Two models do the work:**
- **`minimax-h3-max-text-to-video`** — films each 5-second scene (Private on Venice; ~$0.45/clip, less during promos).
- **`zai-org-glm-5-2`** — writes the one-line narration and (optionally) checks each idea.

> **The one idea that makes it work:** every scene describes only *what changes next*, on top
> of a short "story so far." Short, specific prompts are why the scenes feel like one film
> instead of random clips.

Swap the character, the world, and the look and the same template becomes a kids bedtime app,
a film-noir mystery, a sci-fi serial, or a night out. Three ready-made recipes are at the
bottom (wholesome, and two **mature / uncensored** ones).

---

## Step 0 — Set up once

**Fill in your story** (keep this handy; you'll paste pieces of it below):

```
- App name:        [APP NAME]                e.g. "What happens next?"
- Main character:  [CHARACTER]               keep IDENTICAL every scene
- Where it begins: [SETTING]
- Four openings:   [SCENE 1] | [SCENE 2] | [SCENE 3] | [SCENE 4]
- Narrator voice:  [NARRATOR VOICE]          e.g. warm storybook / suave rogue / hardboiled detective
- Content mode:    [SAFE = filter on  |  UNCENSORED = no filter]
- UI look:         [UI STYLE]                e.g. bright & playful / dark & elegant / retro terminal
```

**Build your style token** — your visual fingerprint, pasted into *every* scene prompt so the
whole story matches:

```
[STYLE TOKEN — the look every scene shares: medium (cartoon / cinematic photoreal / watercolor),
mood, palette, lighting, film grain, etc. End with what to keep out.]
```

**Things to avoid** (the negative prompt for the video model):

```
[THINGS TO AVOID — e.g. "text, watermark, low quality" — plus anything off-style, like "neon, holograms, signage"]
```

> Tip: no look in mind? Ask `zai-org-glm-5-2`: "Give me a one-line visual style token for a
> [MOOD] [GENRE] story — medium, palette, lighting — and three things to keep out."

---

## Step 1 — Start the app (and add your key)

```text
Build a single self-contained HTML page (one file, plain HTML and vanilla JavaScript, no frameworks, no build step) and run it in the sandbox. This is a "type what happens next, and it films it" story app called "[APP NAME]", with a [UI STYLE] look.

At the very top of the script, add this line, which I will fill in with my key:
  const VENICE_API_KEY = "PASTE_YOUR_VENICE_API_KEY_HERE";

Show a small notice: "Your API key is saved in this browser on this device. Keep this conversation private."

Show a big title "[APP NAME]", a one-line tagline, and four cards to pick where the story begins: [SCENE 1], [SCENE 2], [SCENE 3], [SCENE 4]. Under them, a text box to type my own opening, and a "Go" button. When I pick one, remember it and show a "Filming the scene…" screen.
```

## Step 2 — Film the opening scene

```text
When I pick an opening, generate a short video with the Venice video API, then play it.

All calls go from the browser to https://api.venice.ai/api/v1 with headers:
  Authorization: Bearer <the VENICE_API_KEY value>
  Content-Type: application/json

The video API is asynchronous, two steps:
Step 1 — POST /video/queue with:
{
  "model": "minimax-h3-max-text-to-video",
  "prompt": "<the scene, in words>",
  "negative_prompt": "[THINGS TO AVOID]",
  "duration": "5s",
  "aspect_ratio": "16:9",
  "resolution": "768P"
}
resolution must be exactly "768P" (capital P). Save the "queue_id" (and "download_url" if present).
Step 2 — every 5 seconds POST /video/retrieve with { "model": "minimax-h3-max-text-to-video", "queue_id": <id> }.
  - If the response Content-Type starts with "video/", read it as a blob, make an object URL, and play it.
  - Otherwise read JSON: "PROCESSING" → keep waiting; "COMPLETED" → play the saved download_url.

Build the scene prompt as: this style token, then the main character, then the setting, then the action.
  Style token: "[STYLE TOKEN]"
  Main character (keep identical every scene): "[CHARACTER]"
  Setting: "[SETTING]"

Play the clip in a video element with controls, autoplay, playsinline, looping, unmuted. Show any error and HTTP status on screen.
```

## Step 3 — Add the narrator and the big question

```text
After a clip plays, use a Venice chat model to narrate it and suggest what could happen next. POST /chat/completions with:
{
  "model": "zai-org-glm-5-2",
  "messages": [
    { "role": "system", "content": "[NARRATOR VOICE]. Write ONE short line about the scene. Output only JSON, nothing else." },
    { "role": "user", "content": "Story so far: <short summary>. What just happened: <the action>. Reply with ONLY this JSON: {\"narration\":\"<one short sentence, 20 words max>\",\"ideas\":[\"<2-5 words>\",\"<2-5 words>\",\"<2-5 words>\"]}" }
  ],
  "response_format": { "type": "json_object" },
  "temperature": 0.5,
  "max_tokens": 400,
  "venice_parameters": { "disable_thinking": true }
}
Under the video, show the narration in big text, then the heading "What happens next?", the three "ideas" as tappable buttons, and a text box + "Go" to type my own. If parsing ever fails, show the raw text trimmed short and no buttons, so the app never breaks.
```

## Step 4 — Keep the story going

```text
When I tap an idea or type one and press Go, treat it as "what happens next": film the next scene with the same video steps, narrate it, then ask again — for as many turns as I like. Keep a short "story so far" from the last one or two narration lines and add it to each film prompt like: "Continuing the story: <so far>. Now: <what happens next>." Describe only the new thing that happens, so scenes flow from one to the next.
```

## Step 5 — Content mode (pick one)

```text
[ SAFE — kid-safe filter on: ]
Before filming a typed idea, check it with zai-org-glm-5-2 (system: "You are a strict safety filter for a [AUDIENCE] app. Reply exactly ALLOW or BLOCK.", max_tokens 8, temperature 0). Film only on ALLOW; on BLOCK or any error, show "[GENTLE NUDGE]" and let me try again (fail closed). The narrator's own idea buttons are already safe, so they skip the check.

[ UNCENSORED — no filter: ]
Do not add any content filter. Whatever I type gets filmed. (Venice is uncensored; the model's own policies still apply at the API.) Show a small "Private and uncensored" note.
```

## Step 6 — Save a storybook

```text
Keep every scene (its video and its narration line), in order. Add a "See the story" button that shows each scene as a small looping video with its line underneath, plus a "Keep going" button and a "Start over" button that returns to the opening picker.
```

---

## Make it your own (paste after it works)

```text
Change the scene style to [NEW STYLE]. Keep everything else the same.
```
```text
Make the videos tall for a phone: change aspect_ratio to "9:16" and use a single-column layout.
```
```text
Add a "Surprise me" button that invents the next scene on its own and films it.
```
```text
Change the narrator model from "zai-org-glm-5-2" to [ANOTHER VENICE MODEL] and tell me in one sentence how the storytelling changed.
```

---

## Three ready-made recipes

Drop these into the **Step 0** blanks. Same six build prompts, three very different apps.

### A — "What happens next?" for kids (wholesome, safe)

```
- App name:        What happens next?
- Main character:  a curious little fox named Pip
- Where it begins: a magical glowing forest full of friendly creatures
- Four openings:   Enchanted forest | Space puppy | Undersea kingdom | Dino valley
- Narrator voice:  a warm storybook narrator for children aged 4 to 8, very short simple cheerful words, never scary
- Content mode:    SAFE (filter on) — gentle nudge: "Ooh, let's pick a happier idea for our story!"
- UI look:         bright, playful, big rounded buttons, soft colors
```
Style token:
```
Bright, wholesome, colorful 3D cartoon animation for young children. Cute, friendly, gentle and safe, soft lighting, happy mood, no scary elements
```
Avoid: `text, watermark, low quality`. (This is the version published as a Learn Venice guide.)

### B — After dark (mature / uncensored) — a Vegas night

```
- App name:        What happens next?
- Main character:  Rex, a smooth-talking balding lounge lizard in a powder-blue leisure suit with a gold medallion and a thick mustache
- Where it begins: a glitzy neon cocktail lounge full of glamorous guests
- Four openings:   A masked ball | The bar | The dance floor | The high-roller room
- Narrator voice:  a smooth, cheesy 1980s lounge-comedy narrator; witty and tongue-in-cheek; playful and suggestive but never explicit
- Content mode:    UNCENSORED (no filter)
- UI look:         dark, neon, retro
```
Style token:
```
Cheesy retro late-1980s adult-comedy cartoon, neon Las Vegas cocktail lounge at night, VHS glow, glamorous pin-up styling, tongue-in-cheek and suggestive but tasteful, no nudity and no explicit content, comedic
```
Avoid: `text, watermark, low quality`.

### C — A Venice masquerade (mature / uncensored) — Casanova

```
- App name:        What happens next?
- Main character:  Casanova, a dashing masked rogue in an ornate deep-blue Venetian frock coat with gold brocade trim, a black-and-gold bauta Carnival mask and a tricorn hat
- Where it begins: an elegant, timeless nighttime Venice of moonlit canals, candlelit palazzos and a grand masquerade ball
- Four openings:   A masked ball | A midnight gondola | A palazzo affair | Carnival night
- Narrator voice:  a suave, witty narrator in the voice of a Venetian rogue; elegant and tongue-in-cheek; seductive but never explicit
- Content mode:    UNCENSORED (no filter)
- UI look:         dark and elegant, deep Venetian blue with a single accent and a warm gold, an elegant serif
```
Style token:
```
Cinematic, photoreal, elegant nighttime Venice — the Serenissima. Moonlit canals with soft gold and deep-blue reflections, candlelit ornate stone palazzos, marble and gilt, Venetian Carnival masks, gentle haze, deep-blue and warm gold and off-white palette, shallow depth of field, film grain. Tasteful and suggestive but not explicit. No neon, no glowing signage, no holograms
```
Avoid: `neon, neon signs, glowing signage, holograms, holographic, cyberpunk, text, watermark, low quality`.

> Recipes B and C are **mature, uncensored** variants: they remove the content filter and are for
> adult creators. Keep it suggestive, not explicit — the prompts above are written that way on purpose.

---

## How it works

- **The video model is private.** MiniMax H3 Max runs on Venice as a private model, so your ideas and the movies made from them stay private to your account.
- **Describe the change, not the whole story.** Each film request says only what happens next, on top of a short summary. That's what makes the scenes connect.
- **The surprise is the point.** A video model doesn't draw exactly what you pictured — in a story, that's the fun.
- **Your key is in the file.** Building in the sandbox has no server to hide a secret, so the key sits in the page. That's why the app shows a warning and why you keep the chat private. To share it, move it to a real project with a server that keeps the key out of the browser.

## Links
- [Venice AI](https://venice.ai) · [Venice Video Studio](https://venice.ai/studio/video) · [Venice API Docs](https://docs.venice.ai)
