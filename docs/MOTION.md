# Spell Out! — Motion & Morph System

## Purpose

The processing animation is a product feature. It turns unavoidable computation time into a reason to stay and watch.

The visual system should feel like one living substance capable of becoming typography, symbols, creatures, particles, pixels, or 3D objects.

The system must be designed so new morphs can be added later without rewriting the renderer or the application pipeline.

## Core model

Every animated thing is described by four independent concepts:

```text
FORM       = what it is
BEHAVIOR   = how it moves
MATERIAL   = how it looks
SEQUENCE   = what happens next
```

Examples:

```text
FORM: blob
BEHAVIOR: fall + walk + hook + puddle + reform
MATERIAL: glossy pink gel
SEQUENCE: blob_adventure
```

```text
FORM: spellout
BEHAVIOR: pulse + dissolve + explode + assemble
MATERIAL: white gel → pixel → low-poly
SEQUENCE: arcade
```

No form should permanently own a behavior. Shared behaviors are what make the system extensible.

## Form registry

Initial candidates:

- `spellout`
- `heart`
- `blob`
- `pixel_logo`
- `konami_code`
- `low_poly_logo`
- `ink_mass`

Future forms can include objects, icons, glyphs, characters, or entirely new shapes.

## Behavior registry

Initial candidates:

- `idle`
- `pulse`
- `stretch`
- `morph`
- `fall`
- `walk`
- `run`
- `bounce`
- `edge_bounce`
- `orbit`
- `explode`
- `scatter`
- `seek`
- `assemble`
- `split`
- `merge`
- `dissolve`
- `puddle`
- `hook_arc`
- `return_to_center`

Behaviors should be composable rather than implemented as monolithic animations.

## Materials

Materials should be independent of geometry where practical.

Possible materials:

- clean white
- translucent gel
- liquid ink
- neon pink
- cyan
- arcade yellow
- pixel
- low-poly / N64-inspired
- chrome / glass

The same form should be able to change material during a morph.

## True morphing

The preferred transition is continuous geometry transformation.

Possible implementations:

- shared-topology morph targets
- SVG path interpolation
- vertex interpolation
- shader displacement
- point-cloud transitions
- particle-based reconstruction

Blender is appropriate for authoring complex 3D geometry and morph targets. Runtime assets should be exported in a web-friendly format and driven by the browser scene runtime.

## Compound transformations

The system must support one object becoming multiple objects and multiple objects becoming one.

### Split

```text
ONE
 ↓
PART A   PART B   PART C   PART D
```

### Seek / assemble

```text
PART A ↘
PART B → CENTER → COMPLETE FORM
PART C ↗
PART D →
```

### Re-entry

An animated object is not required to stay inside the central hero bounds. It may travel toward a footer, side rail, or viewport edge and later return to the hero.

The scene therefore needs a stable **world/viewport coordinate system** and named anchors such as:

- `heroCenter`
- `heroLeft`
- `heroRight`
- `footer`
- `viewportEdge`
- `customAnchor`

## Sequence graph

Sequences should be represented as graphs or composable timelines rather than one giant imperative animation function.

Conceptual example:

```text
             ┌→ WALK → HOOK → PUDDLE ─┐
SPELL OUT → BLOB                    → REFORM → SPELL OUT
             └→ FALL ──────────────────┘
```

Another:

```text
SPELL OUT
   ↓
EXPLODE
   ↓
A B C D
 ↙ ↓ ↓ ↘
SEEK CENTER
   ↓
ASSEMBLE
   ↓
BOUNCE × 3
   ↓
RETURN CENTER
   ↓
NEXT MORPH
```

This graph model leaves room for branching, random selection, conditional sequences, and future interactive triggers.

## Synchronization with real processing

The animation director listens to semantic application events rather than inventing fake backend progress.

Example:

```text
image_received
    → intro sequence
handwriting_detected
    → letter morphs
characters_extracted
    → glyph sequence
font_build_started
    → longer spectacle
font_ready
    → resolution / settle
```

If processing finishes early, the director can resolve the current sequence gracefully. If processing takes longer, it can enter another compatible loop.

## Loop library

The system should contain short loops that can safely repeat without feeling identical.

A loop should have:

- intro state
- cycle state
- exit state
- compatible next states
- approximate duration
- reduced-motion alternative

This allows the visual experience to fill unpredictable processing time without showing a fake percentage.

## Randomness

Randomness should be constrained and authored.

Use a sequence pool with compatibility rules instead of choosing arbitrary animations. The same session should feel coherent and intentional.

Potential future weighting:

```text
magic:   30%
arcade:  30%
liquid:  25%
weird:   15%
```

These values are examples, not product requirements.

## Editing transition

Processing should resolve into a calm editing state.

```text
SPECTACLE
   ↓
SETTLE
   ↓
WHITE SPACE
   ↓
GLYPH EDITOR
```

The visual system should expose a clean handoff event such as `MORPH_COMPLETE` so the application can transition UI state independently.

## Technical boundary

The motion system should expose a small API to the application:

```text
play(sequence)
queue(sequence)
setForm(form)
morphTo(form, options)
spawn(form, options)
setAnchor(anchor)
pause()
resume()
settle()
```

The exact implementation can evolve. React components should not manipulate Three.js objects directly.

## Quality bar

A new animation is worth adding only if it satisfies at least one of these:

- Creates a genuine visual surprise.
- Demonstrates a new transformation technique.
- Reinforces Spell Out!'s identity.
- Makes processing time more enjoyable.
- Can be reused as a behavior or form in future sequences.

Avoid accumulating isolated one-off animations. Build a reusable vocabulary first.
