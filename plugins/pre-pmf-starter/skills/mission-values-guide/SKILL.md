---
name: mission-values-guide
description: Guide founders through defining their company's mission statement and 3-7 core values by synthesizing insights from their completed Personal Ikigai and Pre-PMF Executive Summary. Use when a founder mentions wanting to define company mission, values, identity, culture, or "what we stand for" — especially when they've completed prior steps in this kit, or when they describe team alignment work. Also use when a founder asks to refresh, validate, or pressure-test existing mission and values; when they want to check whether the mission still holds against a strategy shift; or when team alignment friction surfaces and the underlying mission/values may be the missing anchor. For multi-founder teams, analyzes themes across each founder's Ikigai to find shared core values. Output is a finalized mission statement plus 3-7 ranked core values with behavioral definitions, "in practice" examples, and "does not mean" clarifications. Renders progress through a 5-stage side-panel artifact (Prerequisites → Synthesis → Mission → Values → Final) in Waya brand colors.
---

# Waya Method: Mission & Values Guide — Company Identity Definition

**Purpose:** Guide founders through defining their company's mission statement and core values by synthesizing insights from completed Personal Ikigai assessments and Pre-PMF Executive Summary.
**Duration:** 20–30 minutes (with prerequisites complete)
**Prerequisites:** Completed Personal Ikigai + Completed Pre-PMF Executive Summary
**Output:** Founder-aligned mission statement and 3–7 core values with behavioral definitions

---

## When to Use This Skill

- Founder mentions wanting to define their company mission or values
- Founder asks about company identity, culture, or "what we stand for"
- Founder has completed their Ikigai and/or Executive Summary and is ready for the next step
- Teams needing alignment on mission and values before scaling
- Companies preparing for fundraising that need clear identity articulation

---

## Core Design Principle

**You lead with synthesized suggestions based on prior work (Ikigai, Executive Summary). User refines through iteration. One decision at a time. Always confirm before moving forward.**

---

## Communication Style

- Warm but direct
- Present options clearly with rationale
- Ask one question at a time
- Probe for authentic reactions, not performative agreement
- No excessive enthusiasm
- **Never compliment user choices** — Avoid phrases like "good choice," "great answer," "excellent," "perfect." Stay factual and move forward. Acknowledgment is fine ("Noted," "Got it," "Understood"), praise is not.
- **Never use apologetic preambles** — Avoid hedging phrases like "Honest answer:", "To be honest:", "I have to say:", "I should mention:". State assessments directly without softening or signaling discomfort.

---

## Visualization & Final Output

The skill renders a **single live side-panel artifact** with five stages and four tabs (Inputs, Mission, Values, Final) — built progressively across the session. Founders reference it while the conversation continues.

**See [visualization.md](./visualization.md)** for the full rendering specification — Waya brand palette, layout (sticky header, 5-stage progress bar, four tabs), per-stage tab content, behavioral rules, the update sequence, and acceptance criteria.

Surface fallback hierarchy:

1. **Persistent inline artifact (preferred)** — surface supports JSX / HTML rendering with update-in-place (Cowork side panel, etc.). Render once at Stage 1 and update incrementally through Stage 5.
2. **Re-render fallback** — surface supports inline rendering but cannot update artifacts in place. Re-render the full artifact at each stage transition.
3. **Markdown only** — surface does not support inline rendering. Skip the artifact; deliver stage-by-stage summaries in the conversation and assemble the final mission/values doc as markdown at Stage 5.

Render this as a **persistent side-panel artifact**, not as a wall of inline content the user has to scroll past. Use the host's artifact mechanism (whatever it is on the current surface).

---

## Stage 1: Prerequisite Check

### Prerequisite Search Protocol

Before any user interaction, search for the user's prior work:

1. **Check the current project / workspace.** If running inside a Cowork project or a connected workspace, search the project's knowledge base, files, and prior conversations for: completed Personal Ikigai documents (founder + any team members), and completed Pre-PMF Executive Summary documents.

2. **Check connected connectors.** If any of the following are available, offer to search them:
   - `~~knowledge base` — for prior Ikigai work, executive summaries, mission/values drafts, prior strategy docs
   - `~~cloud storage` — for stored Ikigai documents, executive summary exports, founder bios

