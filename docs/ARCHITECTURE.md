# Spell Out! — Architecture Notes

## Guiding principle

Keep AI interpretation separate from editable typography data, deterministic font generation, and the visual presentation layer.

The product has two very different visual states:

- **PROCESSING:** expressive, fluid, surprising, cinematic.
- **EDITING:** precise, quiet, tactile, professional.

The processing animation must never become a hard-coded one-off. It is an extensible **Morph Director** system capable of introducing new forms, behaviors, and sequences without changing the core handwriting/font pipeline.

```text
Handwriting sample
       ↓
Image preprocessing
       ↓
Gemini multimodal interpretation
       ↓
Structured glyph candidates
       ↓
Editable glyph representation
       ↓
Human correction / drawing
       ↓
Typography metrics + kerning
       ↓
Font generation
       ↓
TTF / OTF export

                 PROCESSING VISUAL LAYER
                         ↑
                real pipeline state
                         ↓
                 Morph Director
                         ↓
          forms + behaviors + sequences
```

## AI layer

Google Gemini is used for multimodal understanding of handwriting samples and for assistance with ambiguous characters and style information.

AI output should be structured data, not opaque visual output that cannot be edited.

Potential glyph metadata:

- Unicode/codepoint.
- Bounding box.
- Confidence.
- Source region.
- Baseline relationship.
- x-height/cap-height relationship.
- Stroke/style observations.
- Candidate vector/path information where reliable.
- Missing/ambiguous status.

## Editable glyph model

The application owns the canonical editable representation of each glyph.

A glyph should be able to preserve:

- Vector paths.
- Source-image reference/crop.
- Metrics.
- Transform/normalization data.
- Edit history or version metadata.
- Optional alternate forms.

This keeps the editor independent from the model provider.

## Input handling

Samples may be photographs or scans. The pipeline should eventually handle:

- Perspective correction.
- Rotation/skew.
- Background cleanup.
- Ink/background separation.
- Line and character segmentation.
- Character-to-source mapping.

## Editor rendering

SVG or Canvas are appropriate for the interactive glyph editor. The rendering layer must support low-latency pointer events for mouse, touch, and stylus input.

The interaction model should expose the same editing primitives across input devices rather than building separate editors.

## Processing visual engine — Morph Director

The processing experience is a first-class product surface, not a decorative loading screen.

### Responsibilities

The Morph Director receives semantic application events such as:

```text
UPLOAD_RECEIVED
IMAGE_ANALYZING
HANDWRITING_FOUND
GLYPHS_EXTRACTING
FONT_BUILDING
COMPLETE
```

It converts those events into visual sequences without knowing how Gemini, image processing, or font generation work internally.

### Extensibility model

Forms, behaviors, materials, and sequences must be data/config driven wherever practical.

```text
Morph Director
├── Form Registry
│   ├── spellout
│   ├── heart
│   ├── blob
│   ├── pixel
│   ├── low_poly
│   └── future forms...
│
├── Behavior Registry
│   ├── liquid
│   ├── orbit
│   ├── fall
│   ├── walk
│   ├── bounce
│   ├── explode
│   ├── assemble
│   ├── dissolve
│   └── future behaviors...
│
├── Material / Style Registry
│   ├── clean
│   ├── gel
│   ├── ink
│   ├── pixel
│   ├── N64
│   └── future styles...
│
└── Sequence Registry
    ├── default
    ├── arcade
    ├── magic
    ├── playful
    └── future sequences...
```

A sequence should describe **what happens**, not contain application-specific logic.

Example concept:

```text
SPELL_OUT
  → LIQUID
  → HEART
  → PIXEL
  → SPELL_OUT
```

More advanced sequences can combine transformation and independent actors:

```text
SPELL_OUT
  → BLOB
  → FALL_TO_FOOTER
  → WALK_LEFT
  → WALK_RIGHT
  → HOOK_ARC
  → PUDDLE
  → REASSEMBLE
  → SPELL_OUT
```

Or a multi-piece sequence:

```text
SPELL_OUT
  → EXPLODE
  → PIECE_A / PIECE_B / PIECE_C / PIECE_D
  → SEEK_CENTER
  → ASSEMBLE
  → BOUNCE_OFF_EDGES
  → RETURN_CENTER
  → NEXT_MORPH
```

The important architectural rule is that **a form does not own its behavior**. A blob can fall, walk, bounce, split, merge, morph, or dissolve. A future form can reuse the same behaviors.

### Real morphs

Whenever feasible, transitions should be true continuous transformations rather than a hard cut between unrelated assets.

Preferred mechanisms include:

- Shared geometry / morph targets.
- Vertex interpolation.
- SVG path interpolation where appropriate.
- Shader-based displacement and distortion.
- Particle/point-cloud transitions for explosions and reassembly.
- Procedural material changes.

Blender may be used to author complex 3D source assets and morph targets. Runtime playback should remain web-native and controllable by the Morph Director rather than depending on pre-rendered video.

### Runtime rendering

The processing hero can use a dedicated WebGL/Three.js layer while the surrounding application remains normal React UI.

Keep the rendering engine isolated behind a small interface so the rest of the app does not depend directly on Three.js internals.

Conceptual boundary:

```text
React / App State
       ↓
Morph Director API
       ↓
Visual Scene Runtime
       ↓
WebGL / Three.js / shaders
```

This leaves room for future rendering techniques without rewriting application state or the product workflow.

### Performance and graceful degradation

The animation is important, but it must never block the actual font pipeline.

- Processing work and visual playback are independent.
- The visual sequence can continue, pause, shorten, or transition based on real pipeline state.
- Avoid faking percentage progress that does not correspond to actual work.
- Respect reduced-motion preferences.
- Provide a lightweight fallback for low-power devices.
- Do not make WebGL a prerequisite for editing or font export.

## Font generation

Font generation should be deterministic from the editable glyph model. The exported font must not depend on a live Gemini call.

The first target is a usable TTF/OTF containing a deliberately limited character set. Coverage can expand after the core workflow is validated.

## Application boundaries

### Frontend

- Studio UI.
- Upload/drop zone.
- Specimen and glyph grid.
- Interactive editor.
- Preview.
- Export UI.
- Processing visual shell.
- Morph Director client/state bridge.

### Server/runtime

- Gemini requests.
- Secrets/API credentials.
- Potentially expensive image processing.
- Font generation if browser execution becomes impractical.
- No dependency on the animation engine.

### Visual runtime

- WebGL/Three.js scene.
- Morph targets.
- Shader/material system.
- Particle/point systems.
- Animation sequencing.
- Input-independent playback.

### Asset authoring

Blender is an authoring tool, not the product runtime.

Possible asset pipeline:

```text
Blender
  ↓
validated topology / morph targets
  ↓
GLB / compatible asset data
  ↓
web visual runtime
```

## Google AI Studio strategy

Use Google AI Studio Build to establish the first full-stack web application and iterate rapidly on the UI. Keep provider-specific calls behind a small application service boundary so the rest of the product is not tightly coupled to prompt implementation details.

The same separation should apply to the visual system: AI/provider code must not know about animation implementation, and animation code must not know about Gemini prompt details.

## Future distribution

After the font itself is reliable, investigate platform-specific ways to make handwriting usable outside applications that support custom fonts. These are separate adapters, not part of the core glyph pipeline.
