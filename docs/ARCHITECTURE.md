# Spell Out! — Architecture Notes

## Guiding principle

Keep AI interpretation separate from editable typography data and deterministic font generation.

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

### Server/runtime

- Gemini requests.
- Secrets/API credentials.
- Potentially expensive image processing.
- Font generation if browser execution becomes impractical.

### Storage

Start with local/project state where possible during prototyping. Introduce persistent cloud storage only when the product needs accounts, sharing, or cross-device projects.

## Google AI Studio strategy

Use Google AI Studio Build to establish the first full-stack web application and iterate rapidly on the UI. Keep provider-specific calls behind a small application service boundary so the rest of the product is not tightly coupled to prompt implementation details.

## Future distribution

After the font itself is reliable, investigate platform-specific ways to make handwriting usable outside applications that support custom fonts. These are separate adapters, not part of the core glyph pipeline.
