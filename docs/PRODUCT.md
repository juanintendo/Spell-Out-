# Spell Out! — Product Definition

> Turn handwriting into a typeface you can actually use.

## Product thesis

Spell Out! turns a user's existing handwriting samples into an editable digital typeface. AI creates the first interpretation; the user remains the authority over the final letterforms.

The product should feel less like an AI generator and more like a small, beautiful type studio.

## Core promise

**Show us how you write. We'll turn it into a font.**

A user should be able to:

1. Upload a reasonably good photo or scan of handwritten text.
2. Let Spell Out! detect and interpret available characters.
3. Review the first-pass alphabet.
4. Select any glyph that needs correction.
5. Refine it with mouse, touch, or stylus/Apple Pencil.
6. Preview the resulting typeface in real text.
7. Export a usable font file.

## Input modes

### Instant

One decent handwriting photo. Spell Out! extracts whatever it can and produces a first draft without demanding a complete alphabet sheet.

### Refine

If specific glyphs are uncertain or missing, Spell Out! asks only for the additional characters it needs.

### Studio

Advanced users can deliberately provide uppercase, lowercase, numbers, punctuation, and additional samples for greater control and coverage.

## Human-in-the-loop principle

**AI gets you 80% there. You make the last 20% yours.**

AI is responsible for interpretation and assistance. It is not the final authority over glyph geometry.

Every generated glyph must have an editable representation so the user can correct, reshape, or redraw it.

## MVP

The first product milestone is intentionally narrow:

**Photo → interpreted glyphs → editable glyph → preview → TTF/OTF export.**

Do not make WhatsApp, Telegram, custom keyboards, accounts, collaboration, or a large font marketplace prerequisites for the MVP.

## Later distribution layer

Once the core font workflow is excellent, Spell Out! can explore ways to use the handwriting in places that do not support arbitrary fonts, including keyboard, sticker, image, and platform-specific workflows.

The product should promise **"Use your handwriting anywhere"** only when the underlying platform integration can genuinely support that experience.

## Non-goals for the first build

- Building a complete professional font editor.
- Supporting every Unicode character.
- Solving every mobile messaging platform.
- Training a custom handwriting foundation model.
- Replacing professional type-design software.

## Product quality bar

The first successful experience should make a user think:

> **"Holy shit, that's actually my handwriting."**

Not merely:

> "The AI generated a font."

The emotional fidelity of the result matters as much as technical correctness.
