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

## Main studio layout

### Project rail

Brand / project navigation on the left. Keep it quiet and compact.

### Canvas

The center is the hero: handwriting samples, glyph specimen, or the selected glyph editor.

### Inspector

Contextual controls on the right: geometry, spacing, baseline, weight, variants, and AI assistance.

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

The inspiration target is the feeling of handwriting interactions on modern touch interfaces: immediate, fluid, and quiet rather than a flashy animation layered on top.

## Progressive effort

Do not make users fill an alphabet sheet before seeing value.

- **Instant:** use any decent sample and get a first draft.
- **Refine:** ask only for ambiguous or missing glyphs.
- **Studio:** allow complete manual control for users who want perfection.

## UX voice

Confident, warm, slightly playful, never childish. Mina can add personality around the edges, but the product itself should remain clear and premium.

## Design rule

> Make the magic obvious, then get out of the user's way.
