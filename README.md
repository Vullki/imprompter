<div align="center">

<img src="assets/icon.svg" alt="Imprompter icon" width="72">

# Imprompter

**Turn any image into a detailed, copy-ready GPT Image prompt. Lift single traits from it, or find out why a regeneration drifted.**

[![License: MIT](https://img.shields.io/badge/License-MIT-black.svg)](LICENSE)
[![Agent Skill](https://img.shields.io/badge/Agent%20Skill-SKILL.md-555.svg)](https://agentskills.io)
[![Target](https://img.shields.io/badge/target-GPT--Image--2.6-777.svg)](#spec)

</div>

---

Most image-to-prompt tools give you a paragraph of adjectives and "8k, masterpiece". Imprompter reads an image the way an art director would, writes only what it can actually see, and tells you what it could not recover.

## What it does

| You give it | Mode | You get |
|---|---|---|
| An image, or "same as this" | **REPLICATE** | Settings, the 3-5 traits that make the image itself, a full prompt, a one-line reference prompt, and notes on what text cannot recover |
| An image + named traits ("just the palette and type") | **HARVEST** | One pasteable block per trait, with no trace of the source's subject |
| A source + its regeneration ("what's off?") | **REPAIR** | Up to 3 misses ranked by visual impact, and one edit prompt for the biggest |
| An idea, no image | **CREATE** | A committed, specific prompt with settings |
| Several images | Multi-image | A role for each (subject, style, background) and one combined prompt |

It covers photos, portraits, products, posters and typography, illustration and anime, infographics and UI, and collages.

## Why it's different

- **No guessing.** If it isn't visible, it isn't in the prompt. Counts and positions are written as measurements ("about 12"), and inferences like lens or film stock become appearance cues only.
- **Text handled properly.** Every legible line is quoted separately with position, typeface and line breaks. Unreadable text stays out and is flagged in the notes, with the readable part quoted so you can fill in the rest.
- **Defects reproduced, not hidden.** REPLICATE keeps the image as it is and lists the defects. Say "clean" to fix them.
- **The real medium.** It never defaults to photorealism or the model's house style.
- **Liftable sections.** FRAME, SETTING, FOCUS, ELEMENTS, COMPOSITION, LIGHT, PALETTE, MATERIALS, STYLE, TEXT, PRESERVE, EXCLUDE. Each one makes sense on its own.
- **Honest.** It never claims a prompt was tested unless it saw the result, and it does not generate images itself.

## Install

The skill is the whole folder. Keep the folder name `imprompter`.

**Claude Code**

```bash
git clone https://github.com/Vullki/imprompter.git ~/.claude/skills/imprompter
```

On Windows, `~/.claude` is `%USERPROFILE%\.claude`.

**claude.ai:** Settings → Capabilities → turn on code execution, then Customize → Skills → **+** → Upload a skill. Upload a ZIP whose root is the `imprompter` folder (so it contains `imprompter/SKILL.md`).

**Codex / ChatGPT:** `agents/openai.yaml` is included. Follow your host's skill-install path and keep that file in place.

Any agent that follows the [Agent Skills](https://agentskills.io) `SKILL.md` format can load it. The agent must be able to see images.

## Use it

Attach an image and say any of these:

- `imprompter` or `give me the prompt`
- `same as this, but on a white background`
- `just the lighting and palette`
- `here's the original and my regeneration, what's off?`
- `GPT Image prompt for a matte black watch on wet slate`

## SPEC

The model settings live in one dated block in `SKILL.md`, checked against OpenAI's image generation docs on 2026-11-26:

- **Models:** `gpt-image-2.6-sunburst` by default, `gpt-image-2.6-flare` for drafts
- **Quality:** `auto | low | medium | high | xhigh | max`
- **Complexity:** `low | medium | high` (default high)
- **Size:** multiples of 16, ratio 1:3 to 3:1, edges up to 3840, 655,360 to 8,294,400 pixels

When OpenAI ships a newer model, name it in your request and Imprompter will use it. If it has a search tool, it checks the new limits; if not, it tells you they are unverified.

## Limits

- It writes prompts for GPT Image. Other generators can use the prompt text, but the SETTINGS line is GPT Image's.
- It does not identify real people from their appearance, and it will not reproduce IDs, passports, currency or official documents.
- Signatures and watermarks are left out unless the image is yours.
- The [evals](evals/prompts.md) check output shape and rule-following. The latest run passed 10 of 10, graded by the same model that wrote the outputs, and GPT Image was not called, so how well a prompt regenerates its image is not measured.

## Package

```
imprompter/
├── SKILL.md
├── README.md
├── LICENSE
├── CHANGELOG.md
├── evals/prompts.md        # 10 behaviour checks
├── evals/results-*.md      # latest run: 10/10 (self-graded)
├── evals/fixtures/         # test images (left out of the release ZIP)
├── agents/openai.yaml
└── assets/icon.svg
```

## License

[MIT](LICENSE) · Built by [Vullki](https://vullki.com)
