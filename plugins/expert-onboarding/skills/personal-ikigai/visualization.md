# Personal Ikigai — Visualization Specification

This document specifies how to render the Ikigai diagram. The skill produces a **single live artifact** that the user watches fill in stage by stage — not a one-shot end-of-session summary.

`SKILL.md` references this document at every Stage 2 and Stage 3 confirmation, and at Stage 4 for the center reveal.

---

## Rendering Rules (Hard Requirements)

These are correctness rules, not polish. Every rendered output must satisfy all of them.

### 1. Items live inside their circles, not in a list below

User-generated items render as `<text>` / `<tspan>` elements positioned at each circle's outer-crescent anchor (see § Layout). Do **not** also emit a parallel `<ul>`, `<div>`, or markdown list of items below or beside the diagram. Items appear in exactly one place: inside the circles. A list below the diagram defeats the purpose of the visualization.

### 2. Use the exact hex colors

Use these hex values exactly — for circle borders, legend swatches, section headers, and any accent text. Do not substitute generic pinks, blues, greens, or yellows.

- Love: `#902913`
- Good At: `#759C8B`
- Paid For: `#F3B742`
- World Needs: `#C37028`

### 3. Pass HTML / SVG content directly — no escape wrappers

When rendering through any visualization tool that accepts HTML or SVG strings (Cowork's `show_widget`, similar host tools), pass the content directly: `<style>...</style><div>...<svg>...</svg></div>` as a literal string. Do **not** wrap in `CDATA`, template literals, JSON-encoded strings, HTML-entity escapes, or any other transport-layer wrapper. Most renderers expect raw HTML and will display escape syntax as visible garbage if it leaks through.

### 4. The `<style>` block is a real `<style>` element

Not stripped, escaped, or rendered as visible text. If CSS source appears as text in the output, that's a render bug — fix the transport, do not work around it.

### 5. Single artifact, no double-render

On surfaces that support in-place artifact updates, emit the artifact once at Stage 2A and update in place at each subsequent stage. Never emit a fresh second copy alongside an existing one.

---

## Surface detection

Pick the best rendering path based on what the host supports:

1. **Persistent inline artifact (preferred)** — if the surface supports JSX / HTML / SVG rendering with update-in-place (e.g. Cowork side panel), render ONE artifact at Stage 2A confirmation and update it incrementally through Stage 4. The user watches the same canvas fill in.
2. **Re-render fallback** — if the surface supports inline rendering but cannot update artifacts in place, re-render the full diagram at each confirmation. Acceptable but less elegant.
3. **Markdown only** — if the surface does not support inline rendering at all, skip the visual entirely, deliver a clean markdown summary at Stage 5, and offer Word export.

After the inline visual lands, always offer a follow-up persistent copy in a `~~design tool` (Figma, Canva, Miro) — see `SKILL.md` § Stage 5.

---

## Layout

Single canvas, four overlapping circles in the canonical Ikigai pattern, plus a small center circle for the final synthesis.

### Geometry (canonical 1100 × 900 viewBox)

| Circle | Center (cx, cy) | Radius |
| --- | --- | --- |
| Love (top) | 550, 290 | 260 |
| Good At (right) | 770, 470 | 260 |
| Paid For (bottom) | 550, 650 | 260 |
| World Needs (left) | 330, 470 | 260 |

**Center Ikigai region:** a small white-fill circle at (550, 470) with r ≈ 75, placed on top of all four overlaps. Empty until Stage 4 confirmation.

### Text anchors — items inside each circle's outer crescent

Each circle's items render in its **outer crescent** — the part of the circle not overlapped by any other.

| Circle | Anchor (x, y) | text-anchor | Stack |
| --- | --- | --- | --- |
| Love | 550, 130 | middle | downward |
| Good At | 920, 470 | end | downward |
| Paid For | 550, 800 | middle | upward |
| World Needs | 180, 470 | start | downward |

### Text anchors — pairwise intersection labels in the lens overlaps

| Intersection | Anchor (x, y) |
| --- | --- |
| Passion (Love ∩ Good At) | 680, 360 |
| Profession (Good At ∩ Paid For) | 680, 580 |
| Vocation (Paid For ∩ World Needs) | 420, 580 |
| Mission (World Needs ∩ Love) | 420, 360 |

Each intersection label has the synthesis statement directly underneath it (small text, max ~28 chars per line, 2 lines max).

### Center Ikigai

Anchored at (550, 470), inside the central white circle. Plus a callout block underneath the entire diagram showing the full Ikigai statement at larger type — the diagram center is the visual anchor, the callout is where the user actually reads it.

---

## Colors

Use these exact hex values everywhere — circle border, legend swatch, section header, accent text:

| Section | Hex |
| --- | --- |
| Love | `#902913` |
| Good At | `#759C8B` |
| Paid For | `#F3B742` |
| World Needs | `#C37028` |

Center circle: `#F1EFDD` (Beige) fill with `#39403A` (Charcoal) border once revealed.

---

## States

### Empty / placeholder — before the section is confirmed

- Circle border: `stroke-dasharray: 8 6` (dashed)
- Inside the crescent: a single `—` dash placeholder
- Color stays the section's hex but at ~40% opacity (desaturated)

### Filled — after section is confirmed

- Circle border: solid stroke (~3px)
- Items rendered inside the crescent at their anchor
- Color at full opacity

### Center reveal animation (Stage 4 confirmation)

When the center Ikigai statement appears, fade in the center white circle, the inner statement, and the callout block underneath the diagram together with a 400ms ease-in transition. This is the visual reward for completing the exercise — make it feel like an arrival.

---

## Text fitting

- Items wrap to a max of 2 lines, ~28 characters per line
- Use `<tspan>` with `dy` offsets for line breaks
- If a circle has more items than fit, show the top N and append "+N more" — and flag in the conversation that this is a signal the user's items are too long. The skill enforces 5–15 word items, so this should rarely happen

---

## Update sequence

The skill confirms sections in a fixed order. After each confirmation, update the artifact in place:

| Stage | Update applied to artifact |
| --- | --- |
| 2A confirmation | First render. Initialize the canvas, populate **Love** circle. Other three circles dashed/empty. |
| 2B confirmation | Populate **Good At** circle (solid stroke, items in crescent) |
| 2C confirmation | Populate **Paid For** circle |
| 2D confirmation | Populate **World Needs** circle |
| 3A confirmation | Reveal **Passion** label + synthesis in its lens |
| 3B confirmation | Reveal **Profession** label + synthesis |
| 3C confirmation | Reveal **Mission** label + synthesis |
| 3D confirmation | Reveal **Vocation** label + synthesis |
| 4 confirmation | Fade in center circle, the inner Ikigai statement, and the callout block (400ms) |

**Do not re-emit a fresh artifact at each step** on surfaces that support in-place update. The point is the user sees one canvas fill in.

---

## Responsive layout

The diagram is **side-panel-first** — readable at ~480px width — and adapts upward.

### Narrow (≤ 600px width)

- Vertical stack: legend → diagram → center Ikigai callout (when revealed)
- Smaller fonts (~12–14px after viewBox scaling)
- SVG uses `viewBox="0 0 1100 900"` and `preserveAspectRatio="xMidYMid meet"` so it scales without distortion
- Container `max-width: 100%` and percentage widths only — no fixed pixel widths on outer containers

### Wider (> 600px)

- Diagram takes ~60% width; legend / center callout sits beside it
- Larger fonts proportional to viewBox

### Center Ikigai placement (post-Stage-4)

The Ikigai statement appears **both** inside the central white circle (small) **and** in a callout block below the diagram (full statement, larger type). The callout is the focal point.

---

## Legend

A small color-key legend renders above the diagram so the user can map color → circle name. Keep it compact:

```
● Love   ● Good At   ● Paid For   ● World Needs
```

Use the four hex colors as visual swatches.

---

## Polish (recommendations)

The Hard Requirements section above covers correctness. These are smaller polish items:

- **Empty-state legibility.** Dashed-circle placeholders must remain visible against the canvas background — light grey on white is too subtle. Use the section's hex at ~40% opacity for the dashed stroke so the circle is still locatable but reads as "not yet."
- **Center reveal feels like an arrival.** The 400ms ease-in is intentional — don't shorten it. The user just spent an hour on this; let the moment land.
- **Font choice.** System sans (`ui-sans-serif, system-ui, sans-serif`) is fine. Avoid display fonts that hurt readability at narrow widths.
- **Spacing between stacked items.** ~16px between item lines inside a circle. Too tight reads as a wall of text; too loose pushes items out of the crescent.

---

## Reference Template

Below is the canonical structure for the rendered artifact. **Adapt** by substituting the placeholder values (`{LOVE_ITEM_1}`, `{PASSION_SYNTHESIS}`, etc.) with the user's content. Keep the structure, geometry, and class names as-is.

```html
<style>
  .ikigai-canvas { font-family: 'Poppins', ui-sans-serif, system-ui, sans-serif; color: #39403A; background: #F1EFDD; max-width: 100%; padding: 16px; }
  .ikigai-svg { width: 100%; height: auto; display: block; }
  .circle-love     { fill: #902913; fill-opacity: 0.12; stroke: #902913; stroke-width: 3; }
  .circle-good-at  { fill: #759C8B; fill-opacity: 0.12; stroke: #759C8B; stroke-width: 3; }
  .circle-paid-for { fill: #F3B742; fill-opacity: 0.12; stroke: #F3B742; stroke-width: 3; }
  .circle-needs    { fill: #C37028; fill-opacity: 0.12; stroke: #C37028; stroke-width: 3; }
  .circle-empty    { fill: none !important; stroke-dasharray: 8 6; opacity: 0.4; }
  .item-text       { font-size: 14px; fill: #39403A; }
  .label-text      { font-size: 16px; font-weight: 600; }
  .lens-label      { font-size: 14px; font-weight: 600; fill: #555; }
  .lens-synthesis  { font-size: 12px; fill: #555; }
  .center-circle   { fill: #F1EFDD; stroke: #39403A; stroke-width: 1.5; opacity: 0; transition: opacity 400ms ease-in; }
  .center-circle.revealed { opacity: 1; }
  .center-text     { font-size: 13px; fill: #39403A; font-weight: 700; opacity: 0; transition: opacity 400ms ease-in; text-transform: uppercase; letter-spacing: 1px; }
  .center-text.revealed { opacity: 1; }
  .ikigai-callout  { margin-top: 16px; padding: 16px; border-left: 4px solid #39403A; font-size: 18px; line-height: 1.4; opacity: 0; transition: opacity 400ms ease-in; color: #39403A; }
  .ikigai-callout.revealed { opacity: 1; }
  .legend          { display: flex; gap: 16px; font-size: 13px; margin-bottom: 12px; flex-wrap: wrap; }
  .legend-swatch   { display: inline-block; width: 12px; height: 12px; border-radius: 50%; vertical-align: middle; margin-right: 4px; }
</style>

<div class="ikigai-canvas">
  <div class="legend">
    <span><span class="legend-swatch" style="background:#902913"></span>Love</span>
    <span><span class="legend-swatch" style="background:#759C8B"></span>Good At</span>
    <span><span class="legend-swatch" style="background:#F3B742"></span>Paid For</span>
    <span><span class="legend-swatch" style="background:#C37028"></span>World Needs</span>
  </div>

  <svg class="ikigai-svg" viewBox="0 0 1100 900" preserveAspectRatio="xMidYMid meet">
    <!-- CIRCLES — add class="circle-empty" for any section not yet confirmed -->
    <circle cx="550" cy="290" r="260" class="circle-love" />
    <circle cx="770" cy="470" r="260" class="circle-good-at" />
    <circle cx="550" cy="650" r="260" class="circle-paid-for circle-empty" />
    <circle cx="330" cy="470" r="260" class="circle-needs circle-empty" />

    <!-- SECTION LABELS — outside the diagram, color-coded -->
    <text x="550" y="40"  text-anchor="middle" class="label-text" fill="#902913">WHAT YOU LOVE</text>
    <text x="1080" y="470" text-anchor="end"   class="label-text" fill="#759C8B">WHAT YOU'RE GOOD AT</text>
    <text x="550" y="880" text-anchor="middle" class="label-text" fill="#F3B742">WHAT YOU CAN BE PAID FOR</text>
    <text x="20"  y="470" text-anchor="start"  class="label-text" fill="#C37028">WHAT THE WORLD NEEDS</text>

    <!-- ITEMS INSIDE CIRCLES — repeat <text> per item, stack vertically in the crescent.
         Wrap long items with <tspan dy="16">. Max 28 chars per line, 2 lines. -->
    <!-- Love crescent (anchor 550,130, text-anchor=middle, stack downward) -->
    <text x="550" y="130" text-anchor="middle" class="item-text">{LOVE_ITEM_1}</text>
    <text x="550" y="150" text-anchor="middle" class="item-text">{LOVE_ITEM_2}</text>
    <text x="550" y="170" text-anchor="middle" class="item-text">{LOVE_ITEM_3}</text>

    <!-- Good At crescent (anchor 920,470, text-anchor=end, stack downward) -->
    <text x="920" y="450" text-anchor="end" class="item-text">{GOOD_AT_ITEM_1}</text>
    <text x="920" y="470" text-anchor="end" class="item-text">{GOOD_AT_ITEM_2}</text>
    <text x="920" y="490" text-anchor="end" class="item-text">{GOOD_AT_ITEM_3}</text>

    <!-- Paid For crescent (anchor 550,800, text-anchor=middle, stack upward) -->
    <text x="550" y="780" text-anchor="middle" class="item-text">{PAID_FOR_ITEM_1}</text>
    <text x="550" y="800" text-anchor="middle" class="item-text">{PAID_FOR_ITEM_2}</text>
    <text x="550" y="820" text-anchor="middle" class="item-text">{PAID_FOR_ITEM_3}</text>

    <!-- World Needs crescent (anchor 180,470, text-anchor=start, stack downward) -->
    <text x="180" y="450" text-anchor="start" class="item-text">{NEEDS_ITEM_1}</text>
    <text x="180" y="470" text-anchor="start" class="item-text">{NEEDS_ITEM_2}</text>
    <text x="180" y="490" text-anchor="start" class="item-text">{NEEDS_ITEM_3}</text>

    <!-- INTERSECTION LABELS — in the lens overlap regions, with synthesis below -->
    <text x="680" y="355" text-anchor="middle" class="lens-label">PASSION</text>
    <text x="680" y="372" text-anchor="middle" class="lens-synthesis">{PASSION_SYNTHESIS}</text>

    <text x="680" y="575" text-anchor="middle" class="lens-label">PROFESSION</text>
    <text x="680" y="592" text-anchor="middle" class="lens-synthesis">{PROFESSION_SYNTHESIS}</text>

    <text x="420" y="355" text-anchor="middle" class="lens-label">MISSION</text>
    <text x="420" y="372" text-anchor="middle" class="lens-synthesis">{MISSION_SYNTHESIS}</text>

    <text x="420" y="575" text-anchor="middle" class="lens-label">VOCATION</text>
    <text x="420" y="592" text-anchor="middle" class="lens-synthesis">{VOCATION_SYNTHESIS}</text>

    <!-- CENTER IKIGAI — add 'revealed' class to circle and text on Stage 4 confirmation -->
    <circle cx="550" cy="470" r="75" class="center-circle" />
    <text x="550" y="475" text-anchor="middle" class="center-text">IKIGAI</text>
  </svg>

  <!-- CENTER CALLOUT — add 'revealed' class on Stage 4 confirmation -->
  <div class="ikigai-callout">
    <strong>Your Ikigai:</strong> {CENTER_IKIGAI_STATEMENT}
  </div>
</div>
```

### How to adapt the template

- **Empty state**: any circle whose section isn't yet confirmed gets `circle-empty` added to its class list. Remove the class once the section is confirmed.
- **Items**: emit one `<text>` element per item, vertically stacked in the crescent at the anchor for that circle. For items long enough to wrap, use `<tspan dy="16">` for the second line; keep a 2-line maximum.
- **Intersection synthesis**: shorten the user's confirmed synthesis statement to fit two lines max in the lens. If it can't, abbreviate — the full version lives in the textual recap at Stage 5.
- **Center reveal (Stage 4)**: add `revealed` class to `.center-circle`, `.center-text`, and `.ikigai-callout`. CSS handles the 400ms fade.
- **Forbidden**: do NOT also output a `<div>` or markdown list of items below this artifact. The SVG is the only place items render.

---

## Acceptance criteria

The visualization is correct when:

1. The artifact appears after **Stage 2A confirmation** (not at Stage 5).
2. Each subsequent stage confirmation updates the same artifact in place (or re-renders cleanly on surfaces without update-in-place).
3. Every user-generated item is anchored visually inside or to its circle's crescent — not in a separate list.
4. The diagram renders without text overflow at 480px width.
5. The center Ikigai statement, once revealed, is the visual focal point (callout below the diagram, plus center anchor).
6. No raw CSS, unescaped HTML, or dangling markup is visible to the user at any stage.
