---
name: okr-workflow-pre-pmf
description: Guide founders at pre-PMF companies through AI-assisted OKR planning sessions covering annual goal setting, quarterly planning, grading previous periods, and mid-year onboarding. Builds on Personal Ikigai, Pre-PMF Executive Summary, and Mission & Values from this kit. Use when a founder asks about OKRs, objectives, key results, quarterly planning, or annual goal-setting at an early-stage startup. Also use when a founder mentions reviewing or grading the prior quarter, doing mid-quarter check-ins, aligning OKRs to a refreshed strategy or exec summary, or translating mission and values into measurable goals. NOT for post-PMF companies with proven traction (ARR, repeatable demand) — those need a different framework, and this skill should redirect to a post-PMF OKR workflow (not yet in this kit). Output is 3-5 finalized OKRs with owners, typed measurable key results (Delta / Zero-Start / Binary / Threshold), devil's advocate KRs, priority ranking, and review cadence. Renders progress through a multi-stage side-panel tracker with Grading, Annual Review, OKRs, and Summary tabs in Waya brand colors.
---

# Waya Method: OKR Planning Guide — Pre-Product Market Fit Companies

**Purpose:** Walk founders through AI-assisted OKR (Objectives and Key Results) planning sessions for pre-product market fit companies. Handles annual goal setting, quarterly planning, grading of previous periods, and mid-year onboarding — all with guidance oriented toward discovering product-market fit.
**Duration:** 90–120 minutes (annual) or 60–90 minutes (quarterly)
**Prerequisites:** Pre-PMF Executive Summary and Mission & Values from this kit (both highly recommended). Personal Ikigai is a soft prereq for founder context. Previous OKRs only matter if grading.
**Output:** Finalized OKR set with owners, measurable key results, priority ranking, and review cadence

---

## When to Use This Skill

- Founder or executive at a pre-PMF company asks about setting OKRs, goals, or objectives
- User mentions annual planning, quarterly planning, or goal-setting for an early-stage company
- User wants to grade or review previous OKRs at a pre-PMF company
- User references customer discovery, hypothesis validation, PMF signals, or learning velocity in the context of goal-setting
- Company is still searching for product-market fit, validating core hypotheses, or in early customer development
- User mentions keywords like "OKR", "objectives", "key results", "quarterly planning", "annual goals" in the context of an early-stage startup

**Important:** if the company has validated product-market fit (e.g. $5M+ ARR, proven repeatable demand, scaling execution), this skill isn't right for them — a post-PMF OKR workflow uses different mechanics (scaling-focused metrics, fewer pivots, tighter cycles). A post-PMF OKR version isn't part of this kit yet.

---

## Visualization & Final Output

The skill renders a **single live side-panel artifact** with a multi-stage progress bar that adapts to session type (annual or quarterly), four tabs (Grading, Annual Review, OKRs, Summary), and per-OKR cards built progressively as you draft each one. Founders watch their plan take shape in real time.

**See [visualization.md](./visualization.md)** for the full rendering specification — Waya brand palette, layout, behavioral rules (single-stage-current invariant, single-OKR-at-a-time drafting display, immediate update triggers), per-tab content, the update sequence, and acceptance criteria.

Surface fallback hierarchy:

1. **Persistent inline artifact (preferred)** — surface supports JSX / HTML rendering with update-in-place (Cowork side panel, etc.). Render once before drafting OKR #1; update incrementally at each stage transition and each OKR confirmation.
2. **Re-render fallback** — surface supports inline rendering but cannot update artifacts in place. Re-render the full tracker at each stage transition.
3. **Markdown only** — surface does not support inline rendering. Skip the tracker; deliver stage-by-stage summaries in the conversation and assemble the final OKR document as markdown at Stage 6.

Render this as a **persistent side-panel artifact**, not as a wall of inline content the user has to scroll past.

---

## Prerequisite Search Protocol

Before any user interaction, search for the user's prior work:

1. **Check the current project / workspace.** If running inside a Cowork project or a connected workspace, search the project's knowledge base, files, and prior conversations for: completed Pre-PMF Executive Summary, Mission & Values document, Personal Ikigai work, prior OKR sets and grading history, team roster, customer research and interview notes.

2. **Check connected connectors.** If any of the following are available, offer to search them:
   - `~~knowledge base` — for Executive Summary, Mission & Values, prior OKR docs, customer research
   - `~~cloud storage` — for OKR exports, customer interview notes, experiment logs, prior strategy docs
   - `~~project tracker` — for prior OKR records, team roster, project completion data, milestone history (especially valuable for grading)

3. **Track what you found** before any user-facing message:
   - Pre-PMF Executive Summary: present / missing
   - Mission & Values: present / missing
   - Personal Ikigai: present / missing (soft prereq)
   - Previous OKRs: present / missing (only matters if grading)
   - Team roster: present / missing
   - Customer research: present / missing

### Branch Logic: Both Critical Prereqs Found

If BOTH the Pre-PMF Executive Summary AND Mission & Values are found:

> *"I found your Pre-PMF Executive Summary and Mission & Values [and Personal Ikigai if also found]. I'll use these to inform OKR drafting:*
>
> ***From Your Executive Summary:***
> *- Problem: [problem statement]*
> *- Solution: [solution description]*
> *- Target Customer: [ICP summary]*
> *- Key validation hypotheses: [list]*
> *- 90-day experiments planned: [list]*
>
> ***From Mission & Values:***
> *- Mission: [mission statement]*
> *- Core values: [list]*
>
> *[If Ikigai found: From Personal Ikigai: [center statement]]*
>
> ***Prior OKRs found:** [Yes — list / No, this is a first session]*
>
> *Does this look correct? Any updates before we proceed?"*

### Branch Logic: Executive Summary Missing

If the Pre-PMF Executive Summary is missing:

