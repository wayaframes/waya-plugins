# OKR Workflow — Side-Panel Tracker Visualization Specification

This document specifies how to render the OKR planning tracker. The skill produces a **single live side-panel artifact** with a multi-stage progress bar that adapts to session type, four content tabs (Grading, Annual Review, OKRs, Summary), and per-OKR cards built progressively as each OKR is confirmed.

`SKILL.md` references this document at the start of each stage and at every artifact-update trigger.

---

## Rendering Rules (Hard Requirements)

These are correctness rules, not polish. Every rendered output must satisfy all of them.

### 1. Render as a persistent side-panel artifact, not inline

The artifact is the working document the founder references **while the conversation continues**. It must live in the host's persistent artifact surface (Cowork side panel, etc.) — not inline in the chat where the founder has to scroll past it. Use whatever update-in-place affordance the host provides.

### 2. Tab content lives inside its own tab

Each of the four tabs (Grading, Annual Review, OKRs, Summary) renders ONLY in its own tab body. Do not also emit a parallel `<ul>`, `<div>`, or markdown list of the same content elsewhere. Tab content appears in exactly one place: inside that tab.

### 3. Use the exact Waya brand hex colors for this skill

This skill uses the same **Mission & Values palette** — preserves brand consistency across the second half of the kit:

- Charcoal `#39403A` — header text, body text, default chrome
- Deep Red `#902913` — missed targets, flagged OKRs (grade < 0.6), failed thresholds
- Burnt Orange `#C37028` — stretch targets, timeline items, attention flags
- Muted Turquoise `#759C8B` — completed stages, on-track OKRs, locked items
- Yellow `#F3B742` — current stage, in-progress drafting items
- Beige `#F1EFDD` — page background

Do not substitute generic colors. The semantic associations (deep red = missed, turquoise = on track) are deliberate.

### 4. Pass HTML / SVG / JSX content directly — no escape wrappers

