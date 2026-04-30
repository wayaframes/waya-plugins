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

- Grey (not started): `#383F3B`
- Green (completed): `#6A9D8A`
- Light Green (completed background): `#D3E9E0`
- Orange (in-progress header): `#D16C02`
- Beige (field labels / subtle accents): `#D0AE89`
- Yellow (progress bar fill): `#EAB62F`

Do not substitute generic greys, greens, or yellows. These hexes must apply to backgrounds, borders, text accents, and progress fill consistently.

### 3. Pass HTML / SVG / JSX content directly — no escape wrappers

When rendering through any visualization tool that accepts HTML / JSX strings (Cowork's `show_widget`, similar host tools), pass the content directly: `<style>...</style><div>...</div>` as a literal string. Do **not** wrap in `CDATA`, template literals, JSON-encoded strings, HTML-entity escapes, or any other transport-layer wrapper. Most renderers expect raw HTML and will display escape syntax as visible garbage if it leaks through.

### 4. The `<style>` block is a real `<style>` element

Not stripped, escaped, or rendered as visible text. If CSS source appears as text in the output, that's a render bug — fix the transport, do not work around it.

### 5. Single artifact, no double-render

On surfaces that support in-place artifact updates, emit the artifact once after the first question is answered, then update in place at each subsequent section transition or data-capture moment. Never emit a fresh second copy alongside an existing one.

### 6. Only one section is `in_progress` at a time

Exactly one section has status `in_progress`. All others are either `complete` (collapsed, green) or `not_started` (collapsed, grey). The `in_progress` section must always match the section of the question currently being asked.

### 7. Completed sections are collapsed; only headers visible

Once a section transitions from `in_progress` to `complete`, its fields collapse and only the section header (now green with `#D3E9E0` background) remains visible. Do not re-expand completed sections. The user can see at most: one previous (completed) section header, the full current section with fields, and one next (not started) section header — all fitting within the visible page area.

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

- **Filled circle** (`#6A9D8A` green): field has been captured. Display with a short inline summary of the captured value (truncate to ~50 chars).
- **Unfilled circle** (`#383F3B` grey outline only, transparent fill): field is pending.

Use `#D0AE89` beige for the field label text. Keep summaries terse — this is a status indicator, not the document.

### Progress bar fill

Above or below the section list (designer's choice — pick what reads best at narrow widths), include a thin overall progress bar. Fill color: `#EAB62F` yellow. Width corresponds to `(completed sections / 7) × 100%`.

---

## States

### `not_started` (default)

- Section header background: white or very light neutral
- Section header text: `#383F3B` grey
- No expand caret
- No fields visible
- No interaction affordance

### `in_progress`

- Section header background: white
- Section header text: `#D16C02` orange (the only orange-text moment in the artifact — strong signal)
- Section is **expanded** — all fields render below the header
- Fields show filled / unfilled circles plus captured summaries

### `complete`

- Section header background: `#D3E9E0` light green
- Section header text: `#6A9D8A` green
- Section is **collapsed** — no fields visible
- Optional: small green checkmark or completion indicator (without using emoji — use a CSS-drawn checkmark or just the color shift)

### Section transition (`in_progress` → `complete`)

When a section completes:

1. The section's fields collapse (animate height to 0 over 300ms)
2. The header background transitions from white to `#D3E9E0`
3. The header text color shifts from `#D16C02` to `#6A9D8A`
4. The next section's header text shifts from `#383F3B` grey to `#D16C02` orange and its fields expand (300ms animation)
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
- **Visual hierarchy.** Section number small, section name large. Field labels (`#D0AE89` beige) smaller than captured summaries (default text color).
- **No skeumorphism.** Clean flat design. The brand colors do the work.

---

## Reference Template

Below is the canonical structure for the rendered artifact. **Adapt** by substituting placeholder values (`{SECTION_1_NAME}`, captured field summaries, etc.) with real content. Keep the structure, color hexes, and class names as-is.

```html
<style>
  .pmf-progress-canvas { font-family: ui-sans-serif, system-ui, sans-serif; max-width: 100%; padding: 16px; }
  .pmf-overall-bar { width: 100%; height: 6px; background: #f0f0f0; border-radius: 3px; margin-bottom: 16px; overflow: hidden; }
  .pmf-overall-fill { height: 100%; background: #EAB62F; transition: width 300ms ease-in-out; }
  .pmf-section { margin-bottom: 8px; border-radius: 6px; overflow: hidden; transition: background 300ms ease-in-out; }
  .pmf-section-header { display: flex; align-items: center; padding: 12px 14px; cursor: default; transition: color 300ms ease-in-out; }
  .pmf-section-num { font-size: 13px; opacity: 0.7; margin-right: 10px; min-width: 20px; }
  .pmf-section-name { font-size: 15px; font-weight: 600; }
  .pmf-section-fields { padding: 4px 14px 14px 44px; max-height: 0; overflow: hidden; transition: max-height 300ms ease-in-out; }
  .pmf-section.in-progress .pmf-section-fields { max-height: 1000px; }

  /* not_started */
  .pmf-section.not-started { background: #ffffff; }
  .pmf-section.not-started .pmf-section-header { color: #383F3B; }

  /* in_progress */
  .pmf-section.in-progress { background: #ffffff; }
  .pmf-section.in-progress .pmf-section-header { color: #D16C02; }

  /* complete */
  .pmf-section.complete { background: #D3E9E0; }
  .pmf-section.complete .pmf-section-header { color: #6A9D8A; }
  .pmf-section.complete .pmf-section-fields { max-height: 0; }

  /* fields */
  .pmf-field { display: flex; align-items: flex-start; margin: 6px 0; font-size: 13px; }
  .pmf-field-circle { width: 12px; height: 12px; border-radius: 50%; margin-right: 10px; margin-top: 4px; flex-shrink: 0; border: 1.5px solid #383F3B; background: transparent; }
  .pmf-field.captured .pmf-field-circle { background: #6A9D8A; border-color: #6A9D8A; }
  .pmf-field-label { color: #D0AE89; font-weight: 500; min-width: 130px; }
  .pmf-field-value { color: #383F3B; flex: 1; }
</style>

<div class="pmf-progress-canvas">
  <div class="pmf-overall-bar">
    <div class="pmf-overall-fill" style="width: {COMPLETED_COUNT}/7 * 100%;"></div>
  </div>

  <!-- Section 1 — Company & Problem -->
  <div class="pmf-section complete">
    <div class="pmf-section-header">
      <span class="pmf-section-num">1</span>
      <span class="pmf-section-name">Company & Problem</span>
    </div>
    <div class="pmf-section-fields">
      <!-- collapsed when complete; fields not visible -->
    </div>
  </div>

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
- **Field captured state**: add `.captured` to a `.pmf-field` once that field is filled. The circle fills green and the value text appears.
- **Field summaries**: keep them under ~50 chars. Truncate with ellipsis if longer.
- **Progress bar fill width**: calculate inline as `(completed_count / 7) * 100%`.
- **Forbidden**: do NOT also output a separate `<div>` or markdown list of captured fields below the artifact. The progress bar is the only place this data renders.

---

## Acceptance criteria

The visualization is correct when:

1. The progress bar appears after **Section 1, Question 1 is answered** (not on the first message).
2. Exactly one section is `in_progress` at any time, with its fields visible.
3. Completed sections are collapsed (`#D3E9E0` background) with only the header visible.
4. Not-started sections are collapsed and grey-text headers only.
5. The four state colors (`#383F3B`, `#6A9D8A`, `#D3E9E0`, `#D16C02`) and the progress fill (`#EAB62F`) are applied exactly — no substituted greys/greens/yellows.
6. The artifact renders cleanly at 480px without text overflow or unreadable fonts.
7. No emoji glyphs anywhere in the progress bar.
8. No raw CSS, unescaped HTML, or dangling markup is visible to the user at any stage.
9. Only one artifact instance exists in the conversation — updates happen in place, not as a new copy.