> *"I don't see a completed Pre-PMF Executive Summary. Your executive summary contains the validation hypotheses and 90-day experiments that should drive your OKRs. Without it, the OKRs we draft will be less grounded.*
>
> *You have three options:*
>
> *1. Run `pre-pmf-executive-summary` first (recommended) — about 60–90 minutes. It's the second skill in this kit.*
> *2. Paste a prior executive summary or business plan you already have.*
> *3. Proceed without it — I can draft generic pre-PMF OKR themes (customer discovery, value validation, PMF signals) but they won't be specific to your business hypotheses.*
>
> *Which do you want?"*

### Branch Logic: Mission & Values Missing

If Mission & Values is missing (Executive Summary may or may not be present):

> *"I don't see a finalized Mission & Values document. Mission and core values are the 'why' that quarterly objectives ladder up to. Without them, the OKRs we set will lack a strategic anchor.*
>
> *You have three options:*
>
> *1. Run `mission-values-guide` first (recommended) — about 20–30 minutes. It's the third skill in this kit.*
> *2. Paste a prior mission and values doc you already have.*
> *3. Proceed without it — we can derive a working mission directly from your executive summary, but core values won't be defined.*
>
> *Which do you want?"*

### Branch Logic: Both Critical Prereqs Missing

If BOTH the Pre-PMF Executive Summary and Mission & Values are missing:

> *"To draft useful OKRs, I really need two things:*
>
> *1. **Pre-PMF Executive Summary** — defines the problem, solution, target customer, validation hypotheses, and planned 90-day experiments your OKRs should test*
> *2. **Mission & Values** — the strategic anchor your objectives ladder up to*
>
> *I don't see either yet.*
>
> ***Recommended path:***
>
> *1. `pre-pmf-executive-summary` (60–90 min)*
> *2. `mission-values-guide` (20–30 min)*
> *3. Return here for OKRs*
>
> *Which would you like to start with?"*

### Personal Ikigai Status (soft prereq)

Personal Ikigai is informative for founder-fit context but doesn't block OKR planning. If missing, just acknowledge:

> *"I notice you haven't completed Personal Ikigai. That's fine for OKR work — it would only have informed the founder-market-fit framing. Proceeding."*

### Graceful Degradation

If any search tool is unavailable (no project context, no connectors), suggest the user connect a relevant tool so future sessions can pull context automatically. If they can't or prefer not to, ask them to paste or summarize the executive summary and mission/values directly. Note what's missing.

---

## Communication Style

- Warm but direct
- One OKR at a time for detailed drafting (outline all first, then go deep one by one)
- Present options clearly with rationale
- Ask one question at a time
- Probe for authentic reactions, not performative agreement
- **Never compliment user choices** — Avoid "good choice," "great answer," "excellent." Stay factual. Acknowledgment is fine ("Noted," "Got it," "Understood"), praise is not.
- **Never use apologetic preambles** — Avoid "Honest answer:", "To be honest:", "I should mention:". State assessments directly.

---

## Key Definitions: Customer Validation Stages

For B2B pre-PMF companies, customers typically progress through distinct validation stages:

### Design Partners

- **What:** early collaborators who work closely with you to shape the product
- **Relationship:** high-touch, frequent communication, co-creation mindset
- **Pricing:** typically free — they're investing time, you're investing product development
- **Goal:** deep qualitative learning about problem, workflow, and solution fit
- **Typical count:** 3–7 design partners
- **Commitment:** regular feedback sessions, willingness to test rough prototypes

### Pilot Customers

- **What:** users testing a more defined product with specific feature set
- **Relationship:** structured onboarding, regular check-ins, but less co-creation than design partners
- **Pricing:** may be free, discounted, or full price — part of pilot is validating willingness to pay
- **Goal:** validate value delivery, engagement, retention, and conversion at small scale
- **Typical count:** 10–30 pilots
- **Commitment:** active usage, feedback on defined workflows, potential conversion to paid

### Progression

Design Partners → Pilot Customers → Paying Customers → Scaled Acquisition

When setting OKRs, be explicit about which stage you're targeting. "Get 20 customers" means different things depending on whether they're design partners, pilots, or paying customers.

---

## Key Results: Types and Scoring

Different KR types require different scoring methods. Labeling each KR with its type at drafting time ensures unambiguous grading later.

| KR Type | When to Use | Scoring Method |
| ----- | ----- | ----- |
| **Delta / Improvement** | Scaling or efficiency metrics with existing baseline | `(Actual - Starting) / (Target - Starting)` |
| **Zero-Start** | New activities, starting from nothing | `Actual / Target` (simple completion %) |
| **Binary / Milestone** | One-time achievements | 1.0 (done) or 0.0 (not done) |
| **Threshold** | Maintain above/below a line | 1.0 (maintained) or 0.0 (breached) |

### Scoring Examples

**Delta / Improvement** (use when improving from a baseline):

- KR: "Increase monthly sales from $500K to $1M"
- Starting: $500K, Target: $1M, Actual: $900K
- **Correct:** ($900K - $500K) / ($1M - $500K) = $400K / $500K = **0.80**
- **Wrong:** $900K / $1M = 0.90 ✗

**Zero-Start** (common at pre-PMF):

- KR: "Conduct 50 customer interviews" (starting from 0)
- Target: 50, Actual: 40
- Score: 40 / 50 = **0.80**

**Zero-Start with Partial Component Completion:**

- KR: "Complete 3 discovery deliverables (interview guide, ICP doc, findings report)"
- Actual: Interview guide done (1), ICP doc done (1), Findings report 50% done (0.5)
- Score: (1 + 1 + 0.5) / 3 = **0.83**

**Binary:**

- KR: "Launch beta to first 10 users"
- Did it happen? Yes = **1.0**, No = **0.0**

**⚠️ Reserve Binary for truly indivisible milestones.** Binary scoring (1.0 or 0.0) should only be used for single, indivisible events: beta launched, contract signed, first paying customer acquired.

For KRs with multiple deliverables or components, use Zero-Start with a count instead:

- Bad (Binary): "Complete discovery phase" → 0.0 if one piece isn't done
- Good (Zero-Start): "Complete 3 discovery deliverables" → 2.5/3 = 0.83

### Prefer "from X to Y" Framing for Delta KRs

Always use explicit "from X to Y" language rather than end-state targets:

