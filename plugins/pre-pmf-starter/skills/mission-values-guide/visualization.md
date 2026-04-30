# Mission & Values — Side-Panel Artifact Visualization Specification

This document specifies how to render the Mission & Values side-panel artifact. The skill produces a **single live artifact** with a 5-stage progress bar, four tabs, and progressively populated content — built across the session, not delivered at the end.

`SKILL.md` references this document at the start of Stage 1, at every stage transition, and at session completion.

---

## Rendering Rules (Hard Requirements)

These are correctness rules, not polish. Every rendered output must satisfy all of them.

### 1. Render as a persistent side-panel artifact, not inline

The artifact is the working document the founder references **while the conversation continues**. It must live in the host's persistent artifact surface (Cowork side panel, etc.) — not inline in the chat where the founder has to scroll past it. On surfaces without a side-panel concept, use whatever update-in-place affordance the host provides. Never emit it as inline markdown the user scrolls through.

### 2. Tab content lives inside its own tab

Each of the four tabs (Inputs, Mission, Values, Final) renders ONLY in its own tab body. Do not also emit a parallel `<ul>`, `<div>`, or markdown list of the same content elsewhere. Tab content appears in exactly one place: inside that tab.

### 3. Use the exact Waya brand hex colors for this skill

This skill uses the **Mission & Values palette** — distinct from other skills in this plugin. Apply these hexes exactly:

- Charcoal `#39403A` — header text, body text, default chrome
- Deep Red `#902913` — eliminated values, conflict flags
- Burnt Orange `#C37028` — alignment gaps, discussion flags
- Muted Turquoise `#759C8B` — confirmed / locked items, strong alignment
- Yellow `#F3B742` — current stage, in-progress items
- Beige `#F1EFDD` — backgrounds

Do not substitute generic colors. The semantic associations (deep red = eliminated, turquoise = locked) are deliberate.

### 4. Pass HTML / SVG / JSX content directly — no escape wrappers

