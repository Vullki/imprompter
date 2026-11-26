# Changelog

All notable changes to Imprompter are recorded here. Dates are YYYY-MM-DD.

## [1.0.1] - 2026-11-26

First live eval run: 10 of 10 checks pass (self-graded; GPT Image was not called, so regeneration quality is not tested). The run exposed four gaps in the instructions, closed here.

### Changed
- REPAIR now ends with a SETTINGS line carrying complexity and quality, so the edit prompt says how to run it.
- HARVEST with a new subject now gives that prompt its own SETTINGS line.
- Text cut off by the frame edge is transcribed with a note on where the edge cuts it, instead of being treated as unreadable.
- A named model newer than SPEC: if there is no search tool or the search finds nothing, the limits are reported as unverified and SPEC values are used.

### Added
- `evals/results-2026-11-26.md` with every output and its grade, and `evals/fixtures/` with the test images and the HTML they were rendered from. The eval 8 portrait is a public-domain image from Wikimedia Commons.
- The release ZIP leaves out `evals/fixtures/` to keep the installed skill small.

## [1.0.0] - 2026-11-26

First public release.

### Added
- Five routes from one skill: REPLICATE (image to full prompt), HARVEST (lift named traits such as palette or typography), REPAIR (rank what drifted between a source and its regeneration, then write one edit prompt), CREATE (prompt from an idea), and multi-image role assignment.
- Fixed output shape: SETTINGS, a ranked SIGNATURE of the 3-5 traits that make the image itself, the prompt, an optional reference line, and at most four NOTES.
- "What carries the image" checklists per image type (photo, person, product, illustration, poster and type, infographic and UI, collage).
- Twelve liftable prompt sections, from FRAME to EXCLUDE.
- A dated SPEC block for GPT-Image-2.6 Sunburst and Flare: quality, complexity, size rules and background, checked against OpenAI's image generation docs on 2026-11-26.
- Honesty rules: never guess what is not visible, keep unreadable text out of the prompt, reproduce defects unless told "clean", never claim a prompt was tested without seeing the result.
- Boundaries for real people, documents, signatures and watermarks, and copyrighted characters.
- `evals/prompts.md` with ten behaviour checks, `agents/openai.yaml` for Codex and ChatGPT, MIT license.

### History before release
- 2026-09-26: started as a GPT Image 2.5 image-to-prompt system prompt.
- 2026-11-09: rebuilt as an agent skill for GPT-Image-2.6, with HARVEST and REPAIR added.
