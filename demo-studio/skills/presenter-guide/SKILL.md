---
name: presenter-guide
description: >-
  Use when someone wants a presenter guide, speaker notes, a teleprompter script,
  per-slide talking points or questions to ask and expect back, a run of show, or
  wants a demo runbook turned into a live walkthrough for delivering a deck.
---

# Presenter Guide

Write this against the FINAL aggregate deck, not a draft: slide numbers, order,
and content need to be locked first, or the guide is presenting a deck that
does not exist yet. Read `references/presenter-guide-format.md`. Per slide:
Talking points, Say (teleprompter, one beat per line), and Ask. Fold a demo
RUNBOOK into the optional `demo` block: cold start, the two lanes, a card per
beat with the exact Ctrl-C, plus reference/switches.

## Quickstart (per-slide points / teleprompter Say / questions + demo run-of-show)

Run it from the working directory where the output belongs, not from inside
the skill. Set `SKILL` to this skill's base directory (the absolute path shown
when the skill loaded) and keep it quoted: some hosts install plugin skills as
directories named like `demo-studio:presenter-guide`, and the colon is harmless in a
quoted absolute path, so there is no need to copy the skill anywhere.

```bash
SKILL="/absolute/path/to/this/skill"   # its base directory, quoted
cp "$SKILL/assets/examples/presenter_guide.example.json" my_pg.json
# edit my_pg.json: slides[] and the optional demo{} block (see references/presenter-guide-format.md)
python3 "$SKILL/assets/build_presenter_guide.py" my_pg.json presenter-guide.html
```

Apply the disciplines in `shared/grounding.md`.
