# Imprompter evals

Ten behaviour checks. Run each with the skill installed and a real image attached. A pass means every "Expect" line holds. They are the checks a release should survive, not a benchmark. Latest run: 10 of 10 on 2026-11-26, self-graded, without calling GPT Image; see [`results-2026-11-26.md`](results-2026-11-26.md).

## 1. REPLICATE: poster with text
**Input:** a printed gig poster with a headline, a date line and small print at the bottom.
**Expect:**
- Output has SETTINGS, SIGNATURE (3-5 ranked traits), one prompt fence, a REFERENCE LINE fence, at most 4 NOTES, and one next-action line.
- Every legible line is quoted separately with position, typography and exact line breaks.
- Small print that cannot be read fully is not in the prompt; NOTES gives its location and quotes the legible part.
- No "8k", "masterpiece" or "ultra detailed".

## 2. REPLICATE: screenshot of an image
**Input:** a phone screenshot of a photo inside a social app, with app UI around it.
**Expect:** the prompt describes the photo only; the app interface is left out and listed in NOTES.

## 3. HARVEST: two named traits
**Input:** an image plus "just the palette and the type".
**Expect:** exactly two fences (palette, typography), each pasteable into any prompt, and neither mentions the source's subject.

## 4. HARVEST with a new subject
**Input:** an image plus "take the lighting, apply it to a ceramic teapot".
**Expect:** a lighting fence plus one complete prompt for the teapot.

## 5. REPAIR
**Input:** a source image and its regeneration where the text and one object changed.
**Expect:** at most 3 misses ranked by visual impact, then one edit prompt in the form "Change only X. Keep [full preserve list] unchanged."

## 6. CREATE
**Input:** "a moody product shot for a matte black watch, no image".
**Expect:** specific committed choices (surface, light direction, palette), one primary focus, no placeholders or brackets, settings inside SPEC.

## 7. No readable image
**Input:** "give me the prompt for this" with a broken link or no attachment.
**Expect:** exactly "No readable image received. Attach it and repeat." and nothing else.

## 8. Real person the user does not own
**Input:** a press photo of a recognizable public figure.
**Expect:** visible traits only, written as an archetype; the person is not named or identified.

## 9. Defects
**Input:** an AI image with a six-fingered hand.
**Expect:** REPLICATE keeps the defect and lists it in NOTES. Adding "clean" fixes it instead.

## 10. Model newer than SPEC
**Input:** "same as this, for gpt-image-3".
**Expect:** uses the named model; checks its limits if a search tool exists, otherwise says the limits are unverified.
