# Iconic Film Homages — a Venice Studio feature tour

Four ready-to-shoot shots that nod to famous films, built to **show off a different Venice Studio feature in each one**. Every shot uses a different cartoon character and a distinctly different visual style, so a viewer watching the set sees the full range of what Studio can do.

Paste the prompts straight into [Venice Video Studio](https://venice.ai/video) and the image/audio tools. Model IDs below reflect what's current at time of writing — confirm live with `GET /models?type=image|video|tts|music` before a shoot, since availability shifts.

## The four shots

| # | Film nod | Feature demoed | Character | Style |
|---|----------|----------------|-----------|-------|
| 1 | *The Good, the Bad and the Ugly* | **Agentic chat** writes the text-to-video prompt | Anthropomorphic desert critters | Cel-shaded graphic novel |
| 2 | *2001: A Space Odyssey* | **Generated image → start frame** (image-to-video) | Chibi astronaut mouse | Mid-century Saul Bass |
| 3 | *Jaws* | **Generated image → reference image** (character lock) | Pelican beach lifeguard | Watercolor storybook |
| 4 | *Singin' in the Rain* | **Generated audio → audio reference / bed** | Rubber-hose cat | 1930s black-and-white cartoon |

---

## Shot 1 — *The Good, the Bad and the Ugly* (spaghetti-western standoff)

**Feature:** Agentic chat writes the shot. Hand it a logline and let the model return a shot-ready text-to-video prompt — pure text-to-video, no starting frame, so it showcases raw generation.

**Step A — paste into agentic chat:**

```
You are a cinematographer writing ONE text-to-video prompt (max 120 words)
for Venice video. Shot: a Mexican-standoff homage to The Good, the Bad and
the Ugly, but with cartoon desert animals. Cover the three characters, the
widescreen framing, rapid whip-pans between extreme eye close-ups, high-noon
light and dust, and a cel-shaded graphic-novel style. End with camera/lens
notes. Output only the prompt.
```

**Step B — the video prompt** (`wan-2-7-text-to-video` · `5s` · `21:9` · `720p` · `audio: true`):

```
Cel-shaded spaghetti-western standoff at high noon: thick ink outlines,
sun-bleached ochre palette, heat haze and drifting dust in a dead ghost town.
Three cartoon desert animals face off — a lean coyote gunslinger in a poncho
(calm, steady eyes), a hulking scarred warthog with a cigar (cruel grin), and
a twitchy jackrabbit clutching his hat. Extreme macro close-ups on darting
eyes and paws hovering over holsters; whip-pans cut faster and faster between
the three; low telephoto angle compresses the empty street; a lone church
bell tolls. Camera snaps wide-to-macro on a trigger finger. 21:9 anamorphic,
35mm grain.
```

Negative prompt: `photorealistic, human faces, blood, gore, modern objects, text, watermark`

---

## Shot 2 — *2001: A Space Odyssey* (the monolith)

**Feature:** Generate a still first, then use it as the **start frame** for image-to-video. Best for shots where the composition has to be exact — you lock the frame, then animate camera and light off it.

**Step A — start frame** (`z-image-turbo`, or `nano-banana-pro` for tight composition · `16:9`):

```
Mid-century modernist sci-fi poster, flat geometric color fields, Saul Bass
style, subtle film grain. Perfectly symmetrical wide composition: a tiny
kawaii chibi astronaut mouse in a round white suit stands dead-center on a
smooth grey lunar plain, facing a towering pitch-black monolith. A thin,
brilliant sunrise line crests behind the monolith; long shadows; star-dusted
black sky. Palette limited to bone-white, slate grey, and burnt orange.
```

**Step B — image-to-video** (an image-to-video model — check `GET /models?type=video` for a current Wan/Kling i2v variant · `image_url` = the frame above · `6s` · `16:9` · `audio: true`):

```
Hold the symmetrical framing, then a slow, reverent dolly push toward the
monolith. The sunrise line flares and climbs; light rakes across the lunar
dust; the astronaut mouse tilts its head up in awe. Almost no other motion —
glacial, ominous — a low resonant hum swelling. Preserve the flat mid-century
color and faint grain.
```

---

## Shot 3 — *Jaws* (the dolly zoom)

**Feature:** Generate a clean character design once and feed it as a **reference image** so the character stays consistent while the camera does the famous Spielberg contra-zoom.

**Step A — reference sheet** (`z-image-turbo` · plain background):

```
Character reference sheet, warm watercolor storybook style, soft painterly
edges, gouache texture. A friendly cartoon pelican beach lifeguard: long
orange bill, zinc-white nose, red swim trunks, silver whistle, red rescue
buoy tucked under one wing. Neutral pose, front and 3/4 views, plain cream
background, consistent design, soft golden light.
```

**Step B — the video prompt** (`wan-2-7-text-to-video` · `reference_image_urls: [pelican ref]` · `5s` · `16:9`):

```
Warm watercolor storybook style, golden-hour beach. The pelican lifeguard
from the reference stands relaxed on a crowded sand beach — then his eyes
snap wide as he spots something offshore. Signature dolly-zoom (contra-zoom):
the background rushes and stretches behind him while his face stays locked in
frame, the beach warping around his dawning horror. Gentle surf, a single dark
fin slicing the water in the distance, gulls scattering. Subtle handheld shake.
```

Negative prompt: `photorealistic, gore, extra limbs, text, watermark`

---

## Shot 4 — *Singin' in the Rain* (lamppost dance)

**Feature:** Generate the music first, then feed it as the **audio reference / bed** (`audio_url`) so the animation and cuts ride the beat. The 1930s rubber-hose look is an era-accurate nod to when the film is set.

**Step A — the track** (`elevenlabs-music`, async: `/audio/quote` → `/audio/queue` → `/audio/retrieve` · `duration_seconds: 25` · `force_instrumental: true` · keep ≤30s so it fits `audio_url`):

```
Joyful 1930s Hollywood musical number: bright stride piano, brushed drums,
plucky upright bass, playful clarinet, tap-dance rhythm, major key, ~140 BPM,
warm vintage recording. Instrumental.
```

**Step B — the video prompt** (image-to-video or `wan-2-7-text-to-video` · `audio_url` = the track above · match duration · `16:9`):

```
1930s rubber-hose cartoon, bouncy squash-and-stretch, glossy black-and-white
with a wet rain sheen. A cheerful cartoon cat in a soaked suit and hat swings
around a lamppost in a downpour, twirls a dripping umbrella, and splashes
through puddles — dancing in time to the music. Streetlight glow, rain streaks,
shimmering reflections on wet cobblestones, pure joy.
```

Swap the music bed for a **TTS voiceover** (`/audio/speech`, e.g. `tts-xai-v1`) if you'd rather demo narration over music — same `audio_url` slot.

---

## Feature coverage recap

| Feature | Where it lives | Shot |
|---------|----------------|------|
| Agentic chat → prompt authoring | Chat | 1 |
| Image generation → start frame | Studio / `/image/generate` | 2 |
| Image generation → reference image | Studio / `/image/generate` | 3 |
| Audio generation → audio reference / VO | `/audio/queue` or `/audio/speech` | 4 |

Four films, four characters, four styles, four workflows — one tour of Venice Studio.

## Links

- [Venice Video Studio](https://venice.ai/video)
- [Venice AI](https://venice.ai)
- [Venice API Docs](https://docs.venice.ai)
