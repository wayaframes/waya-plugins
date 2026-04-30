# Personal Ikigai — Visualization Specification

This document specifies how to render the Ikigai diagram. The skill produces a **single live artifact** that the user watches fill in stage by stage — not a one-shot end-of-session summary.

`SKILL.md` references this document at every Stage 2 and Stage 3 confirmation, and at Stage 4 for the center reveal.

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
| Love | `#c25450` |
| Good At | `#4a7fb8` |
| Paid For | `#c9a23a` |
| World Needs | `#5a9d6e` |

Center circle: `#ffffff` fill with thin neutral-grey border `#888` once revealed.

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

## Polish requirements

- **No raw CSS visible to the user.** The `<style>` block must be a real `<style>` element, not stripped or HTML-escaped. Verify every render.
- **Color encoding consistency.** Same hex applied to the circle border, the legend swatch, the section header, and any accent text. Don't drift.
- **Empty-state legibility.** Dashed-circle placeholders must remain visible against the canvas background.
- **One source of truth for items.** Items live inside their circles. Do **not** also render a parallel markdown list of items below the diagram — that doubles cognitive load.
- **No double-render.** On surfaces that support in-place update, never emit a second copy of the artifact.

---

## Acceptance criteria

The visualization is correct when:

1. The artifact appears after **Stage 2A confirmation** (not at Stage 5).
2. Each subsequent stage confirmation updates the same artifact in place (or re-renders cleanly on surfaces without update-in-place).
3. Every user-generated item is anchored visually inside or to its circle's crescent — not in a separate list.
4. The diagram renders without text overflow at 480px width.
5. The center Ikigai statement, once revealed, is the visual focal point (callout below the diagram, plus center anchor).
6. No raw CSS, unescaped HTML, or dangling markup is visible to the user at any stage.
