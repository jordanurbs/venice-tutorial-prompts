# Venice Tutorial Prompts

Reusable prompt templates and agent skills for creating AI video and image content with [Venice AI](https://venice.ai).

## Templates

Mega-prompt templates designed to be pasted into a frontier language model. Fill in the **MY PROJECT** section, paste the whole doc, and get all prompts back.

| Template | Feature | Description |
|----------|---------|-------------|
| [Reference to Video](reference-to-video-prompt-generator.md) | Kling O3 R2V | Generates all Element reference images, Scene reference images, Start Frames, and Video Studio prompts for a Reference to Video project |
| [Build a Brand](build-a-brand-with-qwen.md) | Qwen 3.7 + Qwen Image 2 Pro | Step-by-step prompts to build a full brand — world, product, explainer, and launch campaign — with consistent copy and visuals |
| [Multilingual Talking Head](multilingual-talking-head-seven-languages.md) | Happy Horse 1.1 | Copy-paste prompts to invent a photorealistic person, then make them speak one line in all seven lip-sync languages, each in front of a landmark — plus rapid-fire backdrop and soundtrack prompts |

## Prompt packs

Ready-to-use prompts you can paste straight into Studio — no fill-in step.

| Pack | Feature | Description |
|------|---------|-------------|
| [Iconic Film Homages](iconic-film-homages-studio-feature-tour.md) | Studio feature tour | Four cartoon homages to famous films (*The Good, the Bad and the Ugly*, *2001*, *Jaws*, *Singin' in the Rain*), each demoing a different Studio-adjacent feature: agentic-chat prompt-writing, image start frame, image reference, and audio reference |
| [The Chrome Canary](chrome-canary-noir-short-film-seedance.md) | Seedance 2.0 R2V | A complete 22-shot noir short film in 21:9 — 15 reference image prompts, every video generation prompt, VO narration (TTS) settings, and score/torch-song music prompts with mix notes. Companion pack to the Learn Venice "make an entire short film" guide |

## Skills

Agent skills for AI coding assistants (Cursor, Claude Code, etc.) that automate the end-to-end production workflow.

| Skill | Description |
|-------|-------------|
| [venice-video-brief](skills/venice-video-brief/SKILL.md) | Generate complete video production briefs — story arcs, reference image prompts with identity lock, R2V video prompts, multi-shot storyboards, QA consistency checks, soundtrack prompts, and optional HTML presentation decks |

## How to Use

### Templates
1. Open a template
2. Fill in the **MY PROJECT** section with your details
3. Paste the entire document into a frontier model (Claude, GPT-4, etc.)
4. Use the generated prompts to create your assets on [venice.ai](https://venice.ai)

### Skills
1. Copy the `skills/` folder into your project's `.cursor/skills/` directory (or `~/.cursor/skills/` for personal use)
2. The agent will automatically detect and use the skill when relevant tasks are requested
3. Trigger by asking to create a "video brief," "R2V project," "video commercial," or "multi-shot storyboard"

## Links

- [Venice AI](https://venice.ai)
- [Venice Video Studio](https://venice.ai/video)
- [Venice API Docs](https://docs.venice.ai)