When rendering through any visualization tool that accepts HTML / JSX strings (Cowork's `show_widget`, similar host tools), pass the content directly. Do **not** wrap in `CDATA`, template literals, JSON-encoded strings, HTML-entity escapes, or any other transport-layer wrapper.

### 5. The `<style>` block is a real `<style>` element

Not stripped, escaped, or rendered as visible text. If CSS source appears as text in the output, that's a render bug — fix the transport, do not work around it.

### 6. Single artifact, no double-render

On surfaces that support in-place updates, emit the artifact once at Stage 4 entry (before drafting OKR #1) and update in place at every subsequent trigger. Never emit a second copy alongside an existing one.

### 7. Update at every trigger — DO NOT BATCH

This skill has strict update-trigger requirements. The founder must see the artifact change as they confirm content. Triggers:

| Trigger | Action |
| --- | --- |
| Stage 4 entry (before OKR #1 drafting) | **CREATE** the artifact (stages bar + empty OKRs tab + header) |
| Each individual OKR confirmed by user | Add that OKR card to the OKRs tab **immediately** |
| Each grading score entered | Add that score to the Grading tab **immediately** |
| Stage 5 alignment / prioritization complete | Update priority numbers on all OKR cards |
| Stage 6 commitment confirmed | Flip all stages to `complete`, populate Summary tab |
| Annual → Quarterly transition | Reset stages bar for quarterly flow, add quarterly OKRs as they're confirmed |

**Do NOT defer updates. Do NOT batch multiple confirmations into a single artifact update.** The founder should see their OKR populate the tracker the moment they confirm it. Batching breaks the "watching it take shape" experience.

### 8. Only one stage is `current` at a time

Exactly one stage segment shows `current` (yellow). All others are either `complete` (turquoise), `upcoming` (charcoal grey), or `skipped` (gray with strikethrough — for stages that don't apply, e.g. no grading on first session).

### 9. Use Poppins for body, DM Mono for labels

Font choices preserve brand consistency. Poppins (or system sans fallback) for body, DM Mono (or system mono fallback) for labels and metadata.

### 10. No emojis anywhere

Use color and CSS-drawn indicators only. No emoji checkmarks, no emoji flags, no emoji status icons.

---

## Surface detection

Pick the best rendering path based on what the host supports:

1. **Persistent inline artifact (preferred)** — surface supports JSX / HTML rendering with update-in-place (Cowork side panel, etc.). Render once at Stage 4 entry; update in place at every trigger.
2. **Re-render fallback** — surface supports inline rendering but cannot update artifacts in place. Re-render the full tracker at each stage transition. Confirmed-OKR cards still get re-emitted, just less elegantly.
3. **Markdown only** — surface does not support inline rendering. Skip the tracker; deliver stage-by-stage summaries in the conversation and assemble the final OKR document as markdown at Stage 6.

---

## Layout

Vertical, side-panel-shaped, sized for ~480–700px width.

### Sticky header

Always visible at the top:

- Company name (or working name)
- Session type chip — "Annual" or "Quarterly", color-coded charcoal
- Period — "FY 2026" or "Q2 2026"
- Stages-completed counter — "3 of 6"

Sticky so the founder always knows where they are.

### Multi-segment stage progress bar (adapts to session type)

Below the header, a horizontal bar with stage segments. **The number of segments depends on session type:**

- **Annual session** (5 stages): Context → Grading → Drafting → Alignment → Output
- **Quarterly session** (6 stages): Context → Grading → Annual Review → Drafting → Alignment → Output

If a stage doesn't apply (e.g. first OKR session ever, no grading), show that segment with `skipped` styling (gray with strikethrough text). Do not omit it — keep the structure consistent.

After Stage 6, the artifact has finished its primary purpose. Stage 7 (kit-completion roadmap message) is a conversational message, not a new tracker stage — don't add a 7th segment.

Each segment shows:

- **Complete** — turquoise `#759C8B` fill, subtle CSS-drawn check
- **Current** — yellow `#F3B742` fill
- **Upcoming** — charcoal `#39403A` outline only
- **Skipped** — gray `#999` outline with strikethrough text

### Four tabs

Below the progress bar, four tabs the user can toggle. Default tab depends on the current stage:

- Stages 1–2 → default to **Grading**
- Stage 3 → default to **Annual Review** (quarterly only — skip if annual session)
- Stages 4–5 → default to **OKRs** (the main working tab)
- Stage 6 → default to **Summary**

Allow the user to switch tabs at any time. Switching does not advance the stage.

#### Tab 1: Grading (populated during Stage 2)

For each previous-period OKR:

- Objective and owner
- Hypothesis tested
- KR table with score per KR (color-coded: green ≥ 0.7, yellow 0.4–0.69, red < 0.4)
- Overall OKR score
- Flag chip if grade < 0.6 or > 0.85
- Investigation note (what was the cause)
- Reflection summary (what worked, what blocked)
- "Strategic insight" callout if a miss revealed hypothesis invalidation

Skipped (gray + strikethrough header) if no previous OKRs exist.

#### Tab 2: Annual Review (populated during Stage 3, quarterly sessions only)

For each annual OKR:

- Current state vs. proposed modification (Keep / Adjust / Pivot / Retire)
- Modification rationale
- Hypothesis evolution — did the core assumption change?
- Previous state preserved for audit

Skipped (gray + strikethrough header) for annual sessions.

#### Tab 3: OKRs (populated during Stage 4 + 5 — the main working tab)

The heart of the artifact. For each drafted OKR:

- **OKR card** with:
  - Objective (large, bold)
  - Hypothesis being tested
  - Owner
  - Priority rank (after Stage 5)
  - Parent annual OKR (if quarterly)
  - **KR table** in scannable format:

| Key Result | Type | From → To | Target |
| --- | --- | --- | --- |
| ... | ... | ... | ... |

  - Devil's advocate KR flagged with a "DA" pill
  - "No DA — [reason]" if intentionally skipped
  - Card border color reflects state: yellow (in-progress drafting), turquoise (locked / confirmed)

Pre-PMF stage labels (Discovery → Validation → Early Traction) shown as small context chips on each card.

Updates in real-time during drafting and alignment stages — every confirmed OKR populates immediately.

#### Tab 4: Summary (populated during Stage 6)

Final exportable view:

- All finalized OKRs in priority order
- Each with hypothesis and full KR table
- Priority ranking visible
- Review cadence (weekly / bi-weekly / quarterly per session type)
- Next session date
- Key PMF signals to watch (extracted from the OKRs)
- Export destinations the user has chosen (or "Pending export")

This tab is what the user would publish or hand off — clean, no session metadata.

---

## States

### Stage indicator

| State | Color | Visual |
| --- | --- | --- |
| `upcoming` | `#39403A` charcoal outline | Empty segment, normal text |
| `current` | `#F3B742` yellow fill | Filled segment |
| `complete` | `#759C8B` turquoise fill | Filled segment with subtle check |
| `skipped` | `#999` outline | Empty segment, strikethrough text |

### OKR card border

| State | Color |
| --- | --- |
| Drafting in progress | `#F3B742` yellow |
| Locked / confirmed | `#759C8B` turquoise |
| Flagged for attention | `#C37028` burnt orange |
| Off-track / scored < 0.6 (grading view) | `#902913` deep red |

### KR score color

| Score | Color |
| --- | --- |
| ≥ 0.7 | `#759C8B` turquoise |
| 0.4–0.69 | `#F3B742` yellow |
| < 0.4 | `#902913` deep red |

### Background

- Page: `#F1EFDD` beige
- Cards: white or very light neutral for contrast
- Section dividers: thin charcoal `#39403A` lines at low opacity

---

## Update sequence

| Moment | Update applied to artifact |
| --- | --- |
| Stage 1 entry | First render of header + stages bar (Stage 1 = `current`). All tabs empty. |
| Stage 1 confirm session type | Adapts the stages bar to annual (5 segments) or quarterly (6). |
| Stage 1 complete | Stage 1 → `complete`. Stage 2 → `current` (or `skipped` if no prior OKRs, advance to Stage 3 or 4). |
| Stage 2 each grade entered | Add that score to the Grading tab immediately. |
| Stage 2 complete | Stage 2 → `complete`. Move to Stage 3 or 4 depending on session type. |
| Stage 3 modification recommendations rendered | Annual Review tab populates with current annual OKRs and proposed changes. |
| Stage 3 complete (quarterly only) | Stage 3 → `complete`. Stage 4 → `current`. Switch default tab to OKRs. |
| Stage 4 entry (before OKR #1 drafting) | Create the artifact OKRs tab fresh. Stages bar shows Stage 4 = `current`. |
| Stage 4 each OKR confirmed | Add that OKR card to the OKRs tab **immediately**. Border = yellow during drafting, turquoise on lock. |
| Stage 4 complete | All 3–5 OKRs rendered. Stage 4 → `complete`. Stage 5 → `current`. |
| Stage 5 priority ranking | Update priority numbers on all OKR cards. |
| Stage 5 complete | Stage 5 → `complete`. Stage 6 → `current`. Switch default tab to Summary. |
| Stage 6 final assembly | Summary tab populates with the export-ready view. |
| Stage 6 export confirmed | Stage 6 → `complete`. All stages turquoise. |
| Annual → Quarterly continuation | Reset stages bar for quarterly flow, leave OKRs tab populated with annual + new quarterly OKRs as they're confirmed. |

**Do not re-emit a fresh artifact at each step** on surfaces that support in-place update.

---

## Responsive layout

Side-panel-first. Readable at ~480px.

### Narrow (≤ 600px)

- Sticky header collapses session-type chip below the company name if needed
- Progress bar segments reduce padding to fit; stage labels truncate to first letter or icon if necessary
- Tab buttons full width, may stack vertically below ~440px
- OKR cards single-column
- KR tables collapse — KR description full-width, type/from-to/target on a second line as small text

### Wider (> 600px)

- Header has more breathing room
- Progress bar always horizontal with full segment labels
- Tab buttons inline horizontal
- OKR cards may use 2-column grid in tabs with multiple items
- KR tables full table layout

---

## Polish (recommendations)

- **Stage transition animations.** ~250ms ease-in-out as the progress bar advances and tab content updates.
- **Locked-OKR pill.** Small CSS-drawn check or "LOCKED" pill on confirmed OKR cards (no emoji).
- **DA KR badge.** Inline "DA" pill next to devil's advocate KR rows so they're scannable.
- **Score chip.** Each KR score shown as a colored pill (turquoise / yellow / deep red based on threshold) for quick scanning in the Grading tab.
- **Skipped-stage strikethrough.** Strikethrough on skipped stage segment label, gray rendering. Makes the omission deliberate-looking.

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

  .okr-canvas {
    font-family: 'Poppins', ui-sans-serif, system-ui, sans-serif;
    color: var(--charcoal);
    background: var(--beige);
    max-width: 100%;
    padding: 16px;
  }
  .okr-label, .okr-meta {
    font-family: 'DM Mono', ui-monospace, monospace;
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    color: var(--charcoal);
    opacity: 0.7;
  }

  /* Sticky header */
  .okr-header { position: sticky; top: 0; background: var(--beige); padding: 12px 0; border-bottom: 1px solid rgba(57, 64, 58, 0.1); margin-bottom: 16px; z-index: 10; }
  .okr-company { font-size: 18px; font-weight: 600; }
  .okr-meta-row { display: flex; gap: 12px; margin-top: 4px; align-items: center; }
  .okr-session-chip { padding: 2px 10px; background: var(--charcoal); color: white; border-radius: 10px; font-family: 'DM Mono', ui-monospace, monospace; font-size: 10px; text-transform: uppercase; letter-spacing: 0.5px; }
  .okr-period { font-size: 12px; opacity: 0.7; }

  /* Progress bar (adapts to session type) */
  .okr-progress { display: flex; gap: 4px; margin: 12px 0; }
  .okr-stage { flex: 1; height: 32px; border-radius: 4px; display: flex; align-items: center; justify-content: center; font-size: 11px; font-weight: 500; transition: background 250ms ease-in-out, color 250ms ease-in-out; padding: 0 6px; }
  .okr-stage.upcoming { background: transparent; border: 1px solid var(--charcoal); color: var(--charcoal); opacity: 0.5; }
  .okr-stage.current { background: var(--yellow); color: var(--charcoal); }
  .okr-stage.complete { background: var(--turquoise); color: white; }
  .okr-stage.skipped { background: transparent; border: 1px solid #999; color: #999; text-decoration: line-through; }

  /* Tabs */
  .okr-tabs { display: flex; gap: 4px; margin: 16px 0 12px; border-bottom: 1px solid rgba(57, 64, 58, 0.15); }
  .okr-tab { padding: 8px 14px; cursor: pointer; font-size: 13px; font-weight: 500; border: none; background: transparent; color: var(--charcoal); opacity: 0.6; }
  .okr-tab.active { opacity: 1; border-bottom: 2px solid var(--charcoal); }

  /* OKR cards */
  .okr-card { background: white; padding: 14px; border-radius: 6px; margin-bottom: 12px; border-left: 3px solid transparent; transition: border-color 250ms ease-in-out; }
  .okr-card.in-progress { border-left-color: var(--yellow); }
  .okr-card.locked { border-left-color: var(--turquoise); }
  .okr-card.flagged { border-left-color: var(--burnt-orange); }
  .okr-card.failed { border-left-color: var(--deep-red); }

  .okr-objective { font-size: 15px; font-weight: 600; margin-bottom: 4px; }
  .okr-hypothesis { font-size: 12px; opacity: 0.75; font-style: italic; margin-bottom: 8px; }
  .okr-priority { display: inline-block; padding: 2px 8px; background: var(--charcoal); color: white; border-radius: 10px; font-family: 'DM Mono', ui-monospace, monospace; font-size: 10px; margin-right: 6px; }

  /* KR tables */
  .kr-table { width: 100%; font-size: 12px; border-collapse: collapse; margin-top: 8px; }
  .kr-table th { font-family: 'DM Mono', ui-monospace, monospace; font-size: 10px; text-transform: uppercase; letter-spacing: 0.5px; opacity: 0.7; text-align: left; padding: 4px 6px; border-bottom: 1px solid rgba(57, 64, 58, 0.15); }
  .kr-table td { padding: 6px; border-bottom: 1px solid rgba(57, 64, 58, 0.08); }
  .kr-da-pill { display: inline-block; padding: 1px 6px; background: var(--burnt-orange); color: white; border-radius: 8px; font-family: 'DM Mono', ui-monospace, monospace; font-size: 9px; margin-right: 4px; }

  /* Score chips (Grading tab) */
  .score-chip { display: inline-block; padding: 2px 8px; border-radius: 10px; font-family: 'DM Mono', ui-monospace, monospace; font-size: 11px; font-weight: 600; }
  .score-chip.high { background: var(--turquoise); color: white; }
  .score-chip.mid { background: var(--yellow); color: var(--charcoal); }
  .score-chip.low { background: var(--deep-red); color: white; }

  .locked-pill { display: inline-block; padding: 2px 8px; background: var(--turquoise); color: white; border-radius: 10px; font-family: 'DM Mono', ui-monospace, monospace; font-size: 10px; }
  .flag-pill { display: inline-block; padding: 2px 8px; background: var(--burnt-orange); color: white; border-radius: 10px; font-family: 'DM Mono', ui-monospace, monospace; font-size: 10px; }

  .okr-tab-panel { display: none; }
  .okr-tab-panel.active { display: block; }
</style>

<div class="okr-canvas">
  <div class="okr-header">
    <div class="okr-company">{COMPANY_NAME}</div>
    <div class="okr-meta-row">
      <span class="okr-session-chip">{SESSION_TYPE}</span>
      <span class="okr-period">{PERIOD}</span>
      <span class="okr-period">{N} of {TOTAL} stages</span>
    </div>
  </div>

  <!-- Progress bar — quarterly session shown (6 segments). Annual session has 5 (no Annual Review). -->
  <div class="okr-progress">
    <div class="okr-stage complete">Context</div>
    <div class="okr-stage complete">Grading</div>
    <div class="okr-stage complete">Annual Review</div>
    <div class="okr-stage current">Drafting</div>
    <div class="okr-stage upcoming">Alignment</div>
    <div class="okr-stage upcoming">Output</div>
  </div>

  <div class="okr-tabs">
    <button class="okr-tab">Grading</button>
    <button class="okr-tab">Annual Review</button>
    <button class="okr-tab active">OKRs</button>
    <button class="okr-tab">Summary</button>
  </div>

  <!-- OKRs tab (active during drafting + alignment) -->
  <div class="okr-tab-panel active">
    <!-- locked OKR card -->
    <div class="okr-card locked">
      <span class="okr-priority">P1</span>
      <span class="locked-pill">Locked</span>
      <div class="okr-objective" style="margin-top: 8px;">{OBJECTIVE_1}</div>
      <div class="okr-hypothesis">Hypothesis: {HYPOTHESIS_1}</div>
      <div class="okr-meta">Owner: {OWNER_1} · Ladders to: Annual #{ANNUAL_PARENT}</div>
      <table class="kr-table">
        <thead>
          <tr><th>Key Result</th><th>Type</th><th>From → To</th><th>Target</th></tr>
        </thead>
        <tbody>
          <tr>
            <td>{KR1_DESCRIPTION}</td>
            <td>{KR1_TYPE}</td>
            <td>{KR1_FROM_TO}</td>
            <td>{KR1_TARGET}</td>
          </tr>
          <tr>
            <td><span class="kr-da-pill">DA</span>{KR_DA_DESCRIPTION}</td>
            <td>{KR_DA_TYPE}</td>
            <td>{KR_DA_FROM_TO}</td>
            <td>{KR_DA_TARGET}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- in-progress OKR card (yellow border, being drafted now) -->
    <div class="okr-card in-progress">
      <span class="okr-priority">P2</span>
      <div class="okr-objective" style="margin-top: 8px;">{OBJECTIVE_2}</div>
      <div class="okr-hypothesis">Hypothesis: {HYPOTHESIS_2}</div>
      <div class="okr-meta">Owner: {OWNER_2}</div>
      <!-- KR table populates as user confirms each KR -->
    </div>
  </div>

  <!-- Grading tab (populated during Stage 2; example shows scored OKR) -->
  <div class="okr-tab-panel">
    <div class="okr-card failed">
      <div class="okr-objective">{PREVIOUS_OBJECTIVE}</div>
      <div class="okr-hypothesis">Hypothesis tested: {PREVIOUS_HYPOTHESIS}</div>
      <div class="okr-meta">Owner: {PREVIOUS_OWNER} · Period: {PREVIOUS_PERIOD}</div>
      <table class="kr-table">
        <tbody>
          <tr>
            <td>{KR1_DESCRIPTION}</td>
            <td><span class="score-chip low">0.32</span></td>
          </tr>
          <tr>
            <td>{KR2_DESCRIPTION}</td>
            <td><span class="score-chip mid">0.65</span></td>
          </tr>
        </tbody>
      </table>
      <div style="margin-top: 8px;">
        <span class="flag-pill">Flagged: 0.48 overall</span>
      </div>
      <div class="okr-meta" style="margin-top: 8px;">Strategic insight</div>
      <div style="font-size: 13px;">{INSIGHT_FROM_MISS}</div>
    </div>
  </div>

  <!-- Annual Review tab (populated during Stage 3, quarterly only) -->
  <div class="okr-tab-panel">
    <div class="okr-card flagged">
      <div class="okr-objective">{ANNUAL_OBJECTIVE}</div>
      <div class="okr-meta">Recommendation: {KEEP_ADJUST_PIVOT_RETIRE}</div>
      <div style="font-size: 13px; margin-top: 6px;">{RATIONALE}</div>
    </div>
  </div>

  <!-- Summary tab (populated at Stage 6 — final exportable view) -->
  <div class="okr-tab-panel">
    <div class="okr-label">{PERIOD} OKRs — Finalized {DATE}</div>
    <!-- one card per finalized OKR in priority order -->
    <div class="okr-card locked">
      <span class="okr-priority">P1</span>
      <div class="okr-objective" style="margin-top: 8px;">{OBJECTIVE_1}</div>
      <table class="kr-table">
        <!-- full KR rows -->
      </table>
    </div>
    <div class="okr-label" style="margin-top: 16px;">Review Cadence</div>
    <div style="font-size: 13px;">{CADENCE_RECOMMENDATIONS}</div>
    <div class="okr-label" style="margin-top: 12px;">Next Planning Session</div>
    <div style="font-size: 13px;">{NEXT_SESSION_DATE}</div>
  </div>
</div>
```

### How to adapt the template

- **Stages bar**: render 5 or 6 segments based on session type. Use `complete` / `current` / `upcoming` / `skipped` classes per the state of each stage.
- **Tab visibility**: only one `.okr-tab-panel` has the `active` class at a time. Switch active panel when stage advances or user clicks a tab.
- **OKR card states**: `in-progress` (yellow), `locked` (turquoise + locked pill), `flagged` (burnt orange), `failed` (deep red, grading view only).
- **KR rows**: build the KR table progressively as the user confirms each KR. DA rows get the inline "DA" pill prefix.
- **Score chips**: in Grading tab, color the score by threshold — high (≥0.7), mid (0.4–0.69), low (<0.4).
- **Forbidden**: do NOT also output a parallel `<div>` or markdown list of OKRs / scores / KRs below this artifact. Each tab's content lives only in its tab.

---

## Acceptance criteria

The visualization is correct when:

1. The artifact is **created at Stage 4 entry** (before drafting OKR #1) — not later.
2. Each OKR populates its card **the moment the user confirms it**, not in a batch.
3. Each grading score appears in the Grading tab the moment it's entered.
4. Exactly one stage is `current` at any time; skipped stages render with strikethrough.
5. The exact six Waya Mission/Values palette hexes are applied (no generic substitutes).
6. Failed/missed OKRs use deep red borders; locked OKRs use turquoise borders; in-progress drafting uses yellow borders.
7. KRs render in scannable table format (Key Result | Type | From → To | Target) — never as bullet-point prose.
8. Devil's advocate KRs are flagged with an inline "DA" pill.
9. The artifact renders cleanly at 480px without text overflow or unreadable fonts.
10. Poppins (or system sans fallback) for body, DM Mono (or system mono fallback) for labels.
11. No emoji glyphs anywhere — all status indicators are CSS-drawn.
12. No raw CSS, unescaped HTML, or dangling markup is visible to the user at any stage.
13. Only one artifact instance exists in the conversation — updates happen in place, not as a new copy.
