# 360° product showcase video — prompt the spin, edit it by talking to an agent (template)

Turn one product photo into a polished, speed-ramped 360° showcase clip on [Venice](https://venice.ai).
Two moves: **prompt the spin in Studio, then describe the edit to an AI agent.** No video-editing
skills and no ffmpeg — you tell an AI coding agent what you want and it writes and runs the edit for
you, on your own machine. Fill in anything in `[BRACKETS]`, then run top to bottom.

**The models that do the work:**
- **`nano-banana-2`** — makes the hero product still (Studio → Image; aspect-ratio + resolution driven; ~$0.02/image).
- **an image-to-video model** (e.g. **`minimax-h3-max-image-to-video`**, Private on Venice) — films the 360° spin from that still. *The simple path — one prompt.*
- **`minimax-h3-max-multi-angle`** — the *precise* orbit on the Venice API/harness (Private tier), driven by an actual camera path. *The power path.*
- **`qwen3-coder-480b-a35b-instruct-turbo`** — a Private, code-optimized model that powers **OpenCode** and does all the editing (speed ramp, loop, formats, music) from plain-language instructions.

> **The one idea that makes it work:** a 360° orbit is easy to prompt, but a *constant-speed* orbit is a
> slow turntable nobody watches. What makes these clips look expensive is a **speed ramp** — the spin
> establishes slowly, whips through the middle, and decelerates onto the hero angle. You don't learn a
> video editor to do it. You describe the retime to an agent and it writes the command. The rule:
> **speed up going into a cut, slow down onto the thing you're selling.**

Swap the product, the finish, and the backdrop and the same template works for a sneaker, a watch, a
bottle, a gadget, or a cosmetics jar. A ready-made recipe is at the bottom.

---

## Step 0 — Set up once

**Fill in your product** (keep this handy; you'll paste pieces of it below):

```
- Product (make the brand fictional): [PRODUCT]     e.g. a faceted glass perfume bottle
- Material / finish:                  [MATERIAL]    e.g. faceted glass, brushed steel, matte plastic
- Any label / wordmark:               [LABEL]       keep it short; the model spells short words best
- Pedestal / surface:                 [SURFACE]     e.g. a dark stone pedestal
- Backdrop:                           [BACKDROP]    e.g. seamless deep-blue-to-black studio
- The hero angle (what you're selling): [HERO]      e.g. the front label — where the spin should settle
```

**Point OpenCode at Venice** (one time). In OpenCode, add a custom OpenAI-compatible provider — check
OpenCode's docs for the exact config keys:

```
Base URL:  https://api.venice.ai/api/v1
API key:   PASTE_YOUR_VENICE_API_KEY_HERE      # keep it private, never share or commit it
Model:     qwen3-coder-480b-a35b-instruct-turbo
```

You'll also need **ffmpeg** installed — OpenCode uses it for you; you never type ffmpeg yourself.

---

## Step 1 — Make the hero still — `nano-banana-2`

Studio → Image. Aspect `1:1`, resolution `2K`. It's about two cents an image, so make a few.

```text
Studio product photograph of [PRODUCT] made of [MATERIAL] with a minimal engraved "[LABEL]" wordmark, centered on [SURFACE] against a [BACKDROP]. Soft key light from the upper left, a crisp rim light catching the edges, a gentle reflection below. Photoreal, high detail, sharp focus, commercial beauty lighting.
Negative: extra objects, hands, clutter, distorted text, watermark.
```

Pick the cleanest, most **symmetrical** result — symmetry spins best.

**Not perfect? Edit it, don't re-roll it.** Open the still in Studio → Edit and change one thing:

```text
Keep this exact [PRODUCT], lighting, and background. Change only [ONE THING — the color / the label / the surface]. Don't change the shape or anything else.
```

Turning one image into exactly the one you want is the single most useful skill on Venice. Save the
result as your hero plate.

---

## Step 2 — Film the 360° spin (one prompt) — Studio → Video

Attach your still. **Draft a small version first** to check the motion, then render the keeper. Save
the finished clip as `orbit.mp4` in a new, empty folder.

```text
A smooth, continuous 360-degree orbit around the [PRODUCT]. The camera circles it one full turn at a steady eye-level height, keeping the [PRODUCT] perfectly centered and completely still. Slow, even motion; soft studio lighting with reflections sliding across it as it turns; shallow depth of field; the seamless backdrop stays behind it. One continuous take, no cuts, no camera shake.
```

Spec: `duration 8s`, aspect follows the image.

**Precise option (power path) — `minimax-h3-max-multi-angle` on the API.** For an exact, repeatable
orbit with real camera control. Requires a hosted `image_url`; the `camera_trajectory` carries the shot
(prompt optional). `azimuth` = horizontal degrees (360 = one turn), `elevation` = vertical degrees,
`distance` = 1 is unchanged (below 1 dollies in). Runs async: `POST /video/quote` → `/video/queue` →
poll `/video/retrieve` → `/video/complete`.

```json
{
  "model": "minimax-h3-max-multi-angle",
  "image_url": "https://<your-host>/hero-plate.png",
  "duration": "8s",
  "resolution": "768P",
  "camera_trajectory": [
    { "time": 0,   "azimuth": 0,   "elevation": 0, "distance": 1 },
    { "time": 0.6, "azimuth": 210, "elevation": 6, "distance": 0.92 },
    { "time": 1,   "azimuth": 360, "elevation": 0, "distance": 0.9 }
  ]
}
```

---

## Step 3 — The speed ramp (this is what makes it look expensive) — OpenCode

Open OpenCode **in the folder with `orbit.mp4`** and type these one at a time. You never write code —
you describe the edit.

**3.1 — Check the clip first:**

```text
This folder has one video, orbit.mp4 — an 8-second 360° spin of a product on a plain background. Run ffprobe and tell me its exact duration, fps, and resolution. Don't edit anything yet.
```

**3.2 — The ramp:**

```text
Retime orbit.mp4 into a speed ramp so it reads as an energetic product spin instead of a slow turntable. Split it into three segments and play each at a different speed:
  1) the first ~1.5 seconds at normal speed (1x) so the product registers,
  2) the middle of the spin sped up to about 4x so it whips around,
  3) the last ~1 second slowed to about 1.2x so it settles gently on [HERO].
Use ffmpeg setpts on trimmed segments and concat them. Keep it silent, keep the original resolution, output yuv420p, and save it as ramp.mp4. Then print the exact ffmpeg command you ran and the new total duration.
```

*(If [HERO] doesn't face the camera at the end of the orbit, tell the agent the timestamp where it does and ask it to land there.)*

**3.3 — Let it check its own work:**

```text
Grab a still frame at 0.3s, at the midpoint, and 0.2s before the end of ramp.mp4 and save them as check-1.png, check-2.png, check-3.png, so I can confirm it starts slow, speeds up in the middle, and settles at the end.
```

---

## Step 4 — Polish (one sentence each) — OpenCode

**Seamless loop** (so it autoplays without a visible jump):

```text
Make a clean seamless loop of ramp.mp4: crossfade the last 0.3s into the first 0.3s (a quick motion-blur whip is fine). Save it as ramp-loop.mp4.
```

**Every platform size:**

```text
From ramp-loop.mp4, export three versions: a 1080x1080 square, a 1080x1920 vertical (center-crop the subject, keep it centered), and a 1920x1080 widescreen (pad the sides with the same background, don't stretch). Name them ramp-square.mp4, ramp-vertical.mp4, ramp-wide.mp4. Keep yuv420p and faststart.
```

**Add music** (optional — generate a bed with Venice's music tool first and save it as `bed.mp3`):

```text
Lay bed.mp3 under ramp-square.mp4: trim the music to the video length, add a 0.25s fade-in and a 1.2s fade-out, normalize to about -14 LUFS, and mux it in. Save as final-square.mp4.
```

---

## Step 5 — Level up: many angles, one runaway spin — OpenCode

Film the spin three times (Step 2), changing "steady eye-level height" to **a low angle looking
slightly up**, **eye level**, and **a high angle looking slightly down**. Save them as
`orbit-low.mp4`, `orbit-eye.mp4`, `orbit-high.mp4`, then tell OpenCode:

```text
I have three clips — orbit-low.mp4, orbit-eye.mp4, orbit-high.mp4 — each a 360° spin of the same product at a different camera height. Speed-ramp each one the same way (slow in, fast through the middle), then chain them with fast 0.3s "whip" wind transitions so it looks like one continuous runaway spin that ends settled on [HERO]. Save as reel.mp4, 1080x1080, yuv420p, faststart. Print the commands.
```

---

## Make it your own (paste after it works)

```text
Change the settle to a slow full second at 1x and make the whole spin 20% faster overall. Save as ramp-punchy.mp4.
```
```text
Add a soft radial vignette and lift the contrast slightly so the product pops off the background. Keep the motion identical.
```
```text
Hold on the final settled frame for an extra 0.8 seconds so there's room for a logo or price.
```

---

## Ready-made recipe — a perfume bottle (fill the blanks)

Drop these into the **Step 0** blanks and run it as-is. `ONDA` is a made-up brand; swap in your own.

```
- Product:          a faceted hexagonal clear-glass perfume bottle filled with amber-gold liquid, a brushed-gold cap
- Material / finish: faceted clear glass and brushed gold
- Label / wordmark:  ONDA
- Pedestal / surface: a smooth dark stone pedestal
- Backdrop:          a seamless deep-blue-to-black gradient studio backdrop
- Hero angle:        the front of the bottle, so the engraved "ONDA" faces camera
```

Glass and liquid catch the light as the spin accelerates, which makes the speed ramp read clearly —
a good product to learn the technique on.

---

## How it works

- **Prompt the spin, describe the edit.** Generating a 360° orbit is one motion sentence over a still. The polish — the part that looks expensive — is a speed ramp you *delegate* to an agent instead of learning a video editor.
- **The agent runs on your machine.** OpenCode writes the ffmpeg and runs it locally. Your video files never get uploaded to the model — only your typed instructions do. The spin runs on a **Private** Venice model, so your product design isn't stored either. (It's Private-tier generation plus local editing — strong and honest, not end-to-end encryption.)
- **Draft small, then finish.** Never pay full resolution to find out the motion is wrong.
- **Symmetry spins best.** Pick the cleanest, most symmetrical still.
- **Speed up into cuts, slow down onto the product.** That's the whole choreography of a good showcase spin.

## Links
- [Venice AI](https://venice.ai) · [Venice Video Studio](https://venice.ai/studio/video) · [Venice API Docs](https://docs.venice.ai)
