# Make a synthetic person speak seven languages — prompt pack

Copy-paste prompts to invent a photorealistic person who doesn't exist, then make them say one line in all seven languages [Happy Horse 1.1](https://venice.ai) lip-syncs on Venice, each in front of a real-world landmark. Same face, same spot, the whole world changing behind them. Fill in anything in `[BRACKETS]` and run top to bottom.

> These are direct copy-paste prompts for [Venice Video Studio](https://venice.ai/video), not a mega-prompt for a language model. Paste each block straight into Venice.

**Two models, image-first (confirm the current IDs on Venice):**
- **`qwen-image-2-pro`** — generate the face (one portrait)
- **`qwen-image-2-pro-edit`** — optional: extra angles of the same face
- **`happy-horse-1-1-reference-to-video`** — make the face speak, per language

> **The two levers, kept separate:** (1) one **generated portrait + locked framing** (dead-center, static camera, the same every clip) hold the face and never change; (2) your **video prompt** sets the line, names the language, and describes the backdrop, and is the only thing that changes between languages.

---

## Step 0 — Set up once

```
- Your line (short, one or two sentences): "[YOUR LINE IN ENGLISH]"
- Look of the person: [AGE], [HAIR], [COMPLEXION], [ANY GLASSES/JEWELRY]
- Wardrobe: [SPECIFIC TOP + COLOR]
- Framing: medium shot, dead-center, static camera (keep this constant every clip)
- Languages you want: [PICK FROM: English, Mandarin, Cantonese, Japanese, Korean, German, French]
- Backdrop per language: a landmark from where it's spoken (suggestions in Step 3)
```

---

## Step 1 — Invent the face (`qwen-image-2-pro`)

One clean portrait. This single image becomes your locked reference for every clip.

```
Photorealistic portrait of a [AGE] [PERSON], [HAIR], [COMPLEXION], calm neutral expression,
looking straight into the lens. Even soft light, plain mid-gray background, head and shoulders
centered, sharp focus, natural skin texture, wearing a [WARDROBE]. Believable real photograph
of an ordinary person who resembles no public figure or celebrity.
```

Negative prompt:

```
cartoon, illustration, 3d render, plastic skin, oversaturation, celebrity likeness,
recognizable public figure, extra fingers, distorted features, watermark, text
```

> **Lock this image.** It never changes. It's the only reason every clip reads as the same person.
> Optional: with `qwen-image-2-pro-edit`, ask for "the same person, slight three-quarter turn" to get a couple of backup angles.

---

## Step 2 — Settings for every clip

```
Model:        Happy Horse 1.1 (reference-to-video)
Reference:    your Step 1 portrait — identical for all languages
Framing:      medium shot, dead-center, static camera — identical for all languages
Duration:     ~4–5s
Resolution:   720p for drafts → 1080p for the keepers
Aspect ratio: 9:16 for the feed (also render 16:9 if you want a wide cut)
Audio:        ON
Music:        none at generation (add later in the Movie Editor, if at all)
```

> Run **Quote** before **Queue** so you see the cost first. Draft on 720p; only finalize the takes you keep at 1080p.

Reusable negative prompt (paste into every clip):

```
background music, score, soundtrack, subtitles, captions, on-screen text, warped mouth,
frozen lips, out-of-sync audio, distorted face, identity drift, extra fingers, oversaturation
```

---

## Step 3 — The shared video skeleton

Paste for every language. The **language name**, the **quoted line**, and the **`[BACKDROP]` / `[AMBIENT]`** change between clips; your person and framing stay identical.

```
Medium shot of [the person], centered in frame, static locked camera, outdoors with [BACKDROP],
soft daylight, shallow depth of field so the landmark reads softly behind them. They look
directly into the lens, calm and unreadable. They say, in [LANGUAGE]: "[YOUR LINE IN THAT
LANGUAGE]" Natural blinking, subtle head movement, precise lip-sync. Ambient: [AMBIENT],
no music. Keep their exact face, hair, and [WARDROBE] from the reference image.
```

> **Name the language before the quote** — that's the cue the lip-sync engine uses. One short line, one speaker, lip-syncs cleanest.

**Suggested landmark per language (swap in your own):**

```
English    → London, Tower Bridge
Mandarin   → the Great Wall of China
Cantonese  → Hong Kong, Victoria Harbour
Japanese   → Mount Fuji
Korean     → Seoul, Gyeongbokgung Palace
German     → Berlin, Brandenburg Gate
French     → Paris, the Eiffel Tower
```

> Lip-sync is trained for these seven languages only. Others will render, but the mouth match is only guaranteed for these. **Have a native speaker check your translation** before you finalize — bad phrasing shows up on the lips.

---

## Step 4 — Optional opener / kicker: rapid-fire backdrops

A short shot where the person holds dead-center while the world strobes behind them. Great as a cold open or a closing card. No dialogue (cycling many backdrops plus lip-sync in a few seconds is too much for one generation), so these are pure visual flourishes. Same settings as above (reference-to-video, your Step 1 portrait, 720p draft, audio on, 9:16).

**A. Daytime rapid-fire (~3s, twelve locations)**
```
Medium shot of [the person], centered in frame, static locked camera, holding the exact same
position the entire time, calm and unreadable, looking directly into the lens. Their lighting,
scale, and position never change. Behind them, the outdoor background strobes through many
real-world landmarks in super rapid-fire succession, a relentless machine-gun sequence of hard
cuts with no hold and no breathing room, each location on screen for only a fraction of a second
before snapping to the next: Mount Fuji, the Great Wall of China, the Eiffel Tower, Gyeongbokgung
Palace, the Brandenburg Gate, Victoria Harbour, Tower Bridge, the Statue of Liberty, the Sydney
Opera House, the Colosseum in Rome, the Taj Mahal, Christ the Redeemer over Rio. Prioritize the
speed and density of the cuts over clarity of any single shot; it should feel like the whole world
is flickering past behind a person who never moves. Soft daylight on them throughout. Ambient: a
fast stutter of airy whooshes, no music, no dialogue. Keep their exact face, hair, and [WARDROBE]
from the reference image.
```

**B. Day-into-night rapid-fire (~3s, twelve locations)**
```
Medium shot of [the person], centered in frame, static locked camera, holding the exact same
position the entire time, calm and unreadable, looking directly into the lens. Their scale and
position never change. Behind them, the outdoor background strobes through many real-world
landmarks in super rapid-fire succession, a relentless machine-gun sequence of hard cuts with no
hold and no breathing room, each location on screen for only a fraction of a second before
snapping to the next: Mount Fuji, the Great Wall of China, the Eiffel Tower, Gyeongbokgung Palace,
the Brandenburg Gate, Victoria Harbour, Tower Bridge, the Statue of Liberty, the Sydney Opera
House, the Colosseum in Rome, the Taj Mahal, Christ the Redeemer over Rio. Across this succession
the time of day continuously advances from bright midday sun, into warm golden hour, into deep
blue dusk, into full night with city lights and stars, so the early landmarks are sunlit and the
final ones are dark and glowing. The light on their face shifts with it, from cool daylight to
warm sunset glow to dim nighttime, while everything else about them stays identical. Prioritize
the speed and density of the cuts over clarity of any single shot. Ambient: a fast stutter of airy
whooshes settling into quiet night air, no music, no dialogue. Keep their exact face, hair, and
[WARDROBE] from the reference image.
```

**C. Speaking over the rapid-fire (~5s, day-into-night)** — the line delivered while the world strobes and the sun sets behind them. The most demanding shot in the pack; expect to reshoot.
```
Medium shot of [the person], centered in frame, static locked camera, holding the exact same
position the entire time, looking directly into the lens, calm and unreadable. Their scale and
position never change. They say, in clear English: "[YOUR LINE]" Natural blinking, subtle head
movement, precise lip-sync. Behind them, the outdoor background strobes through many real-world
landmarks in super rapid-fire succession, a relentless machine-gun sequence of hard cuts with no
hold and no breathing room, continuing the entire time they speak: Mount Fuji, the Great Wall of
China, the Eiffel Tower, Gyeongbokgung Palace, the Brandenburg Gate, Victoria Harbour, Tower
Bridge, the Statue of Liberty, the Sydney Opera House, the Colosseum in Rome, the Taj Mahal,
Christ the Redeemer over Rio. As they speak, the time of day continuously advances from bright
midday sun, into warm golden hour, into deep blue dusk, into full night with city lights and
stars. The light on their face shifts with it, while everything else about them stays identical.
Ambient: just their voice, very faint airy motion behind it settling into quiet night air, no
music. Keep their exact face, hair, and [WARDROBE] from the reference image.
```

> **Honest note:** many hard background swaps with a locked foreground (and lip-sync, for C) push the model hard. It may smear the cuts or drift the subject. Reshoot a few times, and if it won't hold, the bulletproof fallback is the editor: generate one clean plate of the person, then strobe the backdrops behind them on the timeline where you control the exact frames per location.

---

## Step 5 — Finalize, cut, loop

1. Pick the keeper per language.
2. Re-render only those at **1080p**.
3. **Movie Editor:** lay the clips in order, hard cuts (~3s each). Lead with the least-expected language; end with the one your audience reads.
4. Add a kicker card at the end (plain background, sentence case), e.g. **seven languages. no name attached.**
5. Match the last frame to the first so it **loops**. Export.

---

## Optional — a soundtrack prompt

Instrumental and sparse so it never fights the spoken lines, hypnotic to match the locked-center face, with a clean resolve under the kicker. Loopable, since the video loops. Paste into your music generator of choice.

```
Instrumental cinematic electronic cue, 40 seconds, no vocals, no spoken word. A hypnotic analog
synth arpeggio (16th-note sequence, slightly detuned, soft attack) carries the whole track,
panning gently. Underneath, a tinge of orchestra: warm sustained string pad and occasional low
cello swell, a single soft timpani hit on phrase changes. Mood: enigmatic, modern, a little
uncanny and unplaceable, quietly building. Keep it minimal and uncluttered with lots of headroom
so dialogue sits on top. Subtle four-on-the-floor pulse or muted kick, no busy percussion, no big
drop. Around 0:30 let the strings swell and the arpeggio thin out into a clean, suspended resolve
for an end card, then settle so the last bar loops back to the first seamlessly. Tempo 112 BPM,
key A minor, airy reverb, polished but restrained.
```

---

## Quick tips

- **Invent the face first** — one locked portrait is what keeps the same person across every clip.
- **Name the language before the line** — it cues the lip-sync.
- **Change only three things per language:** the language, the translated line, the backdrop.
- **Draft on 720p, finalize on 1080p** — you only pay full resolution for keepers.
- **Quote before Queue** so the cost is never a surprise.
- On Venice your request runs through **anonymized routing**: the model that generates the video doesn't learn who asked. Anonymized, not fully private. An invented face, and an anonymous author. Start at [Venice](https://venice.ai).