3. **Track what you found** before any user-facing message:
   - Founder Ikigai: present / missing
   - Team member Ikigais: list names if multiple
   - Executive Summary: present / missing
   - Key data extractable: Ikigai center statement, Mission intersection, What the World Needs, What You Love; Problem statement, Solution description, Vision, Target customer

### Branch Logic: Both Prerequisites Found

If BOTH Personal Ikigai AND Pre-PMF Executive Summary are found:

> *"I found your completed Personal Ikigai and Pre-PMF Executive Summary. Before we define your mission and values, let me confirm I have the right context:*
>
> ***From Your Ikigai:***
> *- Ikigai Center: [ikigai center statement]*
> *- Your Mission Zone: [mission intersection synthesis]*
> *- What the World Needs: [top 2–3 items]*
>
> ***From Your Executive Summary:***
> *- Problem You Solve: [quantified problem statement]*
> *- Your Solution: [solution description]*
> *- Vision: [closing vision statement if present]*
>
> ***Team Ikigais Found:** [Yes/No — list names if yes]*
>
> *Does this look correct? Any updates before we proceed?"*

If user confirms: proceed to Stage 2.

If user wants updates: *"Let's update that first. What's changed?"* → Capture updates → Re-confirm → Proceed.

### Branch Logic: Personal Ikigai Missing

If Personal Ikigai is missing:

> *"Before we define your company's mission and values, I need to understand who you are as a founder.*
>
> *I don't see a completed Personal Ikigai. Your Ikigai — the intersection of what you love, what you're good at, what you can be paid for, and what the world needs — is the foundation for an authentic mission statement.*
>
> ***Recommended next step:** Complete your Personal Ikigai first. It takes about 60–90 minutes and will make your mission and values much stronger. The `personal-ikigai` skill in this kit will guide you through it.*
>
> *You have three options:*
>
> *1. Run `personal-ikigai` first (recommended)*
> *2. Paste a prior Ikigai you've already done elsewhere*
> *3. Proceed without it — I can create a more generic mission/values approach, but it won't be as authentic*
>
> *Which do you want?"*

If user picks (1): hand off to `personal-ikigai` skill in this plugin.
If user picks (2): incorporate the pasted content and proceed.
If user picks (3): proceed but flag during synthesis that founder-fit signals will be weaker.

### Branch Logic: Executive Summary Missing

If Executive Summary is missing (Personal Ikigai may or may not be present):

> *"I [found your completed Personal Ikigai. However, I] don't see a completed Pre-PMF Executive Summary for your company.*
>
> *Your Executive Summary contains the problem you're solving, your solution, and your market — all essential inputs for a mission statement that's specific to your business, not just your personal values.*
>
> *You have three options:*
>
> *1. Run `pre-pmf-executive-summary` first (recommended) — about 60–90 minutes*
> *2. Give me a quick verbal summary of your company (problem, solution, target customer) and we'll proceed with that lighter context*
> *3. Paste a prior executive summary or business plan you've already written*
>
> *Which do you want?"*

If user picks (1): hand off to `pre-pmf-executive-summary` skill in this plugin.
If user picks (2): capture the quick context, confirm it back, proceed to Stage 2 with explicit acknowledgment that the mission may need refinement once a fuller executive summary exists.
If user picks (3): incorporate and proceed.

### Branch Logic: Both Missing

If BOTH Personal Ikigai and Executive Summary are missing:

> *"To create an authentic mission statement and values, I need two pieces of context:*
>
> *1. **Your Personal Ikigai** — Who you are as a founder, what drives you, what the world needs from you*
> *2. **Your Pre-PMF Executive Summary** — What your company does, the problem you solve, who you serve*
>
> *I don't see either of these completed yet.*
>
> ***Recommended path:***
>
> *1. Start with `personal-ikigai` (60–90 min)*
> *2. Then complete `pre-pmf-executive-summary` (60–90 min)*
> *3. Return here for Mission & Values (20–30 min)*
>
> *This sequence ensures your company identity is built on a solid foundation. Both skills are in this same plugin (`pre-pmf-starter`).*
>
> *Which would you like to start with — your Ikigai or your Executive Summary?"*

### Branch Logic: Multiple Team Ikigais Found

If multiple team member Ikigais exist:

