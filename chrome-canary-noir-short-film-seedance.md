# The Chrome Canary — a complete noir short film with Seedance 2.0 R2V

A full 22-shot prompt pack for making a ~2:30 retro-futurist film-noir short in
[Venice Studio](https://venice.ai/video) with **Seedance 2.0 R2V enhanced** at
**21:9**. This is the companion pack to the Learn Venice long-form guide
"How to Make an Entire Short Film with Venice Studio."

**The story:** Meridian City, a 1958 that never was. A robot torch singer
witnesses a murder — and the only man who'll take her legally-worthless
testimony is a washed-up ex-cop who owes money to the mob that built her.
Bittersweet three-act noir: the truth gets out, but everyone pays for it.

**How this pack works:**

1. Generate the **15 reference images** (character sheets, location plates,
   prop, style key-frame). Every downstream prompt consumes them. We used
   `gpt-image-2` at `21:9 / 1K` after a five-model bakeoff — confirm current
   models with `GET /models?type=image`.
2. For each shot, generate a **storyboard frame** (the shot's first/key frame)
   using the listed refs as image references.
3. Feed the storyboard frame + refs into **Seedance 2.0 R2V enhanced** with the
   shot's video prompt. Keep motion intensity LOW unless the prompt says
   otherwise — noir reads as expensive when it's still. Generate every clip
   with model audio OFF — narration and music are separate passes (Parts 3–4).
4. Render the **voice-over** (Part 3) and the **score + Evie's song** (Part 4),
   then mix under the cut.

**Global style block — append to every image prompt:**

```
1950s Technicolor film noir, dieselpunk retro-futurism, anamorphic 21:9
cinematic still, deep crushed blacks, tobacco smoke haze, film grain and
halation, palette of brass, cream chrome, oxblood leather with canary-yellow
and neon-magenta accents only, shot on vintage anamorphic lenses, cinematic
key lighting
```

**Global suffix — append to every video prompt:**

```
1950s Technicolor film noir, dieselpunk retro-futurism, anamorphic 21:9,
heavy atmosphere, drifting tobacco smoke, film grain and halation, deep
crushed blacks, canary-yellow and neon-magenta accents only, subtle
naturalistic motion, no camera shake
```

---

## Part 1 — Reference images (generate these first)

Character refs use a **two-stage workflow** so every angle is the same
character, not a lucky re-roll:

1. **Masters (generate):** REF-01, REF-04, REF-06 — front-facing, full-body,
   plain backdrop, nothing else in frame. Generate with a text-to-image model
   (we used `gpt-image-2`). Retry until you love them; everything inherits
   from these.
2. **Derivatives (edit):** REF-02, REF-03, REF-05, REF-07 — feed the approved
   master into an image *edit* model (`POST /image/edit`, we used
   `gpt-image-2-edit`) with a "this exact same character, now …" prompt. The
   edit model preserves identity far better than re-prompting from scratch.

Keep character sheets sterile: plain backdrop, no set dressing, no
storytelling. Atmosphere (rain, neon, venetian blinds) belongs in the
location plates and storyboard frames — bake it into a character ref and it
follows the character into every shot.

| # | Ref | Stage | What it locks |
|---|-----|-------|----------------|
| REF-01 | Evie, front | master | Lead character master sheet |
| REF-02 | Evie, profile | edit of REF-01 | Turnaround + chest panel location |
| REF-03 | Evie, face + open chest panel | edit of REF-01 | The memory-spool reveal |
| REF-04 | Jack Marlow, front | master | Second lead master sheet |
| REF-05 | Jack, face detail | edit of REF-04 | Close-up coverage |
| REF-06 | Mr. Graves, front | master | The heavy (chrome left hand) |
| REF-07 | Graves' chrome hand | edit of REF-06 | Insert-shot prop-hand |
| REF-08 | City aerial plate | generate | Establishing world |
| REF-09 | Street plate | generate | Club district block |
| REF-10 | Alley + club door | generate | The canary neon door |
| REF-11 | Lounge interior | generate | The High Orbit club |
| REF-12 | Jack's office | generate | Venetian-blind interior |
| REF-13 | Rooftop plate | generate | Act III location (dawn seam) |
| REF-14 | The spool (prop) | generate | Glowing original + inert blank |
| REF-15 | Style key-frame | generate | Grade anchor |

**Character-sheet style block — append to the three master prompts (replaces
the global style block for character sheets):**

```
Plain seamless dark charcoal studio backdrop, no scenery, no props, no
furniture, no signage, no text, no lettering, nothing else in frame — the
character only. Even cinematic studio key lighting with soft rim light,
1950s Technicolor film noir grade, subtle film grain and halation, deep
crushed blacks, anamorphic 21:9 character reference sheet.
```

### REF-01 — Evie, front (master · generate)

```
Full-body front-facing studio portrait of a beautiful feminine torch-singer
automaton, model Canary C-3, standing centered and perfectly still, arms
relaxed at her sides: elegant cream-and-brass chrome body with art-deco
panel seams like coachwork on a luxury sedan, sculpted art-deco facial
plates, glowing amber vacuum-tube eyes behind small glass lenses, a
luxurious canary-yellow feather boa draped over her shoulders, a small
closed rectangular chest panel with brass hinges over her sternum.
```

### REF-02 — Evie, profile (edit of REF-01)

```
Turn this exact same automaton to a full left side profile view, same
full-body framing, same pose discipline (standing perfectly still, arms at
sides), same canary-yellow feather boa now trailing down her back, her small
closed rectangular chest panel with brass hinges visible in profile over her
sternum. Keep the identical plain dark charcoal studio backdrop, identical
lighting, nothing else in frame.
```

### REF-03 — Evie, face + chest panel detail (edit of REF-01)

```
Close-up detail sheet of this exact same automaton: left half of frame her
face in left profile with glowing amber vacuum-tube eyes; right half of
frame her chest panel hinged open with watchmaker precision revealing a
small brass wire memory spool glowing faintly amber inside a velvet-lined
cavity. Keep the identical plain dark charcoal studio backdrop and lighting,
no text, no nameplates, no lettering, nothing else in frame.
```

### REF-04 — Jack Marlow, front (master · generate)

```
Full-body front-facing studio portrait of a world-weary private investigator
standing centered, mid-40s, rumpled grey three-piece suit, loosened dark
tie, grey fedora, two days of stubble, tired perceptive eyes, a lit
cigarette in his right hand with smoke curling up.
```

### REF-05 — Jack, face detail (edit of REF-04)

```
Close-up head-and-shoulders portrait of this exact same private
investigator: fedora brim shading his tired perceptive eyes, stubble,
loosened tie, cigarette smoke drifting past his face, one half of his face
cut by a hard venetian-blind slash of shadow, warm key light. Keep the
identical plain dark charcoal studio backdrop, nothing else in frame.
```

### REF-06 — Mr. Graves, front (master · generate)

```
Full-body front-facing studio portrait of an immaculate mob enforcer
standing centered: tall, unhurried posture, perfectly tailored black suit,
black leather glove on the right hand only, the left hand a polished chrome
prosthetic with art-deco knuckle segments, a black umbrella furled at his
side.
```

### REF-07 — Graves' chrome hand detail (edit of REF-06)

```
Extreme close-up of this exact same enforcer's polished chrome prosthetic
left hand with art-deco knuckle segments, fingers slightly curled at rest,
black suit cuff and white shirt cuff behind it, neon-magenta reflections
sliding across the chrome, shallow depth of field. Keep the plain dark
charcoal studio backdrop, nothing else in frame.
```

### REF-08 — City plate (aerial, night rain)

```
High aerial establishing plate of a retro-futurist 1958 megacity at night in
heavy rain: Raygun Gothic towers with rounded chrome crowns, zeppelins
drifting between buildings with searchlights, glowing Nixie-tube signage,
elevated highways with finned atomic sedans, a magenta neon haze rising from
the entertainment district below, no text, no people.
```

### REF-09 — Street plate (club district)

```
Street-level establishing plate of a 1958 retro-futurist club district at
night in rain: wet asphalt mirroring magenta neon, finned atomic sedans with
chrome bumpers, pedestrians under black umbrellas, Nixie-tube marquee signs,
steam rising from grates, an alley mouth visible between two buildings, no
readable text.
```

### REF-10 — Alley + club door plate

```
Narrow brick alley at night in rain: wet cobblestones, steam vents, iron fire
escapes, and at the far end a chrome art-deco club door beneath a glowing
canary-yellow neon sign shaped like a singing bird, warm light leaking around
the door frame, yellow neon reflected in a long puddle leading to the door.
```

### REF-11 — Lounge plate (The High Orbit interior)

```
Interior establishing plate of a smoky 1958 art-deco supper club:
chrome-trimmed stage with a single canary-yellow spotlight, round tables with
low lamps, tufted oxblood leather corner booths, tobacco smoke hanging in
layered light, magenta neon bleeding through front windows, a chrome
microphone on the stage, empty of people.
```

### REF-12 — Jack's office plate

```
Interior plate of a 1958 private investigator's office at night: frosted
glass door, slow ceiling fan, venetian blinds cutting street-neon light into
hard slashes across a cluttered desk, Nixie-tube desk clock glowing,
cigarette smoke layering the air, rain on the window, empty of people.
```

### REF-13 — Rooftop plate

```
Rooftop above a shuttered nightclub: a huge dead neon canary sign unlit, a
zeppelin mooring mast rising into rain, wet gravel and vents, the
retro-futurist city sprawl beyond, and on the far horizon the first grey-gold
line of dawn breaking under the storm clouds, no people.
```

### REF-14 — The spool (prop sheet)

```
Product-photography style sheet of a small brass wire memory spool on black
velvet: two views, one intact and faintly glowing amber along its wound wire,
one identical but dark and inert, watchmaker detail, macro lens.
```

### REF-15 — Style key-frame (grade anchor)

```
A rain-streaked window at night, magenta neon and canary-yellow neon
reflected side by side in the glass, cigarette smoke drifting through a slash
of venetian-blind light, deep crushed blacks, film grain and halation.
```

---

## Part 2 — The 22 video generation prompts

Duration is per clip. **Inputs** = which storyboard frame + reference images
to attach in Studio. The opening is a deliberate funnel — city, block, alley,
reveal — each shot physically closer to Evie.

### ACT I — The Witness

**VID-01 — The City** · 8s · *refs: REF-08*

```
Slow forward aerial drift over the rain-soaked retro-futurist city at night.
Zeppelins drift laterally between towers, their searchlights sweeping slowly.
Rain falls through neon haze; signage flickers gently. Elevated traffic
streams like tracer light far below. Camera: continuous slow dolly forward
with a very slight downward tilt, as if beginning a descent.
```

**VID-02 — The Block** · 6s · *refs: REF-09*

```
Street-level: finned atomic sedans hiss through the frame left to right,
tires throwing fine spray, neon reflections rippling in the wet asphalt.
Pedestrians with umbrellas cross mid-ground. Steam pulses from a grate.
Camera: slow steady push-in toward the dark alley mouth between buildings,
gradually letting traffic exit the frame.
```

**VID-03 — The Alley / The Door** · 6s · *refs: REF-10*

```
Continuous slow push down the rain-slicked alley toward the chrome club door.
The canary-yellow neon bird sign buzzes and flickers subtly; its reflection
trembles in the long puddle. The brass doorman-automaton pulls the door
wider; warm light and a wedge of smoke spill out, muffled jazz implied by
pulsing light from inside. Camera: single unbroken dolly-in ending close on
the glowing doorway.
```

**VID-04 — Evie, Mid-Song (reveal)** · 8s · *refs: REF-01, REF-11*

```
Slow push-in from the back of the smoky supper club toward the stage. The
chrome torch singer sways almost imperceptibly as she sings into the chrome
microphone, feather boa stirring, amber tube eyes glowing warmly. Smoke
drifts through the canary spotlight beam; silhouetted patrons shift subtly in
foreground bokeh. Camera: slow dolly-in through the tables, low angle rising
slightly. Motion intensity: LOW.
```

**VID-05 — The Room** · 5s · *refs: REF-11*

```
Static-feeling slow lateral drift across the audience in the smoke. In the
corner booth, the silver-haired man in the white dinner jacket gestures
sharply in a quiet argument; the dark-suited man opposite remains utterly
still, back to camera. Table lamp flames flicker. Camera: very slow lateral
track right, shallow focus finding the booth.
```

**VID-06 — The Reflection (the murder)** · 6s · *refs: REF-03, REF-11*

```
Extreme close-up held on the chrome microphone head. In its warped
reflection, a small brilliant muzzle flash blooms twice from the distant
booth; the reflected room erupts into tiny chaos while the singer's amber
tube eyes, soft behind the mic, flare brighter. Her lips keep singing.
Camera: locked off, focus locked on the chrome. Motion intensity: LOW except
the flash.
```

**VID-07 — Panic** · 5s · *refs: REF-01, REF-11*

```
Wide: the room erupts — patrons surge from tables, a chair topples, smoke
swirls violently, the house lights cut to pulsing red emergency lamps. On
stage the chrome singer stands perfectly motionless in her failing spotlight,
the one still point in the frame. Camera: locked wide, letting chaos move
through composition. Motion intensity: HIGH in crowd, ZERO on her.
```

**VID-08 — The Alley Escape** · 6s · *refs: REF-02, REF-10*

```
The chrome door swings open hard, spilling red emergency light into the
alley. The automaton steps out into the rain, stops dead for one beat —
perfectly still — then walks quickly toward camera and past frame edge,
yellow boa trailing, rain beading and streaming off her cream-and-brass
shoulders. The neon canary buzzes overhead. Camera: static low angle, she
moves through the frame.
```

### ACT II — The Long Rain

**VID-09 — Jack's Door** · 5s · *refs: REF-12*

```
Dim hallway, held frame on the frosted glass door. The chrome silhouette
resolves against the glass, hesitates, then knocks three times — measured,
even, mechanical. The desk lamp glow inside shifts as someone stirs. Camera:
locked off. Sound-driven shot; keep motion minimal.
```

**VID-10 — The Office / The Ask** · 8s · *refs: REF-01, REF-04, REF-12*

```
Two-shot in venetian-blind light. The detective leans back, drags on his
cigarette, exhales a long slow cloud through the light slats, and shakes his
head once — no. The chrome singer does not move at all; only her amber eyes
dim slightly. The ceiling fan turns lazily; blind shadows breathe with it.
Camera: imperceptible push-in. Motion intensity: LOW.
```

**VID-11 — The Spool (the hook)** · 6s · *refs: REF-03, REF-05*

```
Close: the chest panel opens with watchmaker precision — small hinged plates
unfolding — revealing the brass memory spool glowing faintly amber, wire
catching the lamplight. In soft background, the detective's shadow-cut face
turns fully toward it; his cigarette smoke stops rising as he holds his
breath. Camera: slow micro push-in on the spool.
```

**VID-12 — Graves Introduced** · 7s · *refs: REF-06, REF-07, REF-11*

```
The wrecked club in magenta window light. The man in black speaks — calm,
unhurried, lips barely moving — while his chrome left hand drums four slow
fingers on the bar top, magenta reflections sliding across each knuckle. The
bartender flinches at each tap. Camera: slow dolly-in on the hand, then tilt
up to his placid face.
```

**VID-13 — Kessler's Tube & Pawn** · 7s · *refs: REF-02, REF-04, REF-14*

```
Amber-lit repair den. The duplication rig spins both spools slowly — one
glowing, one dark — thin wire whispering between them. The old technician
adjusts his magnifying visor; the chrome singer watches her own memory being
copied, motionless; the detective wipes fog from the rainy window and peers
out. Vacuum tubes pulse gently on the shelves. Camera: slow lateral track
across the bench.
```

**VID-14 — The Near Miss** · 7s · *refs: REF-06, REF-09*

```
Rain hammers under the mooring mast. The detective pulls the chrome singer
back into doorway shadow — one sharp motion, then both freeze. The long
black sedan glides through frame left to right, slow as a shark, wipers
ticking, the chrome prosthetic hand resting motionless on the window sill.
It does not stop. Spray drifts in its wake. Camera: locked in the shadow
with them, watching it pass.
```

**VID-15 — Headlights** · 5s · *refs: REF-01, REF-05*

```
Interior of the parked coupe. Rain crawls down the windshield; oncoming
headlights bloom and slide across the glass as bokeh. The detective turns
his head to look at her; her amber tube eyes glow steady while every other
light in frame smears and moves. Neither speaks. Camera: locked off from the
dash. Motion intensity: LOW.
```

**VID-16 — The Realization** · 6s · *refs: REF-04, REF-12*

```
Under the desk-lamp cone: the detective's hands move photographs and slide a
finger down a ledger column, stopping on a repeated name. He goes still. His
head lifts slowly toward someone off-frame, lamplight catching the change in
his eyes. Smoke drifts through the lamp beam. Camera: slow push-in over the
desk toward his face.
```

### ACT III — The Spool

**VID-17 — The Rooftop Summons** · 7s · *refs: REF-04, REF-06, REF-13*

```
Wide rooftop, rain thinning to drizzle. The stairwell door opens; the
detective steps out, collar up, and walks slowly across the wet gravel
toward the waiting man in black, who does not move at all beneath his
umbrella. The dead neon canary sign looms unlit between them. Camera: slow
crane down from sign height to eye level as the detective crosses.
```

**VID-18 — The Offer** · 8s · *refs: REF-04, REF-06, REF-13*

```
Extreme wide two-shot held. The man in black extends his chrome hand palm-up
and holds it there, patient, rain threading between the two men. With the
gloved hand he raises the slim ledger slightly — the whole offer in one
gesture. The detective's coat moves in the wind; he doesn't answer. Camera:
locked off, tableau; only rain, wind, and the two small figures move.
```

**VID-19 — The Handoff (the lie)** · 6s · *refs: REF-05, REF-07, REF-14*

```
Tight insert: the weathered hand lowers the brass spool into the chrome
palm; the prosthetic fingers close over it one segment at a time, rain
beading on the metal. Rack focus up to the detective's face: nothing. A drop
falls from his hat brim. Camera: locked, single rack focus. Motion
intensity: VERY LOW.
```

**VID-20 — Graves Departs / Dawn** · 6s · *refs: REF-08, REF-13*

```
From the rooftop edge: far below, the black sedan pulls away up the wet
street, taillights smearing. On the horizon the storm clouds split and a
grey-gold seam of dawn widens — the first dry light of the film crawling
across the rooftops. In foreground a match flares; cigarette smoke crosses
the frame. The dead canary sign flickers once, half-lighting. Camera: slow
tilt up from street to horizon.
```

**VID-21 — The Papers** · 5s · *refs: REF-15*

```
The pressroom thunders: rollers spin, a river of front pages races through
the machines in rhythmic motion, ink misting, morning light strobing through
the works. One paper snaps toward camera and holds nearly full-frame for a
beat before whipping away. Camera: locked amid the machinery. Motion
intensity: HIGH, mechanical, rhythmic.
```

**VID-22 — The Dockside Bar (ending)** · 8s · *refs: REF-01, REF-04*

```
Dawn shafts through dusty windows. On the tiny corner stage the chrome
singer sways gently, singing — no spotlight, no boa, dust motes drifting
through the gold light around her. The detective listens at the back table,
thumb turning his coffee cup once. Camera: very slow pull-back through the
whole room, widening until both are small in the warm light. Hold. Fade to
black. Motion intensity: LOW.
```

---

## Continuity & retry notes

- If a character drifts off-model, raise the weight/priority of their REF
  images and simplify the action verbs — Seedance holds identity best when
  each clip contains ONE primary action.
- Never ask two characters to do separate complex actions in one clip; split
  into coverage (that's why the murder is two shots, 05 + 06, and the rooftop
  deal is two shots, 18 + 19).
- Regenerate cheap wide shots (01, 02, 21) last — spend retries on faces.
- Keep motion intensity LOW by default. The one deliberate exception is
  shot 07: chaos everywhere EXCEPT the motionless subject — the most
  instructive Seedance motion-direction exercise in the pack.

---

## Part 3 — Voice-over narration (TTS)

Jack Marlow narrates the whole film — no on-camera dialogue. That means every
video clip should be generated with **model audio OFF / muted** so Seedance
can't synthesize a competing narrator, and the VO is rendered separately and
laid over the cut.

The full timed script (~230 words) is below. It is deliberately sparse —
silence is a tool; shots 05–07 and 19 carry no VO on purpose. At noir cadence
(~110 wpm) it fills roughly 2:05 of a 2:45 cut, leaving room for the song and
the silences.

### The VO script (Jack Marlow)

**[Shots 01–03 — the funnel into the club]**

> Meridian City. Nineteen fifty-eight. The future showed up fifteen years
> early, and the first thing it learned to do was look the other way.
>
> Every joint in town ran on tubes and small favors. The machines poured the
> drinks, sang the songs, took the fall. Nobody watched what they said in
> front of the help.

**[Shot 04 — Evie reveal]**

> That was the night the help started listening.

**[Shots 05–07 — the murder]** *(no VO — let the reflection play in silence,
music only)*

**[Shot 08 — alley escape]**

> Sonny Vale caught two in his own booth, and the only witness in the room
> wasn't legally a person.

**[Shots 09–10 — Jack's office]**

> She found me the way trouble always finds me. Through the door marked
> "machine claims." I told her no. I want that on the record — I told her no.

**[Shot 11 — the spool]**

> Then she opened up her chest and showed me the truth on a brass spool, and
> I remembered why they took my badge.

**[Shot 12 — Graves]** *(no VO until the last second)*

> The Belmontes sent Graves. They always send Graves.

**[Shots 13–15 — the run]**

> A machine's memory is property. Copy it, and it fades — like a song you
> only half remember. Kessler made us two spools: one true, one blank. She
> paid for it with a piece of what she saw.

**[Shot 16 — the realization]**

> That's when it added up. The spool didn't just name the shooter. It named
> the men I owed money to.

**[Shots 17–18 — rooftop]**

> Graves offered me the cleanest deal I ever heard. My whole ledger, gone,
> for one spool of wire. All I had to do was hand over the only honest
> witness in Meridian City.

**[Shot 19 — the handoff]** *(no VO — the lie plays silent)*

**[Shot 20 — dawn]**

> He'd know by morning. Some checks you write knowing they'll bounce.

**[Shot 21 — the papers]**

> The courts couldn't touch a spool of wire. Turns out the morning edition
> could.

**[Shot 22 — dockside bar, close]**

> Her testimony was worthless in any court in the country. Cost me everything
> anyway.
>
> *(beat — she sings)*
>
> Some songs are like that.

### Rendering the VO

**Voice settings (Venice TTS, `tts-kokoro`):**

| Setting | Value |
| --- | --- |
| model | `tts-kokoro` |
| voice | `am_onyx` (deep gravel baritone — closest stock match for a noir PI) |
| speed | `0.92` (slower than natural; noir VO is unhurried) |
| format | `mp3` |

```bash
curl -s https://api.venice.ai/api/v1/audio/speech \
  -H "Authorization: Bearer $VENICE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "tts-kokoro",
    "voice": "am_onyx",
    "speed": 0.92,
    "response_format": "mp3",
    "input": "Meridian City. Nineteen fifty-eight. The future showed up fifteen years early, and the first thing it learned to do was look the other way."
  }' -o vo-shot-01.mp3
```

**Delivery direction (paste ahead of the line if your TTS route accepts
style hints, otherwise keep for a human/VO-model pass):**

```
Dry, unhurried, gravel and smoke. Classic 1950s film-noir private-eye
voice-over. Low pitch, flat affect, faint weariness, no theatricality.
Pause at every period. Never rush a sentence.
```

**Per-line rendering tip:** render each VO block as its own file, one per
shot group (01–03, 04, 08, 09–10, 11, 12, 13–15, 16, 17–18, 20, 21, 22),
rather than one long take — it lets you slide lines against picture in the
edit without re-rendering, and a re-roll of one flubbed line doesn't change
the timing of the rest.

---

## Part 4 — Music (score prompt)

One continuous cue works for the whole short (and for the teaser cut): noir
scores of the era were through-composed, not needle-dropped. Generate at
full length, then duck it under the VO (music bed around −20 dB relative to
narration, swelling in the VO-free stretches: the murder 05–07, the
handoff 19, and Evie's final song 22).

**Main score prompt (any music model — e.g. `elevenlabs-music`):**

```
1950s film-noir score, slow-burn and smoky: a lonely muted trumpet melody
over sparse upright bass, brushed drums, and low tremolo strings. Torch-song
mood, late-night supper club after closing. Builds twice — a dissonant brass
stinger at the murder, a colder string swell for the betrayal — then resolves
into a tender solo piano-and-trumpet coda that ends on one sustained,
unresolved minor chord. Vintage analog warmth, mono-era room tone, tape hiss.
No modern drums, no synthesizers.
```

**Evie's song (diegetic, for shots 03–04 and 22 — generate separately):**

```
A slow 1950s torch song sung by a smoky female voice, close-mic'd on a ribbon
microphone with tube-amp warmth and gentle vinyl crackle. Sparse backing:
brushed drums, upright bass, a distant piano. Melancholy but composed —
a nightclub singer who knows the song is about her. Ends unresolved,
mid-phrase, as if interrupted.
```

**Mix notes:**

- VO on top (0 dB reference), music bed at −20 dB under narration,
  swelling to −12 dB in the VO-free stretches.
- The score and the diegetic song should never play at once: crossfade the
  club song INTO the score at the shot 04 → 05 cut (the moment the murder
  interrupts her set), and hand back to the song for shot 22.
- End the film on the song, not the score — the last sound is Evie,
  mid-phrase, unresolved.

---

## Part 5 — The teaser trailer (35–40s cut)

A self-contained 8-shot teaser you can produce before (or instead of) the
full short. It reuses the same refs and style blocks; shots 1–2 are the
existing city and alley plates, the rest are new setups. Every clip generates
with model audio OFF, same as the short.

### Trailer shot list

| # | Setup | Gen length | In the cut |
| --- | --- | --- | --- |
| T1 | Aerial over Meridian City (REF-08) | 5s | ~4s |
| T2 | Dolly down the alley to the club door (REF-10) | 5s | ~4s |
| T3 | Evie mid-song from the back of the room (REF-01) | 8s | ~6s |
| T4 | Muzzle flash in the chrome mic reflection | 5s | ~4s |
| T5 | Jack behind his desk, venetian-blind neon (REF-04) | 6s | ~5s |
| T6 | Chest panel open, the brass spool (REF-03) | 5s | ~4s |
| T7 | Graves' chrome hand drums on the bar (REF-07) | 5s | ~4s |
| T8 | Club in panic, Evie motionless + title card (REF-01) | 8s | ~7s |

Generate at full length, trim in the edit: ~38s picture. Hard cuts
throughout, fade to black on T8 under the title.

### Trailer VO script (Jack Marlow — single take, ~80 words)

Timed to the cut above at noir cadence (~110 wpm, speed 0.92). One line per
shot; T4 stays silent except the gunshot.

> **[T1]** Meridian City. Nineteen fifty-eight. A town that chromed its sins
> and called them progress.
>
> **[T2]** Down on Bird Street there's a club where the whiskey's honest —
> and nothing else is.
>
> **[T3]** They built her to sing. Nobody thought to ask what she'd remember.
>
> **[T4]** *(no VO — one gunshot, then silence)*
>
> **[T5]** I don't take cases with heartbeats anymore. Turns out she didn't
> have one.
>
> **[T6]** Everything she saw that night, wound onto three inches of brass
> wire.
>
> **[T7]** And the man who owns this town wants that wire... pulled.
>
> **[T8]** The Chrome Canary. Some songs don't die. They just change key.

Render it as one take (same `tts-kokoro` / `am_onyx` / speed 0.92 settings as
Part 3) — the trailer is short enough that a single file keeps the momentum,
and the T4 gap is cut in the edit, not the read. If the take lands long,
nudge speed to 0.95 before touching the script.

### Trailer music prompt

One cue, generated at 40–45s:

```
1950s film-noir trailer score, 40 seconds: smoky solo torch-song vocalise
over sparse upright bass and brushed drums, slow-burn build with dissonant
brass swells, a sudden hard stinger at the midpoint, then a final swell that
cuts to one sustained unresolved minor chord under the title. Vintage analog
warmth, mono-era room tone, tape hiss. No modern drums, no synthesizers.
```

**Trailer mix notes:**

- Land the midpoint stinger exactly on T4's muzzle flash; if the generated
  cue's stinger drifts, slide the music, not the picture.
- Bed at −20 dB under VO, swelling to −14 dB across T4 and again under the
  title card.
- Last sound: the unresolved chord decaying under "They just change key,"
  then one beat of true silence before the end.