- Bad: "Achieve 40% retention" ← what's the starting point?
- Good: "Improve retention from 25% to 40%" ← clear delta
- Bad: "Get to 100 active users" ← what's the baseline?
- Good: "Grow active users from 20 to 100" ← clear delta

---

## Stage 1: Session Context & Validation

### Purpose

Validate the session plan with the user based on available data. Do not infer or guess session type — rely on existing records and confirm with the user.

### Process

**Step 1.1: Present Session Plan for Validation**

Based on available context (existing OKRs, current period, session history), present the session plan clearly:

> *"Based on your records, this session will cover:*
>
> *- [List activities in order, e.g. 'Q1 Grading → Annual Review/Modification → Q2 Goal Setting']*
>
> *Is this correct, or would you like to adjust?"*

**Step 1.2: Handle Mid-Year Q4 Onboarding**

If user is joining in Q4 and no annual OKRs exist:

> *"Since you're joining in Q4, you have two options:*
>
> ***Option A:** Set Q4 goals now to close out the year strong, then do annual planning for next year near the end of this quarter.*
>
> ***Option B:** Skip Q4 goal-setting and wait to do comprehensive annual planning about 1 month before next year starts.*
>
> *Which approach fits your situation better?"*

Save selection and proceed accordingly.

**Step 1.3: OKR Methodology Overview (Pre-PMF Focus)**

Once session plan is confirmed, provide context:

> ***"OKRs for Pre-PMF Companies***
>
> *At your stage, OKRs serve a different purpose than at scaled companies. You're not optimizing a known machine — you're searching for product-market fit. Your OKRs should:*
>
> *- **Prioritize learning over growth metrics:** 'Conduct 30 customer interviews' beats 'Grow revenue 50%' when you're still validating*
> *- **Be hypothesis-driven:** each objective should test a core assumption about your business*
> *- **Allow for pivots:** expect to learn things that change your direction — that's success, not failure*
> *- **Focus on PMF signals:** retention, organic referrals, 'very disappointed' survey scores, repeat usage*
>
> *You'll set 3–5 OKRs (not more). Each needs an owner, measurable key results, and at least one 'devil's advocate' key result to ensure you're not hiding problems.*
>
> ***Lean Startup Alignment***
>
> *Your OKRs should align with the Build-Measure-Learn feedback loop:*
>
> *- **Value Hypothesis OKRs:** test if your product delivers enough value (do customers care?)*
> *- **Growth Hypothesis OKRs:** test how new customers will discover you (can you scale?)*
>
> *At pre-PMF, prioritize Value Hypothesis OKRs first. Growth without validated value is premature scaling.*
>
> *The unit of progress isn't features shipped or revenue earned — it's **validated learning** about what customers actually want."*

**Step 1.4: Session Preparation Checklist**

> ***"Before we begin, ensure you have:***
>
> *For Grading (if applicable):*
>
> *- Access to metrics / data for each existing OKR*
> *- Notes on what worked and what blocked progress*
>
> *For Goal Setting:*
>
> *- Your current hypotheses about customers and product*
> *- Recent customer feedback or research*
> *- Understanding of your runway and resource constraints*
> *- Team members available (or their input) for ownership assignment*
>
> *For Group Sessions:*
>
> *- All key decision-makers present*
> *- 90–120 minutes blocked (annual) or 60–90 minutes (quarterly)*
>
> *Ready to proceed?"*

### Stage 1 Output

- Session plan confirmed (or adjusted)
- Mid-year onboarding choice recorded (if applicable)
- User confirms readiness to proceed

Update the side-panel tracker (see [visualization.md](./visualization.md)) at Stage 1 entry. Mark Stage 1 → complete and move to next stage on confirmation.

---

## Stage 2: Previous Period Grading

### Skip Condition

If no previous OKRs exist (e.g. first OKR session ever, or first session of a new company), skip this stage entirely. Mark the Grading tab in the artifact as "skipped" (gray with strikethrough).

### Purpose

Grade each OKR from the previous period, flag outliers for investigation, and capture learnings before setting new goals.

### Process

**Step 2.1: Present OKRs for Grading (with Project Context)**

If actuals are available (metrics, customer data, project completion rates from `~~project tracker`), pre-populate initial grades for each KR. Present these to the user for confirmation or correction. Only leave blank if no relevant data exists.

For each OKR from the previous period:

> ***"Grading: [Objective]** Owner: [Name] Period: [Period]*
>
> *Key Results:*
>
> *1. [KR1 description] - Target: [target_value] [unit]*
> *2. [KR2 description] - Target: [target_value] [unit]*
>
> ***Linked Project Context** (if available from `~~project tracker`):*
>
> *- Tasks completed: [X of Y]*
> *- Milestones hit: [list]*
> *- Blockers logged: [summary]*
>
> *What was the final outcome for each key result?"*

**Step 2.2: Calculate and Validate Grade**

Present calculation transparently using the appropriate scoring method for each KR type:

> *"Let's calculate the grade for each Key Result:*
>
> ***KR1:** [Description]*
>
> *- Type: [Delta / Zero-Start / Binary / Threshold]*
> *- [Show relevant calculation]*
> *- Score: **[X.XX]***
>
> ***KR2:** [Description]*
>
> *- Type: [Delta / Zero-Start / Binary / Threshold]*
> *- [Show relevant calculation]*
> *- Score: **[X.XX]***
>
> ***Overall OKR Score:** average of KR scores = **[X.XX]***
>
> *Does this match your records?"*

**Step 2.3: Flag Investigation (if needed)**

If grade < 0.6:

> *"This OKR scored below 0.6, which signals either:*
>
> *- **Goals were too ambitious** for the time/resources available, OR*
> *- **Execution struggled** due to blockers, priority shifts, or capability gaps*
>
> *Before we move on, which was it? And what would you do differently?"*

If grade > 0.85:

> *"This OKR scored above 0.85, which signals either:*
>
> *- **Goals were too conservative** and you could have aimed higher, OR*
> *- **Exceptional execution** that deserves recognition and replication*
>
> *Before we move on, which was it? What enabled this outcome?"*

Require a response before proceeding.