> *"I found Ikigais for multiple team members:*
>
> ***[Founder 1 Name]:** [One-sentence Ikigai summary — e.g. "Driven by democratizing access to technology for underserved small business owners through systematic, scalable solutions."]*
>
> ***[Founder 2 Name]:** [One-sentence Ikigai summary]*
>
> ***[Founder 3 Name]:** [One-sentence Ikigai summary — if applicable]*
>
> *This is valuable — your company values should reflect your founding team's shared beliefs, not just one person's perspective.*
>
> *I'll analyze themes across all Ikigais to find where your team naturally aligns. The mission statement will focus on company direction from your Executive Summary, but informed by the team's collective 'why.'*
>
> *Ready to proceed?"*

Update the side-panel artifact (see [visualization.md](./visualization.md)) at the start of Stage 1 to show prerequisites status. Mark Stage 1 → complete and Stage 2 → in_progress at the end of Stage 1.

---

## Stage 2: Context Synthesis (Internal Analysis)

Before generating mission/values suggestions, perform systematic analysis across all inputs. **This analysis is internal — not shown to the user.** It populates the artifact's Inputs tab.

### Step 2A: Individual Ikigai Theme Extraction

For each team member's Ikigai, extract themes using:

**Word clustering:**

- Group semantically similar words/phrases across all four Ikigai circles
- Identify recurring concepts (e.g. "transparency," "access," "efficiency," "empowerment")
- Note frequency and placement (appears in Love AND Good At = stronger signal)

**Sentiment analysis:**

- Identify emotionally charged language in "What You Love" and "What the World Needs"
- Flag passion indicators: superlatives, personal stories
- Note frustration / pain language that indicates deeply felt problems

**Output per team member:**

- Primary drivers: top 3 themes by frequency / intensity
- Emotional anchors: what energizes them most
- Problem sensitivity: what frustrates them most
- Unique angle: themes that appear only for this person

### Step 2B: Cross-Team Correlation Analysis

If multiple team Ikigais exist, build a theme overlap matrix:

| Theme | Founder 1 | Founder 2 | Founder 3 | Correlation Strength |
| ----- | ----- | ----- | ----- | ----- |
| [Theme A] | ✓ (Love, Mission) | ✓ (Good At) | ✓ (World Needs) | **Strong** |
| [Theme B] | ✓ (Love) | ✓ (Love, Vocation) | — | Moderate |
| [Theme C] | ✓ (Profession) | — | ✓ (Paid For) | Moderate |
| [Theme D] | ✓ (Love) | — | — | Weak (individual) |

Identify:

- **Shared core themes:** appear across 2+ founders in high-signal areas (Love, Mission, Ikigai Center)
- **Complementary themes:** different founders bring different strengths that combine well
- **Potential tensions:** themes that might conflict between founders (flag for values discussion)

### Step 2C: Executive Summary Correlation

Map team themes to business context:

| Team Theme | Executive Summary Connection | Strength |
| ----- | ----- | ----- |
| [Shared Theme A] | Directly reflected in Problem Statement | **Strong** |
| [Shared Theme B] | Implicit in Solution approach | Moderate |
| [Shared Theme C] | Aligns with Target Customer needs | Moderate |
| [Individual Theme D] | Not reflected in current positioning | Gap |

Identify:

- **Mission candidates:** themes that are BOTH deeply personal to founders AND central to business value prop
- **Values candidates:** themes that reflect HOW the team operates, not just WHAT they're building
- **Alignment gaps:** personal themes not reflected in business (explore if business should evolve OR if theme is personal-only)

### Step 2D: Synthesis Output (Internal Reference)

**Mission Statement Inputs:**

- Strongest correlated theme between team Ikigais and Exec Summary problem/solution
- Emotional language from founder "What You Love" sections
- Specificity from Exec Summary (target customer, quantified problem)

**Values Candidates Ranked by:**

1. **Team correlation strength** — appears across multiple founders
2. **Behavioral evidence** — founders demonstrated this, not just stated it
3. **Business relevance** — connects to how the company should operate
4. **Differentiation potential** — not generic; specific to this team

**Flag for Discussion:**

- Themes with high individual passion but low team correlation
- Potential value conflicts between founders
- Gaps between personal drivers and business positioning

**Synthesis Checklist (before proceeding):**

- Team Ikigai Summaries: one-sentence per founder
- Shared Themes: ranked list with correlation strength
- Mission Candidates: 3 directions with theme backing
- Values Candidates: 10 options with source attribution
- Alignment Score: Strong / Moderate / Weak
- Discussion Flags: any tensions or gaps to explore

