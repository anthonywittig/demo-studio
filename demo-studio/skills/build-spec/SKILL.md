---
name: build-spec
description: >-
  Use when someone wants a build spec, wants a customer demo specified so a
  coding agent can build it end to end, or asks what to hand an engineer to make
  the demo real.
---

# Build Spec

Read `references/build-spec.md`, then fill `assets/build_spec_template.md`.
Non-negotiables: name the skills/refs to read with "reference wins", a preflight
that installs prereqs, a definition-of-done gate whose tests loop until green,
mock-by-default, generic/public-safe, pinned pre-release versions.

## Quickstart (hand to a coding agent)

Run it from the working directory where the output belongs, not from inside
the skill. Set `SKILL` to this skill's base directory (the absolute path shown
when the skill loaded) and keep it quoted: some hosts install plugin skills as
directories named like `demo-studio:build-spec`, and the colon is harmless in a
quoted absolute path, so there is no need to copy the skill anywhere.

```bash
SKILL="/absolute/path/to/this/skill"   # its base directory, quoted
cp "$SKILL/assets/build_spec_template.md" BUILD_SPEC.md
# fill it in (see references/build-spec.md)
```

Apply the disciplines in `shared/grounding.md`.
