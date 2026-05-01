# Pre-PMF Executive Summary — Progress Bar Visualization Specification

This document specifies how to render the progress bar artifact. The skill produces a **single live progress bar** that the user watches fill in section by section across the seven sections of the executive summary — not an end-of-session deliverable.

`SKILL.md` references this document at the first-question-answered moment, at every section transition, and at session completion.

---

## Rendering Rules (Hard Requirements)

These are correctness rules, not polish. Every rendered output must satisfy all of them.

### 1. Each section's fields live inside that section, not in a list below

When a section is `in_progress`, its field indicators (filled / unfilled circles + captured-data summaries) render inside the expanded section block. Do **not** also emit a parallel `<ul>`, `<div>`, or markdown list of section data below or beside the progress bar. Fields appear in exactly one place: inside the in-progress section.

### 2. Use the exact Waya brand hex colors

These are correctness, not aesthetics — the brand palette is a deliberate design choice for this artifact.

- Charcoal (not started): `#39403A`
- Muted Turquoise (completed): `#759C8B`
- Beige (completed background): `#F1EFDD`
- Burnt Orange (in-progress header): `#C37028`
- Field-label muted text: `rgba(57, 64, 58, 0.65)` (charcoal at 65% opacity)
- Yellow (progress bar fill): `#F3B742`

This is the canonical Waya brand palette, shared with `mission-values-guide` and `okr-workflow-pre-pmf`.

Do not substitute generic greys, greens, or yellows. These hexes must apply to backgrounds, borders, text accents, and progress fill consistently.

### 3. Pass HTML / SVG / JSX content directly — no escape wrappers

