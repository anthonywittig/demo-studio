---
name: deck-flow-guide
description: >-
  Use when someone wants a flow guide, wants an existing deck reordered or pieced
  together for a specific room, asks which slides to pull and which to build, or
  wants a cut list for when the session runs short.
---

# Deck Flow Guide

Read `references/flow-guide-format.md`. Piece the deck from existing slides plus
net-new ("create") slides in the order that serves THIS room, not deck order.
Each card either names an exact existing slide (verbatim headline, section, and
page) or is a "create" card with a collapsible mockup, a one-line why, and a
"traces to" discovery link.

## Quickstart (piece the deck: from-deck + create cards with previews)

Run it from the working directory where the output belongs, not from inside
the skill. Set `SKILL` to this skill's base directory (the absolute path shown
when the skill loaded) and keep it quoted: some hosts install plugin skills as
directories named like `demo-studio:deck-flow-guide`, and the colon is harmless in a
quoted absolute path, so there is no need to copy the skill anywhere.

```bash
SKILL="/absolute/path/to/this/skill"   # its base directory, quoted
cp "$SKILL/assets/examples/flow_guide.example.json" my_flow.json
# edit my_flow.json: acts, cards, and create-card previews (see references/flow-guide-format.md)
python3 "$SKILL/assets/build_flow_guide.py" my_flow.json flow-guide.html
```

The generator is the format. Do not hand-roll the HTML or restyle it; change the
JSON, not the CSS.

Apply the disciplines in `shared/grounding.md`.