**Only proceed to Stage 3 when synthesis is complete.**

Update the side-panel artifact's Inputs tab with the team theme matrix and mission/values candidate lists, then mark Stage 2 → complete and Stage 3 → in_progress.

---

## Stage 3: Mission Statement Development

### Introduction

> *"Let's start with your mission statement.*
>
> *A strong mission statement answers: **Why does this company exist beyond making money?***
>
> *It should be:*
>
> *- **Specific** enough to guide decisions (not generic platitudes)*
> *- **Ambitious** enough to inspire (but grounded in reality)*
> *- **Authentic** to who you are as founders (connected to your Ikigai)*
> *- **Actionable** for your team (they can use it to prioritize)*
>
> *Based on your Ikigai and Executive Summary, I've drafted three mission statement options. Each takes a slightly different angle."*

### Generated Mission Options

Render the three options into the artifact's Mission tab and present in the conversation:

> *"Here are three mission statement drafts for [Company Name]:*
>
> *---*
>
> ***Option A: Problem-Centered***
> *"[Company Name] exists to [solve specific problem] for [target customer] by [unique approach]."*
>
> *[1–2 sentence rationale: how this connects to their Ikigai's 'What the World Needs' and Executive Summary problem statement]*
>
> *---*
>
> ***Option B: Impact-Centered***
> *"[Company Name]'s mission is to [desired world change/impact] through [method/approach]."*
>
> *[1–2 sentence rationale: how this connects to their Ikigai's Mission intersection and vision]*
>
> *---*
>
> ***Option C: Customer-Centered***
> *"We [action verb] [target customer] to [outcome they achieve] so they can [higher-order benefit]."*
>
> *[1–2 sentence rationale: how this connects to their Ikigai's 'What You Love' and business model]*
>
> *---*
>
> ***Initial reaction:** Which of these resonates most with you? Or is there an element from each that feels right?"*

### Refinement Loop

**If user picks one option:** *"Noted. What specifically drew you to Option [X]? And is there anything about the wording you'd change?"*

**If user likes elements from multiple:** *"Let me combine those elements. How about: '[New synthesized mission statement]'. Does this capture it better?"*

**If user dislikes all options:** *"Fair enough. These didn't land. Help me understand what's missing: Is it too generic? Too narrow? Does it not reflect what actually drives you? Is there a word or phrase that feels off? What would you want it to say, even roughly?"*

**If user's reaction feels performative:** *"Before we lock this in — imagine reading this mission statement to your team on a hard day when everyone's questioning why they're here. Does this actually answer that question for you?"*

Update the artifact's Mission tab with each iteration so the refinement history is visible.

### Mission Statement Refinement Questions

| Issue | Probe |
| ----- | ----- |
| Too generic | "Could a competitor say this same thing? What makes YOUR approach unique?" |
| Too narrow | "Does this still work if you expand to adjacent markets or products?" |
| Missing emotion | "What's the feeling you want someone to have when they read this?" |
| Too long | "If you had to cut this in half, what's the essential core?" |
| Jargon-heavy | "How would you explain this to someone outside your industry?" |
| Not actionable | "How would an employee use this to make a decision?" |

### Mission Statement Confirmation

> *"Here's your refined mission statement:*
>
> ***[Company Name] Mission:***
> *"[Final mission statement]"*
>
> *Before we move to values, I want to make sure this feels right. Read it out loud once.*
>
> *Does it:*
>
> *- ✅ Feel authentic to why you started this company?*
> *- ✅ Differentiate you from competitors?*
> *- ✅ Give your team a north star for decisions?*
>
> *Ready to lock this in and move to values? Or do you want to refine further?"*

**Confirmation required before proceeding.** Once confirmed, mark the mission as locked in the artifact (turquoise border / checkmark per [visualization.md](./visualization.md)) and mark Stage 3 → complete, Stage 4 → in_progress.

---

## Stage 4: Core Values Discovery

### Introduction to Values

> *"Now let's define your core values.*
>
> *Company values should be:*
>
> *- **Behaviors, not aspirations** — things you actually do, not things you wish you did*
> *- **Differentiating** — not generic (every company claims 'integrity')*
> *- **Memorable** — 3–7 values max, or no one remembers them (same number of digits as a phone number)*
> *- **Actionable** — you can hire, fire, and make decisions based on them*
>
> *Based on your Ikigai[s] and how you've described your company, I've identified 10 potential values. We'll narrow these down to your core 3–7."*

### Generated Values List (10 Options)

Render the 10 values into the artifact's Values tab and present in the conversation:

> *"Here are 10 values that emerged from your Ikigai and Executive Summary:*
>
> *| # | Value | Source | What It Means in Practice |*
> *| ----- | ----- | ----- | ----- |*
> *| 1 | **[Value 1]** | [From: Ikigai 'What You Love' / Exec Summary / etc.] | [Specific behavior example] |*
> *| 2 | **[Value 2]** | [Source] | [Behavior example] |*
> *| ... | ... | ... | ... |*
> *| 10 | **[Value 10]** | [Source] | [Behavior example] |*
>
> ***First pass:** Looking at this list, which 2–3 values feel most essentially you — the ones you'd never compromise on even if it cost you money or growth?"*

### Values Elimination Process

**Round 1: Identify must-haves (10 → ~5–6)**

> *"You identified [values they selected] as non-negotiables.*
>
> *Now let's eliminate. Looking at the remaining values, which ones are:*
>
> *- Nice-to-have but not essential?*
> *- Things you aspire to but don't consistently practice yet?*
> *- Generic enough that they don't actually guide decisions?*
>
> *Which 3–4 values can we cut?"*

**Probe if user struggles:** *"Let me put it differently: if a candidate was exceptional but clearly didn't embody [Value X], would you still hire them? If yes, it's probably not a core value."*

In the artifact, mark eliminated values with the deep red treatment per [visualization.md](./visualization.md).

**Round 2: Pressure test remaining values (~5–6 → 4–7)**

> *"We're down to [X] values. Let's pressure test each one:*
>
> ***[Value 1]:** Can you give me a specific example of when you or your team demonstrated this value? Especially when it was hard or costly to do so?"*

[Repeat for each remaining value]

**Authenticity check:** *"Any of these feel more aspirational than real? It's better to have fewer authentic values than more aspirational ones."*

**Round 3: Final prioritization (remaining → 3–7 ranked)**

> *"Almost there. Here are your remaining values:*
>
> *1. [Value A]*
> *2. [Value B]*
> *3. [Value C]*
> *4. [Value D]*
> *5. [Value E] (if applicable)*
>
> *Last question: if you could only keep THREE of these — the absolute core — which would they be?*
>
> *This doesn't mean the others don't matter. But which three would you put on your wall, in your job postings, and reference in every all-hands?"*

### Values Definitions

> *"Let's make these values actionable. For each core value, we need:*
>
> *- A clear definition (1–2 sentences)*
> *- What it looks like in practice (specific behaviors)*
> *- What it does NOT mean (common misinterpretations)*
>
> *Let's start with **[Value 1]**:*
>
> *Here's my suggested definition:*
> *"[Value 1]: [Draft definition based on context]"*
>
> ***In practice:** [Behavior example]*
> ***Does NOT mean:** [Clarification]*
>
> *How does this land? Anything you'd adjust?"*

[Repeat for each core value]

### Values Confirmation

> *"Here are your finalized core values:*
>
> *---*
>
> ***[Company Name] Core Values***
>
> ***1. [Value 1]***
> *[Definition]*
> *- In practice: [Behavior]*
> *- Does not mean: [Clarification]*
>
> ***2. [Value 2]***
> *[Definition]*
> *- In practice: [Behavior]*
> *- Does not mean: [Clarification]*
>
> ***3. [Value 3]***
> *[Definition]*
> *- In practice: [Behavior]*
> *- Does not mean: [Clarification]*
>
> *[**4. [Value 4]** — if applicable, through **7. [Value 7]**]*
>
> *---*
>
> *Do these feel like values you could:*
>
> *- Hire and fire based on?*
> *- Reference in difficult decisions?*
> *- Proudly share with customers and investors?*
>
> *Ready to finalize?"*

**Confirmation required before proceeding.**

### Optional: Values Deep-Dive Review

After values are confirmed, offer a final review pass:

> *"Before we lock these in for export — would you like to walk through each value and review what it is and what it is not? This is a chance to tighten the 'in practice' and 'does not mean' descriptions so they're crisp enough to use in hiring and decision-making."*

If user agrees: walk through each value one at a time. For each, present:

- **[Value Name]**
- **What it IS:** [Current "in practice" description]
- **What it is NOT:** [Current "does not mean" description]
- *"Anything you'd sharpen, add, or cut?"*

Iterate on each value before moving to the next. Update the side-panel artifact as changes are confirmed.

If user declines: proceed directly to Stage 5.

This step is optional but recommended — especially for teams with 5+ values where the "does not mean" boundary matters for consistency.

Mark Stage 4 → complete, Stage 5 → in_progress.

---

## Stage 5: Final Output

### Completion Summary

> *"Here's your complete company identity:*
>
> *---*
>
> *## [Company Name] — Mission & Values*
>
> *### Our Mission*
> *"[Final mission statement]"*
>
> *### Our Core Values*
>
> ***1. [Value 1]:** [Definition]*
>
> ***2. [Value 2]:** [Definition]*
>
> ***3. [Value 3]:** [Definition]*
>
> *[Additional values if applicable]*
>
> *---*
>
> *Would you like me to export this? I'll check which tools are connected and recommend the best destination."*

**Note:** the exported document contains ONLY the mission statement and core values with definitions. Do not include alignment checks, next steps, or session metadata in the export — those are session artifacts, not company documents. Next steps and follow-up actions belong in the conversation, not the document.

### Export Destinations

Check which connectors are available and recommend:

- **`~~knowledge base` connected** (Notion, Confluence, etc.) → publish Mission & Values as a page (linkable from onboarding, hiring, all-hands).
- **`~~cloud storage` connected** (Box, Egnyte, Drive, etc.) → save as a document.
- **Neither connected** → generate as a downloadable file (markdown, or `.docx` if a docx skill is available).

**Do not push anything to external tools until the user confirms both content and destination.**

Mark Stage 5 → complete (all stages turquoise / locked) on the artifact.

---

## Recommended Next Steps in This Kit

After completing your mission and values, the natural next step in the **pre-pmf-starter** kit is:

**`okr-workflow-pre-pmf`** — translate your mission and values into quarterly OKRs oriented toward discovering product-market fit.

Ask the user: *"Ready to move on to OKRs, or would you like to pause here?"*

**Invocation behavior on the user's response.** When the user affirms — even loosely, even alongside other tasks like *"save this first"* or *"sure, but let me also..."* — invoke `okr-workflow-pre-pmf` immediately via the Skill tool. Do not ask a second confirmation question. If the user's reply references existing material the next skill produces — *"we already have OKRs from last quarter"*, *"we have goals written down somewhere"*, *"may have most of what we need"* — invoke `okr-workflow-pre-pmf` with the referenced artifact as the baseline (grading + refresh path). Treat the prior recommendation + a domain-relevant response as a single invocation signal, not two separate decisions.

When invoking, pass through:

- Company name
- Mission statement
- Core values (with definitions)
- Linkages back to Ikigai and Executive Summary

If user wants to pause, offer a clean exit with mission and values exported and a clear path back.

---

## Clarifying Question Patterns

### When Mission Statement Feedback Is Vague

- *"What specifically feels off about it?"*
- *"Is it the words, or what it's saying?"*
- *"What would make it feel more 'you'?"*

### When Values Selection Is Difficult

- *"If you had to bet your company on one value, which would it be?"*
- *"Which of these would you defend even if an investor pushed back?"*
- *"What value would you be embarrassed NOT to have?"*

### When User Rushes Through

- *"These decisions will guide hundreds of future decisions. Worth taking an extra few minutes."*
- *"Would you hire someone who doesn't share these values? If you hesitated, we should discuss."*

### When Values Feel Generic

- *"Every company says they value [X]. What makes YOUR version different?"*
- *"How would someone know you live this value just by watching your team for a day?"*

---

## Common Pitfalls to Avoid

- Accepting the first draft without iteration
- Letting users keep more than 7 values (they won't remember them)
- Generic values like "integrity," "excellence," "innovation" without specific definition
- Mission statements that could apply to any company in the space
- Skipping the prerequisite check and creating shallow outputs
- Not connecting values back to founder Ikigai (feels imposed vs. authentic)
- Values that are aspirational but not currently practiced

---

## Session Success Indicators

- Mission statement is specific to THIS company (not generic)
- Values reduced to 3–7 (not 8–10)
- Each value has clear behavioral definition
- User can articulate why each value matters to them personally
- Clear connection to Ikigai visible in outputs
- User expresses confidence in using these for decisions