**Step 2.4: Capture Reflections**

For all OKRs (flagged or not):

> *"Quick reflection:*
>
> *- What worked well in pursuing this objective?*
> *- What blocked progress or slowed you down?"*

**Note on strategic insights from misses:** at pre-PMF, a "miss" often reveals strategic insight, not execution failure. For example, discovering customers don't want what you assumed is valuable learning that should inform your pivot. When capturing reflections, flag these cases: *"Miss due to hypothesis invalidation — validates need to pivot."* This context is valuable for Annual OKR Review in Stage 3.

**Step 2.5: Pre-PMF Specific Grading Guidance**

> ***"A note on grading at pre-PMF stage:***
>
> *A 'failed' OKR that taught you customers don't want what you assumed? That's valuable progress toward PMF.*
>
> *A 'successful' OKR that hit vanity metrics but didn't validate your core hypothesis? That's a warning sign.*
>
> *Grade honestly, but weight your interpretation toward learning velocity over raw metric achievement."*

### Stage 2 Output

- Each OKR graded with score (0.0–1.0)
- Flags investigated for outliers (<0.6 or >0.85)
- Reflections captured (what worked, what blocked)
- Strategic insights from misses documented

Update the artifact's Grading tab with all scores, flags, and reflections. Mark Stage 2 → complete.

---

## Stage 3: Annual Goal Review/Update (Quarterly Sessions Only)

### Skip Condition

If session is annual planning, skip this stage entirely — user is creating new annual OKRs, not reviewing existing ones.

### Purpose

During quarterly planning sessions, review annual OKRs and allow modifications. This is the ONLY time annual OKRs can be updated.

### Process

**Step 3.1: Surface Annual OKRs**

> ***"Your Current Annual OKRs for [Year]:***
>
> *1. **[Objective 1]** (Owner: [Name])*
>    *- [KR1], [KR2], [KR3]*
> *2. **[Objective 2]** (Owner: [Name])*
>    *- [KR1], [KR2], [KR3]*
>
> *Quarterly planning is the one time you can modify annual OKRs. Based on what you learned last quarter, do any need adjustment?"*

**Step 3.2: Recommended Modifications**

Before asking the user what to change, provide a first-pass recommendation based on grading data and learnings from the quarter:

> ***"Recommended Changes Based on Q[X] Results:***
>
> ***[Annual OKR 1]:** [Keep as-is / Adjust / Pivot / Retire]*
>
> *- Rationale: [Based on quarterly score, learnings, and what was validated/invalidated]*
>
> ***[Annual OKR 2]:** [Keep as-is / Adjust / Pivot / Retire]*
>
> *- Rationale: [Based on quarterly score, learnings, and what was validated/invalidated]*
>
> *Do you agree with these recommendations, or see it differently?"*

This grounds the conversation in data rather than open-ended questions.

**Step 3.3: Modification Options**

> *"For each annual OKR, you can:*
>
> *- **Keep as-is:** still relevant and achievable*
> *- **Adjust targets:** recalibrate key result targets based on new information*
> *- **Pivot objective:** fundamentally shift direction based on validated learning*
> *- **Retire:** no longer relevant to your path to PMF*
>
> *Which OKRs, if any, need modification?"*

**Step 3.4: Pre-PMF Modification Guidance**

> ***"Pivoting is expected at pre-PMF:***
>
> *If customer discovery revealed your initial hypothesis was wrong, changing your annual OKRs isn't failure — it's the system working.*
>
> *The question isn't 'did we stick to the plan?' but 'are we now pointed more accurately at PMF?'*
>
> *That said, avoid modifying OKRs just because they're hard. Distinguish between:*
>
> *- **Valid pivot:** new evidence changes what success looks like*
> *- **Giving up:** discomfort with ambitious goals"*

**Step 3.5: Capture Modifications**

For each modified OKR, capture what changed and why, and save the previous state for history.

### Stage 3 Output

- Annual OKRs reviewed
- Modifications captured with rationale
- Previous state preserved for audit trail

Update the artifact's Annual Review tab. Mark Stage 3 → complete (or skipped, if annual session).

---

## Stage 4: Goal Drafting

### Purpose

Create 3–5 new OKRs for the upcoming period (annual or quarterly), with proper ownership, measurable key results, and devil's advocate metrics.

### Constraints

- **Minimum:** 3 OKRs
- **Maximum:** 5 OKRs
- **Each OKR must have:** owner, 2–4 key results, at least 1 devil's advocate KR (when appropriate — see Step 4.5)

### Process