When rendering through any visualization tool that accepts HTML / JSX strings (Cowork's `show_widget`, similar host tools), pass the content directly: `<style>...</style><div>...</div>` as a literal string. Do **not** wrap in `CDATA`, template literals, JSON-encoded strings, HTML-entity escapes, or any other transport-layer wrapper. Most renderers expect raw HTML and will display escape syntax as visible garbage if it leaks through.

### 4. The `<style>` block is a real `<style>` element

Not stripped, escaped, or rendered as visible text. If CSS source appears as text in the output, that's a render bug — fix the transport, do not work around it.

### 5. Single artifact, no double-render

On surfaces that support in-place artifact updates, emit the artifact once after the first question is answered, then update in place at each subsequent section transition or data-capture moment. Never emit a fresh second copy alongside an existing one.

### 6. Only one section is `in_progress` at a time

Exactly one section has status `in_progress`. All others are either `complete` (collapsed, green) or `not_started` (collapsed, grey). The `in_progress` section must always match the section of the question currently being asked.

### 7. Completed sections are collapsed by default but click-to-expand

Once a section transitions from `in_progress` to `complete`, its fields collapse and only the section header (now green with `#F1EFDD` background) remains visible by default. **Completed sections must be click-to-expand**: clicking the section header reveals the captured fields in place; clicking again collapses. Use a native `<details>`/`<summary>` element with the default disclosure marker hidden and a CSS chevron that rotates on `[open]`. Captured field data must be persisted in the artifact for ALL completed sections (not only the in-progress one) so click-to-expand has data to reveal on demand.

Default visual state stays as specified — the user sees at most one previous (completed) section header, the full current section with fields, and one next (not started) section header. Expanding a completed section is a deliberate user action for review, not the default.

### 8. No emojis anywhere in the progress bar

Use color coding only. The brand palette carries the visual semantics — emoji checkmarks or other glyphs would conflict.

---

## Surface detection

Pick the best rendering path based on what the host supports:

1. **Persistent inline artifact (preferred)** — surface supports JSX / HTML rendering with update-in-place (Cowork side panel, etc.). Render once after the first question is answered; update in place at each section transition and each field-capture moment.
2. **Re-render fallback** — surface supports inline rendering but cannot update artifacts in place. Re-render the full progress bar at each section transition.
3. **Markdown only** — surface does not support inline rendering. Skip the progress bar entirely; deliver section completion summaries as plain text in the conversation, and assemble the final executive summary as markdown at the end of Section 7.

---

## Layout

Vertical stack, full width, sized to fit one previous + current + one next section in the visible viewport at common side-panel widths (~480–700px).

### Section data model

Seven sections, each with status (`not_started` | `in_progress` | `complete`) and a field list:

```
Section 1: Company & Problem
  Fields: company_name, name_meaning, problem, target_customer,
          problem_evidence, problem_severity, founder_connection

Section 2: Solution & Discovery
  Fields: solution_concept, current_alternatives, differentiation,
          customer_discovery, key_learning

Section 3: Market Opportunity
  Fields: icp, tam, sam, som, geographic_focus, industry_focus,
          why_now, supporting_trends

Section 4: Business Model
  Fields: revenue_model, pricing, pricing_positioning,
          competitive_landscape, acquisition_channel,
          unit_economics, timeline_to_revenue

Section 5: Validation Plan
  Fields: validation_completed, key_risks, ninety_day_experiments,
          success_criteria, kill_criteria

Section 6: Team
  Fields: founder_market_fit, relevant_experience, commitment_level,
          team_composition, key_gaps, first_hire

Section 7: The Ask
  Fields: funding_amount, runway, use_of_funds, key_milestones,
          validation_outcomes
```

### Section header

Each section header shows: section number, section name, status indicator (color-coded chip), and an expand/collapse caret (only meaningful for the in-progress section, since completed sections stay collapsed).

### Field display (in-progress section only)

For each field in the currently-in-progress section:

- **Filled circle** (`#759C8B` green): field has been captured. Display with a short inline summary of the captured value (truncate to ~50 chars).
- **Unfilled circle** (`#39403A` grey outline only, transparent fill): field is pending.

Use `rgba(57, 64, 58, 0.65)` beige for the field label text. Keep summaries terse — this is a status indicator, not the document.

### Progress bar fill

Above or below the section list (designer's choice — pick what reads best at narrow widths), include a thin overall progress bar. Fill color: `#F3B742` yellow. Width corresponds to `(completed sections / 7) × 100%`.

---

## States

### `not_started` (default)

- Section header background: white or very light neutral
- Section header text: `#39403A` grey
- No expand caret
- No fields visible
- No interaction affordance

### `in_progress`

- Section header background: white
- Section header text: `#C37028` orange (the only orange-text moment in the artifact — strong signal)
- Section is **expanded** — all fields render below the header
- Fields show filled / unfilled circles plus captured summaries

### `complete`

- Section header background: `#F1EFDD` light green
- Section header text: `#759C8B` green
- Section is **collapsed by default** — no fields visible
- **Click-to-expand**: clicking the section header expands the fields in place; clicking again collapses. Implement via `<details>`/`<summary>` with the native marker hidden
- Chevron indicator rotates on `[open]` to signal state (CSS-drawn, no emoji)
- Optional: small green checkmark or completion indicator (without using emoji — use a CSS-drawn checkmark or just the color shift)

### Section transition (`in_progress` → `complete`)

When a section completes:

1. The section's fields collapse (animate height to 0 over 300ms)
2. The header background transitions from white to `#F1EFDD`
3. The header text color shifts from `#C37028` to `#759C8B`
4. The next section's header text shifts from `#39403A` grey to `#C37028` orange and its fields expand (300ms animation)
5. The overall progress bar fill animates from `(N-1)/7` to `N/7`

All transitions ~300ms ease-in-out. Snappy enough to feel responsive, slow enough to register the change.

---

## Update sequence

The skill triggers updates at specific moments. After each, update the artifact in place:

| Moment | Update applied to artifact |
| --- | --- |
| Pre-Stage 1 (before first question) | Do not render yet. The progress bar is created **after the first question is answered**, not before. |
| Section 1, Question 1 answered | First render. Section 1 = `in_progress` (orange, expanded). Sections 2–7 = `not_started` (grey, collapsed). The first field captured shows a filled circle; the rest of Section 1's fields show unfilled circles. |
| Each subsequent answer in Section 1 | Flip the corresponding field's circle from unfilled → filled and add the captured summary. |
| Section 1 completion announcement | Section 1 → `complete`. Section 2 → `in_progress`. Animate the transition. |
| Each answer in Section 2 | Flip Section 2's relevant field. |
| Section 2 completion announcement | Section 2 → `complete`. Section 3 → `in_progress`. |
| ... continuing through Sections 3, 4, 5, 6 ... | Same pattern. |
| Section 7 completion announcement | Section 7 → `complete`. All sections green and collapsed. The yellow progress bar reaches 100%. |

**Do not re-emit a fresh artifact at each step** on surfaces that support in-place update. The point is that the user sees one progress bar advance through the seven sections.

---

## Responsive layout

Side-panel-first. The artifact must remain readable and useful at ~480px width and adapt upward.

### Narrow (≤ 600px)

- Vertical stack of section headers
- Section header height ~44px (touch-friendly even though desktop)
- In-progress section's fields render below the header at indented full width
- Field summaries truncate to ~36 chars before ellipsis
- Overall progress bar is narrow but always visible

### Wider (> 600px)

- Same vertical stack, no horizontal split
- Section headers more breathing room
- Field summaries truncate to ~60 chars

The progress bar artifact does NOT need a side-by-side layout — it stays vertical at all widths. Width adaptation is just type sizes, padding, and truncation.

---

## Polish (recommendations)

The Hard Requirements section above covers correctness. These are smaller polish items:

- **Animation timing.** 300ms ease-in-out on state transitions. Long enough to register, short enough to stay responsive.
- **Font choice.** System sans (`ui-sans-serif, system-ui, sans-serif`). Avoid display fonts.
- **Spacing.** Generous padding inside in-progress section so fields don't read as cramped. Tight padding on collapsed sections so the user can see context.
- **Visual hierarchy.** Section number small, section name large. Field labels (`rgba(57, 64, 58, 0.65)` beige) smaller than captured summaries (default text color).
- **No skeumorphism.** Clean flat design. The brand colors do the work.

---

## Reference Template

Below is the canonical structure for the rendered artifact. **Adapt** by substituting placeholder values (`{SECTION_1_NAME}`, captured field summaries, etc.) with real content. Keep the structure, color hexes, and class names as-is.

```html
<style>
  .pmf-progress-canvas { font-family: ui-sans-serif, system-ui, sans-serif; max-width: 100%; padding: 16px; }
  .pmf-overall-bar { width: 100%; height: 6px; background: #f0f0f0; border-radius: 3px; margin-bottom: 16px; overflow: hidden; }
  .pmf-overall-fill { height: 100%; background: #F3B742; transition: width 300ms ease-in-out; }
  .pmf-section { margin-bottom: 8px; border-radius: 6px; overflow: hidden; transition: background 300ms ease-in-out; }
  .pmf-section-header { display: flex; align-items: center; padding: 12px 14px; cursor: default; transition: color 300ms ease-in-out; }
  .pmf-section-num { font-size: 13px; opacity: 0.7; margin-right: 10px; min-width: 20px; }
  .pmf-section-name { font-size: 15px; font-weight: 600; }
  .pmf-section-fields { padding: 4px 14px 14px 44px; max-height: 0; overflow: hidden; transition: max-height 300ms ease-in-out; }
  .pmf-section.in-progress .pmf-section-fields { max-height: 1000px; }

  /* not_started */
  .pmf-section.not-started { background: #ffffff; }
  .pmf-section.not-started .pmf-section-header { color: #39403A; }

  /* in_progress */
  .pmf-section.in-progress { background: #ffffff; }
  .pmf-section.in-progress .pmf-section-header { color: #C37028; }

  /* complete (click-to-expand via <details>) */
  .pmf-section.complete { background: #F1EFDD; }
  .pmf-section.complete > summary { cursor: pointer; list-style: none; display: flex; align-items: center; padding: 12px 14px; color: #759C8B; }
  .pmf-section.complete > summary::-webkit-details-marker { display: none; }
  .pmf-section.complete .pmf-chevron { display: inline-block; width: 8px; height: 8px; margin-left: auto; border-right: 2px solid #759C8B; border-bottom: 2px solid #759C8B; transform: rotate(-45deg); transition: transform 200ms ease; }
  .pmf-section.complete[open] .pmf-chevron { transform: rotate(45deg); }
  .pmf-section.complete .pmf-section-fields { max-height: none; padding: 4px 14px 14px 44px; }

  /* fields */
  .pmf-field { display: flex; align-items: flex-start; margin: 6px 0; font-size: 13px; }
  .pmf-field-circle { width: 12px; height: 12px; border-radius: 50%; margin-right: 10px; margin-top: 4px; flex-shrink: 0; border: 1.5px solid #39403A; background: transparent; }
  .pmf-field.captured .pmf-field-circle { background: #759C8B; border-color: #759C8B; }
  .pmf-field-label { color: rgba(57, 64, 58, 0.65); font-weight: 500; min-width: 130px; }
  .pmf-field-value { color: #39403A; flex: 1; }
</style>

<div class="pmf-progress-canvas">
  <div class="pmf-overall-bar">
    <div class="pmf-overall-fill" style="width: {COMPLETED_COUNT}/7 * 100%;"></div>
  </div>

  <!-- Section 1 — Company & Problem (complete; click-to-expand) -->
  <details class="pmf-section complete">
    <summary>
      <span class="pmf-section-num">1</span>
      <span class="pmf-section-name">Company & Problem</span>
      <span class="pmf-chevron"></span>
    </summary>
    <div class="pmf-section-fields">
      <!-- captured fields persist here for review on expand -->
      <div class="pmf-field captured">
        <div class="pmf-field-circle"></div>
        <div class="pmf-field-label">Problem hypothesis</div>
        <div class="pmf-field-value">{CAPTURED_SUMMARY_TRUNCATED}</div>
      </div>
      <div class="pmf-field captured">
        <div class="pmf-field-circle"></div>
        <div class="pmf-field-label">Target customer</div>
        <div class="pmf-field-value">{CAPTURED_SUMMARY_TRUNCATED}</div>
      </div>
      <!-- ...remaining captured fields for Section 1... -->
    </div>
  </details>

  <!-- Section 2 — Solution & Discovery (currently in progress) -->
  <div class="pmf-section in-progress">
    <div class="pmf-section-header">
      <span class="pmf-section-num">2</span>
      <span class="pmf-section-name">Solution & Discovery</span>
    </div>
    <div class="pmf-section-fields">
      <div class="pmf-field captured">
        <div class="pmf-field-circle"></div>
        <div class="pmf-field-label">Solution concept</div>
        <div class="pmf-field-value">{CAPTURED_SUMMARY_TRUNCATED}</div>
      </div>
      <div class="pmf-field captured">
        <div class="pmf-field-circle"></div>
        <div class="pmf-field-label">Current alternatives</div>
        <div class="pmf-field-value">{CAPTURED_SUMMARY_TRUNCATED}</div>
      </div>
      <div class="pmf-field">
        <div class="pmf-field-circle"></div>
        <div class="pmf-field-label">Differentiation</div>
        <div class="pmf-field-value">—</div>
      </div>
      <div class="pmf-field">
        <div class="pmf-field-circle"></div>
        <div class="pmf-field-label">Customer discovery</div>
        <div class="pmf-field-value">—</div>
      </div>
      <div class="pmf-field">
        <div class="pmf-field-circle"></div>
        <div class="pmf-field-label">Key learning</div>
        <div class="pmf-field-value">—</div>
      </div>
    </div>
  </div>

  <!-- Section 3 — Market Opportunity (not started) -->
  <div class="pmf-section not-started">
    <div class="pmf-section-header">
      <span class="pmf-section-num">3</span>
      <span class="pmf-section-name">Market Opportunity</span>
    </div>
    <div class="pmf-section-fields">
      <!-- collapsed when not_started; fields not visible -->
    </div>
  </div>

  <!-- Sections 4–7 follow the same pattern: not-started until reached, in-progress while active, complete and collapsed afterward -->
</div>
```

### How to adapt the template

- **Section state classes**: every `.pmf-section` element has exactly one of `not-started`, `in-progress`, `complete`. As the skill progresses, swap classes. The CSS handles all the visual transitions.
- **Element type per state**: `not-started` and `in-progress` sections render as `<div class="pmf-section ...">`. `complete` sections render as `<details class="pmf-section complete">` with a `<summary>` for the header — this gives click-to-expand for free.
- **Field captured state**: add `.captured` to a `.pmf-field` once that field is filled. The circle fills green and the value text appears.
- **Field persistence on completion**: when transitioning a section from `in-progress` to `complete`, retain all captured field markup inside the `<details>` body. Do not strip the captured fields — they must be available when the user clicks to expand.
- **Field summaries**: keep them under ~50 chars. Truncate with ellipsis if longer.
- **Progress bar fill width**: calculate inline as `(completed_count / 7) * 100%`.
- **Forbidden**: do NOT also output a separate `<div>` or markdown list of captured fields below the artifact. The progress bar is the only place this data renders.

---

## Acceptance criteria

The visualization is correct when:

1. The progress bar appears after **Section 1, Question 1 is answered** (not on the first message).
2. Exactly one section is `in_progress` at any time, with its fields visible.
3. Completed sections are collapsed by default (`#F1EFDD` background) with only the header visible. Clicking a completed section header expands it to reveal the captured fields; clicking again collapses. A chevron indicates open/closed state.
4. Not-started sections are collapsed and grey-text headers only.
5. The four state colors (`#39403A`, `#759C8B`, `#F1EFDD`, `#C37028`) and the progress fill (`#F3B742`) are applied exactly — no substituted greys/greens/yellows.
6. The artifact renders cleanly at 480px without text overflow or unreadable fonts.
7. No emoji glyphs anywhere in the progress bar.
8. No raw CSS, unescaped HTML, or dangling markup is visible to the user at any stage.
9. Only one artifact instance exists in the conversation — updates happen in place, not as a new copy.
