---
name: create-slides
description: >-
  Use when someone wants net-new slides built, a dark PPTX that drops into an
  aggregate deck, slide mockups or diagrams for a demo deck, or wants the
  net-new slides it already built tweaked and re-rendered.
---

# Create Slides

Read `references/create-slides-pptx.md`, which documents locating the pptx
skill via `shared/pptx_tools.sh` (its path varies by machine, so probe for it,
do not hardcode it). Copy `assets/build_create_slides.js` out and edit it (one block
per slide), then ALWAYS run the render-and-inspect QA loop and view every
slide image before shipping. Google-Slides-safe: block arrows, solid borders,
no connectors or dashes; no em dashes; dark and readable.

## Quickstart (dark, Google-Slides-safe PPTX)

Run these from the working directory where the deck belongs, not from inside
the skill: the installed plugin may be read-only, and nothing here needs to be
written into it. Set `SKILL` to this skill's base directory (the absolute path
shown when the skill loaded) and keep it quoted. Some hosts install plugin
skills as directories named like `demo-studio:create-slides`; the colon is
harmless in a quoted absolute path, so there is no need to copy the skill
anywhere. `CREATE_SLIDES_ASSETS` tells your copy of the builder where the kit
lives, so the copy can sit beside the outputs.

```bash
SKILL="/absolute/path/to/this/skill"   # its base directory, quoted
SHARED="$SKILL/shared"; [ -d "$SHARED" ] || SHARED="$SKILL/../../shared"
export CREATE_SLIDES_ASSETS="$SKILL/assets"
[ -d node_modules/pptxgenjs ] || npm install --no-save pptxgenjs@^3.12.0   # once per working directory
cp "$SKILL/assets/build_create_slides.js" my_slides.js
# edit my_slides.js: one builder block per net-new slide (see references/create-slides-pptx.md)
. "$SHARED/pptx_tools.sh"
PPTX_SKILL="$(find_pptx_skill)" || exit 1
render_preflight || echo "proceeding without visual QA, deck is UNVERIFIED"

node my_slides.js
python3 "$SHARED/guardrails.py" create-slides.pptx
python3 "$PPTX_SKILL/scripts/office/validate.py" create-slides.pptx
python3 "$PPTX_SKILL/scripts/office/soffice.py" --headless --convert-to pdf create-slides.pptx
pdftoppm -jpeg -r 150 create-slides.pdf slide
# then VIEW every slide-N.jpg and fix
```

Apply the disciplines in `shared/grounding.md`.