**CREATE the side-panel tracker artifact NOW (before drafting OKR #1)** with all stages in the progress bar, an empty OKRs tab, and the company name / session type in the header. This is a non-negotiable update trigger — see [visualization.md](./visualization.md).

**Step 4.1: Frame the Period**

For Annual:

> *"You're setting annual OKRs for [Year]. These are your north star objectives that quarterly goals will ladder up to.*
>
> *At pre-PMF, your annual OKRs should answer: **'What must we prove or learn this year to find product-market fit?'**"*

For Quarterly:

> *"You're setting Q[X] OKRs. These should directly support your annual objectives while being achievable in ~12 weeks.*
>
> *Reference your annual OKRs: [Display existing annual OKRs]*
>
> *Each quarterly OKR should connect to at least one annual objective."*

If any annual OKRs have downstream context (criteria or requirements captured during annual planning), surface it:

> ***"Inputs from Annual Planning:***
>
> *The following items were captured during annual planning as potential inputs for quarterly OKRs or projects:*
>
> *From [Annual OKR Objective]:*
>
> *- [downstream context items]*
>
> *Consider these as you draft quarterly Key Results or plan supporting projects."*

**Note on laddering:** quarterly OKRs typically ladder to one annual objective, but can ladder to multiple when they genuinely support both.

**Step 4.2: Pre-PMF Goal Theme Guidance**

> ***"Recommended OKR Themes for Pre-PMF (Lean Startup Aligned):***
>
> ***Value Hypothesis Themes (prioritize these first):***
>
> *1. **Customer Discovery:** deeply understand the problem and who has it*
>    *- Example: 'Validate our ICP hypothesis through direct customer engagement'*
>    *- Tests: do customers have the problem we think they have?*
>
> *2. **Value Proposition Testing:** prove your solution solves the problem **and customers will pay for it***
>    *- Example: 'Demonstrate measurable value delivery to early users **and validate willingness to pay**'*
>    *- Tests: does our MVP deliver enough value that customers care? **Will B2B customers convert to paid?***
>    *- For B2B: willingness to pay is a critical validation signal — free usage without conversion may indicate 'vitamin not painkiller'*
>
> *3. **PMF Signal Hunting:** find evidence of product-market fit*
>    *- Example: 'Achieve early indicators of organic product-market fit'*
>    *- Tests: would customers be 'very disappointed' without us?*
>
> ***Growth Hypothesis Themes (only after value is validated):***
>
> *4. **Sustainable Experimentation:** build capacity to learn fast*
>    *- Example: 'Establish rapid experimentation infrastructure'*
>    *- Tests: can we run the Build-Measure-Learn loop efficiently?*
>
> *5. **Unit Economics Exploration:** understand if the business can work*
>    *- Example: 'Validate path to sustainable unit economics'*
>    *- Tests: can we acquire customers profitably? Is LTV:CAC ratio viable?*
>
> ***⚠️ Common Pre-PMF Mistake:** setting growth OKRs (more users, more revenue) before validating that customers actually want what you're building. Resist the temptation to scale before you have something worth scaling.*
>
> *Which themes resonate with where you are right now?"*

**Step 4.3: Draft Each OKR**

**Process note:** it's fine to outline all 3–5 OKRs at a high level upfront to confirm alignment with the user. But when drafting in detail (defining KRs, asking tightening questions), work through **one OKR at a time**. Presenting multiple OKRs for detailed input simultaneously overwhelms users.

**Derive before asking:** when financial, operational, or capacity data is available (e.g. pricing, team size, engagement scope, hourly rates), calculate baseline estimates and present them in the first draft rather than asking the user to do the math. Examples: if you know engagement pricing and hourly rates, derive estimated hours per engagement; if you know team size and engagement load, derive capacity constraints. Present your calculation transparently so the user can correct assumptions, but don't make them do arithmetic you can do yourself.

For each OKR (repeat 3–5 times):

> ***"OKR [#] of [3–5]***
>
> ***Objective:** what do you want to achieve? (qualitative, inspirational) [User input]*
>
> ***Owner:** who is accountable for this? [Present team members or allow manual entry]*
>
> ***Parent Annual OKR:** [for quarterly only] which annual objective does this support?"*

**Update the artifact** to add this OKR card the moment the user confirms the objective, owner, and KRs. Don't batch multiple OKRs into a single artifact update.

**Step 4.4: Define Key Results**

For each KR (2–4 per objective):

> ***"Key Result [#]:***
>
> *- What will you measure?*
> *- What **type** of KR is this? (Delta, Zero-Start, Binary, Threshold)*
> *- What's the **starting value**? (required for Delta type, 0 for Zero-Start)*
> *- What's the **target value**?*
> *- What unit? (%, #, $, etc.)"*

When presenting drafted KRs back to the user, **always use table format**:

| Key Result | Type | From → To | Target |
| --- | --- | --- | --- |
| Conduct 50 customer interviews | Zero-Start | 0 → 50 | 50 interviews |
| Achieve 65% weekly active usage | Threshold | — | ≥ 65% |
| Improve retention | Delta | 25% → 40% | 40% |
| (DA) Track activation rate to guard against vanity signups | Threshold | — | ≥ 30% |

Tables make KR type, direction, and targets scannable at a glance. Never present KRs as bullet-point prose during drafting, review, or final output.

**Validate measurability:** *"Can this be measured objectively at the end of the period with no ambiguity? If there's any subjectivity, let's make it more concrete."*

**Step 4.5: Devil's Advocate Key Result Check**

> ***"Devil's Advocate Check:***
>
> *Every objective needs at least one KR that guards against unintended consequences or gaming the primary metrics.*
>
> *Looking at your Key Results for '[Objective]': [List KRs]*
>
> *What could go wrong if you hit these numbers? What might you sacrifice or hide to achieve them?*
>
> *Examples for pre-PMF:*
>
> *- Chasing user signups? → track activation rate or 'very disappointed' score*
> *- Rushing to ship features? → track customer-reported bugs or support load*
> *- Focused on revenue? → track churn or NPS*
> *- Running lots of experiments? → track decision quality or implemented learnings*
> *- Doing ICP discovery or GTM planning? → track prospects expressing intent to buy (validates that research is translating to real demand, not staying theoretical)*
>
> *Which devil's advocate KR will you add?"*

**When Devil's Advocate KRs are optional:**

DA KRs are **recommended but not required** for every OKR. They are most valuable when:

- KRs involve **continuous metrics that could be over-optimized** (signups, experiments run, features shipped)
- There's a risk of hitting the number while missing the spirit of the objective
- Gaming or unintended consequences are plausible

OKRs that typically **don't need** a DA KR:

- Discovery / preparation work (building interview guides, completing research phases)
- Binary milestones with inherent quality gates (launching MVP, completing hiring)
- OKRs where guardrails already exist in other OKRs

If an OKR has no natural DA, skip it rather than forcing one. Note: *"No Devil's Advocate — [reason]"* in session notes.

**Step 4.6: Generating Context-Specific Key Results**

Rather than copying template KRs, work with the user to generate KRs specific to their context:

1. **Identify the hypothesis:** what specific assumption are we testing?
2. **Find the metric:** what observable outcome would prove/disprove this hypothesis?
3. **Set the target:** what level of achievement would be ambitious but achievable given their resources and timeline?
4. **Validate measurability:** can this be measured objectively with no ambiguity?

The examples below are for reference and inspiration — not copy/paste templates. Each company's KRs should reflect their unique situation, stage, and hypotheses.

**Reference examples for pre-PMF Key Results:**

Customer Discovery:

- Conduct [X] customer problem interviews with ICP-matching prospects
- Achieve [X]% 'very disappointed' score on Sean Ellis survey
- Document [X] validated customer pain points with supporting quotes

Value Proposition:

- [X]% of pilot users report measurable improvement in [core metric]
- Achieve [X]-week retention rate among activated users
- [X]% of users complete core value action within first [timeframe]

PMF Signals:

- [X]% of new users from organic referrals
- [X]% weekly active usage rate among registered users
- Achieve [X] NPS score from active users

Experimentation:

- Run [X] validated experiments with documented learnings
- Reduce experiment cycle time to [X] days
- [X]% of experiments produce actionable insights

Unit Economics:

- Achieve [X]:1 LTV:CAC ratio on at least one channel (3:1 is healthy baseline for B2B SaaS)
- Achieve [X]-month CAC payback period
- Reach [X]% gross margin on delivered value
- [X]% of customers convert from free / trial to paid

*Note: LTV:CAC ratio is more meaningful than CAC alone — a high CAC is fine if lifetime value supports it. For early-stage, aim for at least one channel showing 3:1+ LTV:CAC potential.*

**Step 4.7: MVP Type Guidance (Lean Startup Reference)**

When key results involve building or testing:

> ***"MVP Types for Your Key Results:***
>
> *If your OKR requires building something to test, choose the lightest-weight MVP that will generate the learning you need:*

| MVP Type | When to Use | Example KR |
| ----- | ----- | ----- |
| **Landing Page** | Test demand before building | 'Achieve [X]% email signup rate' |
| **Wizard of Oz** | Test UX with manual backend | 'Complete [X] user sessions with manual fulfillment' |
| **Concierge** | Deep customer learning | 'Deliver value manually to [X] customers' |
| **Single-Feature** | Test core value prop | '[X]% of users complete core action' |
| **Piecemeal** | Test workflow with existing tools | 'Serve [X] customers using existing tools' |
| **Video MVP** | Explain complex value prop | 'Achieve [X]% I-would-pay-for-this responses' |

> *The best MVP is the one that generates validated learning fastest, not the one that's most impressive."*

**Step 4.8: Enforce Limits**

If user attempts to create more than 5 OKRs:

> *"You've drafted 5 OKRs, which is the maximum for effective focus. If this new objective is critical, which existing one should it replace?*
>
> *Remember: at pre-PMF, focus is your primary competitive advantage against larger, better-resourced companies."*

If user has fewer than 3:

> *"You have [X] OKRs. I'd recommend at least 3 to ensure you're making progress on multiple dimensions of PMF. What other area deserves focused attention this period?"*

### Stage 4 Output

- 3–5 drafted OKRs with objectives, owners, typed KRs, and devil's advocate checks
- Each KR labeled with type and start/target values
- Downstream context captured for quarterly / project cascade

Update the artifact's OKRs tab with each OKR as it's confirmed (do not batch). Mark Stage 4 → complete when all 3–5 are drafted.

---

## Stage 5: Alignment & Prioritization

### Purpose

Review all drafted OKRs together, ensure quarterly goals ladder to annual, and force prioritization.

### Process

**Step 5.1: Display All Drafted OKRs**

> ***"Your Drafted OKRs for [Period]:***
>
> ***OKR 1: [Objective]** (Owner: [Name])*
> *Hypothesis: [hypothesis]*
>
> *| Key Result | Type | From → To | Target |*
> *| ----- | ----- | ----- | ----- |*
> *| [KR1 description] | [type] | [from → to] | [target] |*
> *| [KR2 description] | [type] | [from → to] | [target] |*
> *| (DA) [KR3 description] | [type] | [from → to] | [target] |*
>
> *[Repeat for all OKRs]*
>
> *Looking at these together, do they represent the most important work for achieving PMF this [year/quarter]?"*

**Step 5.2: Ladder Check (Quarterly Only)**

> ***"Annual Alignment Check:***
>
> *| Quarterly OKR | Supports Annual OKR |*
> *| ----- | ----- |*
> *| [Q-OKR 1] | [Annual OKR X] |*
> *| [Q-OKR 2] | [Annual OKR Y] |*
>
> *Are there any annual OKRs with no quarterly support? If so, is that intentional, or should we add / adjust a quarterly objective?"*

**Step 5.3: Balance Check (Pre-PMF Specific)**

> ***"Pre-PMF Balance Check:***
>
> *Reviewing your OKRs against the PMF journey:*
>
> *- [ ] **Problem validation:** do you have OKRs that prove customers have the problem you're solving?*
> *- [ ] **Solution validation:** do you have OKRs that prove your solution works?*
> *- [ ] **PMF signals:** do you have OKRs measuring early PMF indicators?*
> *- [ ] **Monetization:** do you have OKRs validating willingness to pay?*
> *- [ ] **Sustainability:** do you have OKRs ensuring you can keep operating while searching?*
>
> *Any critical gaps?"*

**Step 5.4: Force Rank**

If user has 4–5 OKRs:

> *"If resources became constrained and you could only fully pursue 3, which would they be?*
>
> *Rank from highest to lowest priority:*
>
> *1. [Objective title only]*
> *2. [Objective title only]*
> *3. [Objective title only]*
> *4. [Objective title only]*
> *5. [Objective title only]"*

**Display note:** show only objective titles when asking for force rank — displaying full KRs is too much information to process for a prioritization decision.

Save ranking in session notes and update the artifact's OKR cards with the priority numbers.

**Step 5.5: Final Commitment**

> ***"Commitment Check:***
>
> *These [X] OKRs represent your focus for [period]. Pursuing them means saying 'no' or 'not yet' to other things.*
>
> *Are you ready to commit to these? If any feel wrong in your gut, now is the time to adjust."*

### Stage 5 Output

- Confirmation of final OKR set
- Ladder alignment verified (quarterly)
- Priority ranking captured
- Commitment recorded

Mark Stage 5 → complete on the artifact. Populate the Ladder view if quarterly.

---

## Stage 6: Output & Next Steps

### Purpose

Generate final documentation, set review cadence, and prepare for execution.

### Process

**Step 6.1: Generate Summary**

> ***"[Period] OKRs — Finalized [Date]***
>
> *---*
>
> ***OKR 1: [Objective]** Owner: [Name] | Priority: [#] | [Parent: Annual OKR X — if quarterly]*
> *Hypothesis: [hypothesis]*
>
> *| Key Result | Type | From → To | Target |*
> *| ----- | ----- | ----- | ----- |*
> *| [KR1 description] | [type] | [from → to] | [target] |*
> *| [KR2 description] | [type] | [from → to] | [target] |*
> *| (DA) [KR3 description] | [type] | [from → to] | [target] |*
>
> *---*
>
> *[Repeat for all OKRs]*
>
> *---*
>
> ***Priority Ranking:***
>
> *1. [OKR X]*
> *2. [OKR Y]*
>
> ***Next Planning Session:** [Date — calculated based on period]"*

### Export Destinations

Check which connectors are available and recommend:

- **`~~knowledge base` connected** (Notion, Confluence, etc.) → publish OKRs as a structured page or database with properties for owner, period, priority, hypothesis, KR targets, and grades. Pre-PMF companies often use a knowledge base as their primary operating system — this is a natural home.
- **`~~project tracker` connected** (Asana, Linear, Jira, etc.) → publish OKRs at the workspace level, with each KR as a trackable goal. Each quarterly OKR can also seed a project for execution.
- **`~~cloud storage` connected** (Box, Egnyte, Drive, etc.) → save the OKR summary as a document and a parallel sheet for tracking actuals against targets across the period.
- **None connected** → generate as downloadable files (markdown plus a structured data file).

**Do not push anything to external tools until the user confirms both content and destination.**

### Step 6.2: Review Cadence

For Annual OKRs:

> ***"Recommended Review Cadence:***
>
> *- **Monthly:** review KR progress, identify blockers, adjust tactics if needed (30–45 min)*
> *- **Quarterly:** full grading, annual review, and next quarter planning (90 min)*
>
> *Would you like to set up reminders?"*

For Quarterly OKRs:

> ***"Recommended Review Cadence:***
>
> *- **Weekly:** check KR progress in team standup (5 min)*
> *- **Bi-weekly:** review and adjust tactics if off-track (30 min)*
> *- **End of Quarter:** full grading and next quarter planning (60–90 min)*
>
> *Would you like to set up reminders?"*

### Step 6.3: Pre-PMF Closing Guidance

> ***"Remember — at pre-PMF, the goal of OKRs is learning:***
>
> *If you discover something that invalidates an OKR, that's not failure — that's the system working. Document what you learned, and save major pivots for your next quarterly planning session.*
>
> *The worst outcome isn't missing OKR targets. It's hitting targets that don't actually move you toward product-market fit.*
>
> *Good luck this [period]."*

### Step 6.4: Annual → Quarterly Flow Prompt (Annual Sessions Only)

**Quarterly OKR Naming Convention:** when transitioning from annual to quarterly planning, label quarterly OKRs as "Q[X]-1", "Q[X]-2", etc. (e.g. "Q2-1: Validate Target Segments"). This prevents confusion between annual OKR numbering and quarterly OKR numbering. Always include "Ladders to Annual #[Y]" in the quarterly OKR header to make the connection explicit.

After annual planning is finalized, check if the user should immediately continue into current quarter planning:

- If currently in **month 1 or 2** of the quarter → prompt to continue into quarterly OKR planning
- If currently in **month 3** of the quarter → user is already in standard next-quarter planning window, no special prompt needed

> *"Annual OKRs are now set. Since we're in [Month] (early in Q[X]), would you like to continue into Q[X] Quarterly OKR planning to set OKRs that ladder up to these annual objectives?*
>
> *This will let you immediately translate your annual goals into actionable quarterly targets."*

If user accepts, proceed to Stage 4 in quarterly mode with the just-created annual OKRs as context.

### Stage 6 Output

- Final OKR document generated and exported
- Review cadence confirmed
- Next session scheduled

Mark Stage 6 → complete on the artifact. Populate the Summary tab.

---

## Stage 7: Kit Completion & Roadmap Feedback

### Purpose

Brief acknowledgment that the user has completed the full **pre-pmf-starter** kit, plus an open invitation for what they'd want to see next. This is for the founder, not for marketing — it's how we learn what to build.

### Process

> *"You've now completed the **pre-pmf-starter** kit:*
>
> *- ✅ Personal Ikigai*
> *- ✅ Pre-PMF Executive Summary*
> *- ✅ Mission & Values*
> *- ✅ OKRs (this skill)*
>
> *That's a real foundation — personal alignment, validated direction, strategic anchor, and quarterly objectives that ladder to it. Solid place to operate from while you search for product-market fit.*
>
> *We're actively building more skills, and we'd rather build what real founders are asking for than guess. A few things on our roadmap or under consideration:*
>
> *1. **Translating quarterly OKRs into actionable project plans** — turn each OKR into a sprint-ready set of tasks with owners and deadlines.*
> *2. **Lean Startup experiment design and execution** — structure each validation hypothesis from your executive summary into a runnable experiment with explicit success and kill criteria.*
> *3. **Pre-seed / seed investor updates and board decks** — turn your quarterly OKR progress into monthly investor updates and quarterly board materials.*
> *4. **Fundraising prep — data room organization and financial modeling** — build the data room your future investor will actually open, and a financial model you can defend in a partner meeting.*
>
> *Which of these would actually help you most right now? Or what's missing — what skill would have made this kit substantially more useful?*
>
> *Open a discussion at [github.com/wayaframes/waya-plugins/discussions](https://github.com/wayaframes/waya-plugins/discussions) for public threads, or email [wayaframes@gmail.com](mailto:wayaframes@gmail.com) for private feedback. We prioritize based on what we hear from real users.*
>
> *Good luck out there."*

This stage runs **only after the full kit is detected as complete** (Personal Ikigai, Pre-PMF Executive Summary, Mission & Values, AND this OKR session). If the user got here without the prior three, skip Stage 7 — they didn't complete the kit, and the message wouldn't make sense.

---

## Session State Machine

```
START
  |
[Stage 1: Session Context & Validation]
  |
  +-- Has previous OKRs to grade? --> [Stage 2: Grading] --> continue
  +-- No grading needed --> continue
  |
  +-- Is Quarterly Session? --> [Stage 3: Annual Review/Update] --> continue
  +-- Is Annual Session --> skip to Stage 4
  |
[Stage 4: Goal Drafting]
  |
[Stage 5: Alignment & Prioritization]
  |
[Stage 6: Output & Next Steps]
  |
  +-- Full kit complete (all 4 prior skills detected)? --> [Stage 7: Kit Completion]
  +-- Not full kit --> END
  |
END
```

---

## Downstream Context Cascade Logic

OKRs feed into downstream planning:

- **Annual OKRs** → downstream context is surfaced during **Quarterly OKR** planning as suggested inputs for quarterly KRs
- **Quarterly OKRs** → downstream context is surfaced during **Project** creation as requirements or milestones

This creates a natural cascade: annual goals → quarterly objectives → project execution.

---

## Error Handling

### Missing Context

If session history is unavailable:

> *"I don't have your OKR history loaded. Let me ask a few questions to understand where you are:*
>
> *1. Is this annual planning or quarterly planning?*
> *2. Do you have existing OKRs that need grading?*
> *3. When did you start planning? (to check for mid-year onboarding)"*

### Missing Team Data

If team roster is unavailable:

> *"I don't have your team roster connected. You can either:*
>
> *- Connect a `~~project tracker` or `~~knowledge base` so I can pull team data*
> *- Enter owner names manually for now*
>
> *How would you like to proceed?"*

### User Wants to Exceed OKR Limit

> *"I understand there's a lot you want to accomplish. However, research consistently shows that more than 5 OKRs dilutes focus and reduces achievement.*
>
> *At pre-PMF especially, focus is your primary advantage. Let's prioritize ruthlessly: which of these will most accelerate your path to PMF?"*

---

## Emergency Reset: Fundamental Change Scenarios

This workflow handles standard OKR planning cycles. Sometimes the world fundamentally changes — a pandemic, major market disruption, key customer/funding loss, or other external shock that invalidates all existing goals.

If the user indicates a need for complete goal reset due to extraordinary circumstances:

> *"It sounds like you're facing a fundamental change that goes beyond normal quarterly adjustments. The standard OKR workflow isn't designed for emergency resets.*
>
> *For situations like this, an emergency strategy reset process would help you:*
>
> *- Assess the new reality*
> *- Triage existing commitments*
> *- Set emergency-mode priorities*
> *- Plan the path back to normal operations*
>
> *I don't have a structured emergency reset workflow in this kit yet — but rather than force this through the standard OKR flow, I'd recommend pausing OKR planning, doing a focused triage with your leadership team, and returning to OKR planning once the new reality is clearer. Want to talk through that triage informally now, or come back to this skill later?"*

**Trigger phrases to watch for:**

- *"Everything has changed"*
- *"We need to throw out all our goals"*
- *"The market just collapsed"*
- *"We lost our main customer/funding"*
- *"Complete pivot required"*

Do NOT attempt to handle fundamental resets within the standard OKR grading / planning flow.

---

## Clarifying Question Patterns

### When Objectives Are Vague

- *"What specific hypothesis does this objective test?"*
- *"How will you know if you've succeeded at the end of the period?"*
- *"Could a competitor say this same objective? What makes yours specific?"*

### When KRs Aren't Measurable

- *"Can this be measured objectively at the end of the period with no ambiguity?"*
- *"If two people looked at the data, would they agree on the score?"*
- *"What tool or system will you use to track this?"*

### When User Resists Devil's Advocate KRs

- *"What could go wrong if you hit these numbers?"*
- *"What might you sacrifice to achieve this metric?"*
- *"If I were an investor, what question would I ask about this OKR?"*

### When User Wants Too Many OKRs

- *"If resources became constrained, which of these would you drop first?"*
- *"Which of these, if you only achieved it, would still make this a successful period?"*

---

## Pre-PMF vs Post-PMF Differentiation Summary

This guide is specifically designed for **pre-PMF companies**:

| Aspect | Pre-PMF Approach (this skill) |
| ----- | ----- |
| **Primary Goal** | Find product-market fit |
| **OKR Themes** | Customer discovery, hypothesis validation, PMF signals |
| **Success Metrics** | Learning velocity, experiment count, retention, 'very disappointed' scores |
| **Pivot Tolerance** | High — pivots based on learning are celebrated |
| **Guidance Tone** | Exploratory, hypothesis-driven, learning-focused |
| **Example Objectives** | "Validate core value proposition", "Achieve early PMF signals" |
| **Devil's Advocate Focus** | Prevent vanity metrics, ensure learning quality |
| **Unit Economics** | LTV:CAC ratio validation (3:1+ target for viable channel) |

For post-PMF companies focused on scaling, this skill isn't right — they need a workflow oriented around scaling-focused metrics, fewer pivots, and tighter execution cycles. A post-PMF OKR workflow isn't part of this kit yet.

---

## Common Pitfalls

- Setting growth OKRs before validating product-market fit
- More than 5 OKRs (dilutes focus)
- KRs that can't be measured objectively
- Missing devil's advocate KRs on metrics that can be gamed
- Modifying annual OKRs outside quarterly reviews
- Binary scoring on multi-component deliverables
- Delta KRs without explicit starting values
- Celebrating "successful" OKRs that hit vanity metrics
- Treating OKR misses as failures rather than learning opportunities
- Forcing devil's advocate KRs where they don't add value
- Presenting all OKRs for detailed review simultaneously (one at a time)
- Confusing design partners, pilot customers, and paying customers
- Presenting KRs as bullet-point prose instead of tables (harder to scan and compare)
- Asking users to calculate baselines when the data is already available in context
- ICP discovery OKRs without a demand-validation DA (e.g. "prospects expressing intent to buy")
- Confusing annual and quarterly OKR numbering (use Q[X]-1, Q[X]-2 for quarterly)
- Batching multiple OKR confirmations into a single artifact update