When rendering through any visualization tool that accepts HTML / JSX strings (Cowork's `show_widget`, similar host tools), pass the content directly: `<style>...</style><div>...</div>` as a literal string. Do **not** wrap in `CDATA`, template literals, JSON-encoded strings, HTML-entity escapes, or any other transport-layer wrapper. Most renderers expect raw HTML and will display escape syntax as visible garbage if it leaks through.

### 5. The `<style>` block is a real `<style>` element

Not stripped, escaped, or rendered as visible text. If CSS source appears as text in the output, that's a render bug — fix the transport, do not work around it.

### 6. Single artifact, no double-render

On surfaces that support in-place artifact updates, emit the artifact once at the start of Stage 1 and update in place at each stage transition or content-change moment. Never emit a fresh second copy alongside an existing one.

### 7. Only one stage is `current` at a time

Exactly one of the five stages (Prerequisites, Synthesis, Mission, Values, Final) has status `current` (yellow). All others are either `complete` (turquoise) or `upcoming` (charcoal grey). The `current` stage must always match the section of the conversation in flight.

### 8. Use Poppins for body, DM Mono for labels

Font choices are intentional. Poppins (or system sans-serif fallback) for body content, DM Mono (or system monospace fallback) for labels and metadata. Don't substitute display fonts.

---

## Surface detection

Pick the best rendering path based on what the host supports:

1. **Persistent inline artifact (preferred)** — surface supports JSX / HTML rendering with update-in-place (Cowork side panel, etc.). Render once at the start of Stage 1; update in place at each stage transition and content-change moment.
2. **Re-render fallback** — surface supports inline rendering but cannot update artifacts in place. Re-render the full artifact at each stage transition. Acceptable but less elegant.
3. **Markdown only** — surface does not support inline rendering. Skip the artifact; deliver stage-by-stage summaries in the conversation and assemble the final mission/values doc as markdown at Stage 5.

---

## Layout

Vertical, side-panel-shaped, sized for ~480–700px width.

### Sticky header

Always visible at the top:

- Company name (or working name)
- Founder name(s) — comma-separated
- Stage progress indicator (small, below the names)

Sticky so the founder always knows where they are.

### 5-segment stage progress bar

Below the header, a horizontal bar with five segments — one per stage:

1. Prerequisites
2. Synthesis
3. Mission
4. Values
5. Final

Each segment shows:

- **Complete** — turquoise `#759C8B` fill, white check or simple line indicator (no emoji)
- **Current** — yellow `#F3B742` fill
- **Upcoming** — charcoal `#39403A` outline only, no fill

### Four tabs

Below the progress bar, four tabs the user can toggle. Default tab depends on the current stage:

- Stages 1–2 active → default to **Inputs**
- Stage 3 active → default to **Mission**
- Stage 4 active → default to **Values**
- Stage 5 active → default to **Final**

Allow the user to switch tabs at any time. Switching does not advance the stage.

#### Tab 1: Inputs (populated during Stages 1–2)

Contents:

- **Founder Ikigai summaries** — one short paragraph per founder (one-sentence Ikigai distillation)
- **Executive Summary key data** — problem statement, solution, vision, target customer (each 1–2 lines)
- **Team theme overlap matrix** — when multiple founders, the table from Step 2B with correlation strength shown via color (turquoise = strong, yellow = moderate, charcoal grey = weak)
- **Discussion flags** — any tensions or alignment gaps surfaced during synthesis, marked with burnt orange `#C37028`

#### Tab 2: Mission (populated during Stage 3)

Contents:

- **Three draft mission options** — rendered as cards. The selected option highlighted with a turquoise `#759C8B` border.
- **Refinement history** — successive iterations stacked with timestamps (newest on top)
- **Final locked mission** — when confirmed, a single hero card with turquoise border and a small lock indicator (text "LOCKED" or a CSS-drawn check, no emoji)

#### Tab 3: Values (populated during Stage 4)

Contents:

- **Initial 10 candidate values** — rendered as a ranked list with source attribution (Ikigai zone, Exec Summary section, etc.)
- **Elimination rounds** — eliminated values get the deep red `#902913` strikethrough treatment. Remaining values stay default. As elimination proceeds, the list visually narrows.
- **Final 3–7 core values** — once the user finalizes, render each as a card with: value name (large), definition (1–2 sentences), "in practice" behavior (bullet), "does not mean" clarification (bullet). Each card has a turquoise border once locked.

#### Tab 4: Final (populated during Stage 5)

Contents:

- Locked mission statement at top, hero treatment.
- Core values listed below with full definitions, "in practice," and "does not mean."
- Export-ready view — no alignment checks, no next-steps language, no session metadata. This tab is what the user would publish/export.

---

## States

### Stage indicator on the progress bar

| State | Color | Visual |
| --- | --- | --- |
| `upcoming` | `#39403A` charcoal outline | Empty segment |
| `current` | `#F3B742` yellow fill | Filled segment |
| `complete` | `#759C8B` turquoise fill | Filled segment with subtle check |

### Items inside tabs

| Status | Color treatment |
| --- | --- |
| Pending / not yet captured | Default chrome, italics or muted text |
| In progress / being refined | Yellow `#F3B742` accent (border or chip) |
| Confirmed / locked | Turquoise `#759C8B` border + small lock indicator |
| Eliminated (values only) | Deep red `#902913` strikethrough |
| Flagged (tension, gap) | Burnt orange `#C37028` accent + flag icon (CSS, no emoji) |

### Background

- Page background: `#F1EFDD` beige
- Card backgrounds: white or very light neutral for contrast against beige
- Section dividers: thin charcoal `#39403A` lines at low opacity

---

## Update sequence

The skill triggers updates at specific moments. After each, update the artifact in place:

| Moment | Update applied to artifact |
| --- | --- |
| Start of Stage 1 (prerequisite check begins) | First render. Stage 1 = `current` (yellow). All other stages = `upcoming` (charcoal). All tabs empty. Show "Searching for prerequisites..." in Inputs tab. |
| Stage 1 search results in | Populate Inputs tab with what was found (Ikigai summaries, Exec Summary data, team matrix). Mark missing prerequisites with burnt orange flags. |
| Stage 1 complete (user has confirmed context or chosen path) | Stage 1 → `complete` (turquoise). Stage 2 → `current` (yellow). |
| Stage 2 internal synthesis runs | Update Inputs tab with theme matrix and candidate lists (mission directions, value candidates). |
| Stage 2 complete (synthesis done) | Stage 2 → `complete`. Stage 3 → `current`. Switch default visible tab to Mission. |
| Stage 3 mission options rendered | Mission tab populates with three option cards. |
| Stage 3 refinement iterations | Mission tab refinement history stacks each iteration. |
| Stage 3 mission confirmed | Mission tab shows locked hero card (turquoise border). Stage 3 → `complete`. Stage 4 → `current`. Switch default tab to Values. |
| Stage 4 candidate values rendered | Values tab populates with 10-item list. |
| Stage 4 elimination rounds | Eliminated values get deep red strikethrough. Remaining values stay clean. |
| Stage 4 final values defined | Values tab populates with final 3–7 cards (turquoise border). |
| Stage 4 complete | Stage 4 → `complete`. Stage 5 → `current`. Switch default tab to Final. |
| Stage 5 final assembly | Final tab populates with the export-ready view. |
| Stage 5 confirmed / exported | Stage 5 → `complete`. All stages turquoise. |

**Do not re-emit a fresh artifact at each step** on surfaces that support in-place update.

---

## Responsive layout

Side-panel-first. Readable at ~480px.

### Narrow (≤ 600px)

- Sticky header collapses founder names to first names + initials if needed
- Progress bar segments stack vertically if width is too tight (rare — the 5 segments usually fit)
- Tab buttons full width, stack vertically below ~440px
- Card content single-column

### Wider (> 600px)

- Header has more breathing room
- Progress bar always horizontal
- Tab buttons inline horizontal
- Cards may use 2-column grid in tabs with multiple items (e.g. final values display)

---

## Polish (recommendations)

- **Stage transition animations.** ~250ms ease-in-out as the progress bar advances and tab content updates.
- **Locked-item lock indicator.** A small CSS-drawn check or "LOCKED" pill (no emoji) on confirmed mission/values.
- **Strikethrough for eliminated values.** Use deep red strikethrough; keep the value name visible at reduced opacity so the user remembers what they cut.
- **Alignment flags.** Burnt orange flag icons (CSS-drawn or unicode-but-not-emoji) for tensions or gaps.
- **Card hover** (where supported). Subtle elevation change. Don't go overboard — this is a working document, not a portfolio.

---

## Reference Template

Below is the canonical structure. **Adapt** by substituting placeholder values with real content. Keep the structure, color hexes, font stacks, and class names as-is.

```html
<style>
  :root {
    --charcoal: #39403A;
    --deep-red: #902913;
    --burnt-orange: #C37028;
    --turquoise: #759C8B;
    --yellow: #F3B742;
    --beige: #F1EFDD;
  }

  .mv-canvas {
    font-family: 'Poppins', ui-sans-serif, system-ui, sans-serif;
    color: var(--charcoal);
    background: var(--beige);
    max-width: 100%;
    padding: 16px;
  }
  .mv-label, .mv-meta {
    font-family: 'DM Mono', ui-monospace, monospace;
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    color: var(--charcoal);
    opacity: 0.7;
  }

  /* Sticky header */
  .mv-header { position: sticky; top: 0; background: var(--beige); padding: 12px 0; border-bottom: 1px solid rgba(57, 64, 58, 0.1); margin-bottom: 16px; z-index: 10; }
  .mv-company { font-size: 18px; font-weight: 600; }
  .mv-founders { font-size: 13px; opacity: 0.8; }

  /* Progress bar */
  .mv-progress { display: flex; gap: 4px; margin: 12px 0; }
  .mv-stage { flex: 1; height: 32px; border-radius: 4px; display: flex; align-items: center; justify-content: center; font-size: 12px; font-weight: 500; transition: background 250ms ease-in-out, color 250ms ease-in-out; }
  .mv-stage.upcoming { background: transparent; border: 1px solid var(--charcoal); color: var(--charcoal); opacity: 0.5; }
  .mv-stage.current { background: var(--yellow); color: var(--charcoal); }
  .mv-stage.complete { background: var(--turquoise); color: white; }

  /* Tabs */
  .mv-tabs { display: flex; gap: 4px; margin: 16px 0 12px; border-bottom: 1px solid rgba(57, 64, 58, 0.15); }
  .mv-tab { padding: 8px 14px; cursor: pointer; font-size: 13px; font-weight: 500; border: none; background: transparent; color: var(--charcoal); opacity: 0.6; }
  .mv-tab.active { opacity: 1; border-bottom: 2px solid var(--charcoal); }

  /* Cards */
  .mv-card { background: white; padding: 14px; border-radius: 6px; margin-bottom: 10px; border-left: 3px solid transparent; transition: border-color 250ms ease-in-out; }
  .mv-card.locked { border-left-color: var(--turquoise); }
  .mv-card.in-progress { border-left-color: var(--yellow); }
  .mv-card.flagged { border-left-color: var(--burnt-orange); }
  .mv-card.eliminated { opacity: 0.5; text-decoration: line-through; text-decoration-color: var(--deep-red); }

  .mv-mission-text { font-size: 16px; font-weight: 500; line-height: 1.4; }
  .mv-value-name { font-size: 15px; font-weight: 600; margin-bottom: 4px; }
  .mv-value-def { font-size: 13px; line-height: 1.4; margin-bottom: 8px; }
  .mv-value-detail { font-size: 12px; opacity: 0.85; margin-top: 4px; }

  .mv-flag-pill { display: inline-block; padding: 2px 8px; font-size: 10px; background: var(--burnt-orange); color: white; border-radius: 10px; font-family: 'DM Mono', ui-monospace, monospace; text-transform: uppercase; letter-spacing: 0.5px; }
  .mv-locked-pill { display: inline-block; padding: 2px 8px; font-size: 10px; background: var(--turquoise); color: white; border-radius: 10px; font-family: 'DM Mono', ui-monospace, monospace; text-transform: uppercase; letter-spacing: 0.5px; }

  .mv-tab-panel { display: none; }
  .mv-tab-panel.active { display: block; }
</style>

<div class="mv-canvas">
  <div class="mv-header">
    <div class="mv-company">{COMPANY_NAME}</div>
    <div class="mv-founders">{FOUNDERS}</div>
  </div>

  <div class="mv-progress">
    <div class="mv-stage complete">Prerequisites</div>
    <div class="mv-stage complete">Synthesis</div>
    <div class="mv-stage current">Mission</div>
    <div class="mv-stage upcoming">Values</div>
    <div class="mv-stage upcoming">Final</div>
  </div>

  <div class="mv-tabs">
    <button class="mv-tab">Inputs</button>
    <button class="mv-tab active">Mission</button>
    <button class="mv-tab">Values</button>
    <button class="mv-tab">Final</button>
  </div>

  <!-- Inputs tab (collapsed in this example, populated during Stages 1-2) -->
  <div class="mv-tab-panel">
    <div class="mv-label">Founder Ikigai Summaries</div>
    <div class="mv-card">
      <div class="mv-value-name">{FOUNDER_NAME}</div>
      <div class="mv-value-def">{ONE_SENTENCE_IKIGAI_SUMMARY}</div>
    </div>
    <!-- repeat per founder -->

    <div class="mv-label">Executive Summary Key Data</div>
    <div class="mv-card">
      <div class="mv-meta">Problem</div>
      <div class="mv-value-def">{PROBLEM_STATEMENT}</div>
      <div class="mv-meta" style="margin-top: 8px;">Solution</div>
      <div class="mv-value-def">{SOLUTION_DESCRIPTION}</div>
      <div class="mv-meta" style="margin-top: 8px;">Target Customer</div>
      <div class="mv-value-def">{TARGET_CUSTOMER}</div>
    </div>

    <!-- discussion flags -->
    <div class="mv-card flagged">
      <div class="mv-flag-pill">Flag</div>
      <div class="mv-value-def" style="margin-top: 6px;">{TENSION_OR_GAP_DESCRIPTION}</div>
    </div>
  </div>

  <!-- Mission tab (active in this example) -->
  <div class="mv-tab-panel active">
    <div class="mv-label">Draft Mission Options</div>
    <div class="mv-card in-progress">
      <div class="mv-meta">Option A — Problem-Centered</div>
      <div class="mv-mission-text">{OPTION_A_MISSION}</div>
      <div class="mv-value-detail">{OPTION_A_RATIONALE}</div>
    </div>
    <div class="mv-card">
      <div class="mv-meta">Option B — Impact-Centered</div>
      <div class="mv-mission-text">{OPTION_B_MISSION}</div>
      <div class="mv-value-detail">{OPTION_B_RATIONALE}</div>
    </div>
    <div class="mv-card">
      <div class="mv-meta">Option C — Customer-Centered</div>
      <div class="mv-mission-text">{OPTION_C_MISSION}</div>
      <div class="mv-value-detail">{OPTION_C_RATIONALE}</div>
    </div>

    <!-- after refinement, the locked card -->
    <!--
    <div class="mv-card locked">
      <div class="mv-locked-pill">Locked</div>
      <div class="mv-mission-text" style="margin-top: 6px;">{FINAL_MISSION_STATEMENT}</div>
    </div>
    -->
  </div>

  <!-- Values tab (collapsed, populated during Stage 4) -->
  <div class="mv-tab-panel">
    <!-- 10 candidates with eliminated ones marked -->
    <div class="mv-card eliminated">
      <div class="mv-value-name">{VALUE_NAME}</div>
      <div class="mv-meta">{SOURCE_ATTRIBUTION}</div>
      <div class="mv-value-def">{IN_PRACTICE_BEHAVIOR}</div>
    </div>
    <div class="mv-card locked">
      <div class="mv-locked-pill">Locked</div>
      <div class="mv-value-name" style="margin-top: 6px;">{FINAL_VALUE_NAME}</div>
      <div class="mv-value-def">{DEFINITION}</div>
      <div class="mv-value-detail">In practice: {IN_PRACTICE}</div>
      <div class="mv-value-detail">Does not mean: {DOES_NOT_MEAN}</div>
    </div>
  </div>

  <!-- Final tab (collapsed, populated during Stage 5) -->
  <div class="mv-tab-panel">
    <div class="mv-card locked">
      <div class="mv-meta">Mission</div>
      <div class="mv-mission-text" style="margin-top: 6px;">{FINAL_MISSION}</div>
    </div>
    <div class="mv-label" style="margin-top: 16px;">Core Values</div>
    <!-- one card per final value -->
  </div>
</div>
```

### How to adapt the template

- **Stage classes**: every `.mv-stage` element has exactly one of `upcoming`, `current`, `complete`. As the session progresses, swap classes. The CSS handles all visual transitions.
- **Tab visibility**: only one `.mv-tab-panel` has the `active` class at a time. Switching tabs swaps the active class.
- **Card states**: `in-progress` (yellow border), `locked` (turquoise border + locked pill), `flagged` (burnt orange border + flag pill), `eliminated` (deep red strikethrough at reduced opacity).
- **Default tab on stage transitions**: when stage advances from 2 → 3, switch active tab to Mission. When 3 → 4, switch to Values. When 4 → 5, switch to Final. The user can override by clicking a different tab.
- **Forbidden**: do NOT also output a parallel `<div>` or markdown list of mission options or values below this artifact. Each tab's content lives only in its tab.

---

## Acceptance criteria

The visualization is correct when:

1. The artifact appears at the start of Stage 1 (not later).
2. Exactly one stage is `current` at any time, with the matching tab as the default visible tab.
3. The exact six Waya brand hexes from this skill's palette are applied (no generic substitutes).
4. Eliminated values use deep red strikethrough; locked items use turquoise borders; flags use burnt orange.
5. The artifact renders cleanly at 480px without text overflow or unreadable fonts.
6. Poppins (or system sans fallback) for body, DM Mono (or system mono fallback) for labels.
7. No emoji glyphs anywhere — all status indicators are CSS-drawn.
8. No raw CSS, unescaped HTML, or dangling markup is visible to the user at any stage.
9. Only one artifact instance exists in the conversation — updates happen in place, not as a new copy.
