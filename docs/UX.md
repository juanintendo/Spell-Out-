# Spell Out! — UX Direction

## Experience model

Spell Out! is a type studio, not a conventional dashboard. The interface should make the transformation from physical handwriting to digital type feel tangible, precise, and a little magical.

## Core flow

```text
UPLOAD
  ↓
UNDERSTAND
  ↓
FIRST DRAFT
  ↓
REVIEW
  ↓
TUNE
  ↓
PREVIEW
  ↓
EXPORT
```

## Visual direction

- Editorial, tactile, playful, and highly polished.
- Generous whitespace and strong typography.
- Subtle grids and typographic guides instead of heavy UI chrome.
- Motion should communicate physicality: ink, paper, tracing, shaping, and refinement.
- Avoid generic AI-dashboard aesthetics.
- Controls should feel like instruments in a type studio.

## Processing vs. editing

These are intentionally different experiences.

### PROCESSING

The interface becomes a small visual spectacle. A fluid hero object can morph continuously between typography, abstract forms, symbols, pixels, and 3D forms while the actual handwriting pipeline runs.

The goal is not to make the user stare at a progress bar. The goal is to make waiting feel like part of the product.

The animation should create curiosity: **“What is it going to become next?”**

### EDITING

The spectacle stops. The UI becomes calm, white, precise, and professional.

Editing trails are restrained and functional. Pointer/stylus feedback should feel like a premium drawing instrument rather than a decorative effect.

The contrast is intentional:

> Magic while the machine works. Precision when the human takes over.

## Main studio layout

### Project rail

Brand / project navigation on the left. Keep it quiet and compact.

### Canvas

The center is the hero: handwriting samples, glyph specimen, or the selected glyph editor.

### Inspector

Contextual controls on the right: geometry, spacing, baseline, weight, variants, and AI assistance.

## Processing visual language

The visual reference is gooey, fluid cursor interaction: clean UI surrounded by responsive liquid matter.

The hero object should feel alive rather than like a conventional loader.

Possible visual vocabulary:

- Liquid trails.
- Gel-like blobs.
- Morphing typography.
- Ink-like distortion.
- Pixel disintegration/reassembly.
- Low-poly / retro 3D moments.
- Particles that behave as physical pieces.
- Elastic motion and overshoot.
- Edge collisions and rebounds.
- Temporary forms that can leave the main hero area and return.

A sequence may become a miniature animation story. For example:

```text
SPELL OUT
  → liquid blob
  → falls toward footer
  → walks across the page
  → hooks into an arc
  → becomes a puddle
  → reforms
  → SPELL OUT
```

Another sequence could be:

```text
SPELL OUT
  → explodes into four pieces
  → pieces move independently
  → pieces seek each other
  → assemble
  → bounce against viewport edges
  → return to center
  → next transformation
```

These are examples of a reusable language, not fixed animation requirements.

## Morph principles

### Real transformation over cuts

Whenever possible, the viewer should perceive one continuous object becoming another.

Avoid:

```text
fade out → unrelated asset appears
```

Prefer:

```text
shape stretches → geometry changes → material changes → new form resolves
```

### Behavior is reusable

A blob should not be a special-case “blob animation.” It should be an object that can use shared behaviors such as fall, walk, bounce, split, merge, orbit, dissolve, or seek.

This lets future forms and characters participate in the same visual language.

### Surprise with restraint

The animation should be memorable without becoming noisy. Long sequences need moments of stillness. The UI surrounding the hero remains quiet so the moving object has visual authority.

## Glyph editing

Selecting a glyph opens a focused editing state.

The editor should support:

- Bézier handles and editable vector points.
- Move, reshape, smooth, add, and remove points.
- Baseline and x-height guides.
- Horizontal and vertical metrics.
- Direct redraw/tracing.
- Mouse click-and-drag.
- Touch/finger input.
- Stylus and Apple Pencil input where supported.
- Original handwriting ghost/reference layer.
- Undo/redo.

## Original → generated → edited

When refining a glyph, the UI should make the relationship visible:

**Original ink → AI interpretation → Your edit**

A comparison slider or ghost overlay can communicate this without forcing the user into a separate screen.

## Motion principles

Motion should feel responsive rather than decorative.

Important interactions:

- Upload recognition.
- Character detection.
- Glyph construction.
- Selecting a glyph.
- Entering edit mode.
- Drawing and dragging points.
- Saving a correction.
- Generating a preview.
- Export completion.

For direct drawing, the stroke should feel physically connected to the input. The interface should react to pressure/velocity information when available, while degrading gracefully for mouse and touch.

The processing hero uses a different motion language: fluid, elastic, cinematic, and surprising. The editor uses precise, immediate, low-amplitude feedback.

## Progressive effort

Do not make users fill an alphabet sheet before seeing value.

- **Instant:** use any decent sample and get a first draft.
- **Refine:** ask only for ambiguous or missing glyphs.
- **Studio:** allow complete manual control for users who want perfection.

## UX voice

Confident, warm, slightly playful, never childish. Mina can add personality around the edges, but the product itself should remain clear and premium.

## Design rule

> Make the magic obvious, then get out of the user's way.
