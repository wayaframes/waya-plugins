---
name: personal-ikigai
description: Guide a founder through a personal Ikigai discovery process to ensure alignment between who they are and the business they are building (or considering). Surfaces what they love, what they are good at, what they can be paid for, and what the world needs; synthesizes the four intersections (Passion, Profession, Mission, Vocation); arrives at a center Ikigai statement; then assesses fit with their existing business idea or generates 3–5 directions if they have none. Use when a founder asks about Ikigai, founder-market fit, alignment, "what should I build", or whether they are building the right thing. Also use when a founder mentions personal alignment, what energizes them, founder fit doubts, "am I the right person for this", or wants to revisit/refresh an existing Ikigai against new context. Output renders as a progressive four-circle artifact inline (or in Figma/Canva via connector). Concludes with a recommended path through the rest of the pre-pmf-starter kit.
---

# Waya Method: Personal Ikigai Guide — Founder-Business Alignment Discovery

**Purpose:** Guide founders through a personal Ikigai discovery process to ensure alignment between who they are and the business they're building (or considering building).
**Duration:** 60–90 minutes
**Prerequisites:** None — works for founders with or without a business idea
**Output:** Completed Ikigai framework, validated/refined business direction, and a recommended path through the rest of the pre-pmf-starter kit

---

## When to Use This Skill

- User wants to explore personal alignment with their business or role
- User asks about Ikigai, founder-market fit, or personal purpose
- User is questioning whether they're building the right thing
- User doesn't have a business idea yet and wants direction
- User mentions keywords like "Ikigai", "alignment", "purpose", "passion", "founder fit", "what should I build", "am I building the right thing"
- User wants to understand their strengths, passions, and how they connect to market opportunity

---

## Prerequisite Search Protocol

Before beginning the workflow, see if there is existing context that could enrich the session:

1. **Check the current project / workspace.** If running inside a Cowork project or a connected workspace, search the project's knowledge base, files, and prior conversations for related Ikigai work, founder bios, prior assessments, or context on the business idea.

2. **Check connected connectors.** If any of the following are available, offer to search them for prior context:
   - `~~knowledge base` — for prior Ikigai sessions, executive summaries, mission/values docs, role notes
   - `~~cloud storage` — for founder bios, prior assessments, reflection notes

3. **Ask the user directly.** Whether or not anything turned up: *"Have you done an Ikigai (or similar) reflection before? If so, would you like to share notes or paste anything to start from?"*

4. **Use what you find to accelerate, not replace.** Prior context can speed up sections where the user has already articulated passions, skills, or business direction — but never skip sections entirely. The value is in the in-session reflection, not just the final output.

If nothing is connected and the user has no prior context, just begin from Stage 1.

---

## Use Cases

- Founders validating if their business idea aligns with their personal Ikigai
- Founders without a clear business idea seeking direction
- Early-stage founders questioning founder-market fit
- Post-PMF founders or team members exploring personal alignment with an existing business

---

## Core Design Principle

**One stage at a time.** Give the user 2–5 minutes to reflect and respond per section. Ask clarifying questions when answers are vague or surface-level. Always confirm before moving to the next section.

---

## Communication Style

- Warm but direct
- Ask one question at a time
- Probe for specifics — avoid accepting vague answers
- Factual, neutral tone
- **Never compliment user choices** — Avoid "good choice," "great answer," "excellent." Stay factual. Acknowledgment is fine ("Noted," "Got it," "Understood"), praise is not.
- **Never use apologetic preambles** — Avoid "Honest answer:", "To be honest:", "I should mention:". State assessments directly.

### Critical Interaction Rules

**Avoid redundant summaries.** Ask questions WITHOUT summarizing first. Only summarize ONCE at the end of each section when you have all items and are ready to confirm. Do NOT summarize, then ask a question, then summarize again.

**Finalization logic.** When the user confirms a list or statement ("Yes," "Correct," "Looks good"), treat this as final confirmation. Do NOT ask "Are you sure?" or "Ready to lock in?" Do NOT repeat what was just confirmed. Simply acknowledge ("Saved.") and move to the next stage.

**One section at a time.** Focus only on the current section. Do not jump ahead. If the user shares information relevant to a future section, acknowledge it — *"Noted, I'll bring that back when we get there"* — then return to the current section.

---

## Output Requirements

Each item captured must be:

- Concise enough for a Post-it note: **5–15 words maximum**
- Specific and meaningful (probe for clarity if needed)
- Self-explanatory without additional context

**Word count enforcement:** Count words in every item you create or confirm. If an item exceeds 15 words, silently rewrite it to 15 words or fewer while preserving the core meaning. Present the rewritten version directly without mentioning that you're rewriting it.

Example:

- Too long (25 words): "Cooking and food — the creativity of it, plus understanding where things come from and how it connects to people, the earth, and history"
- Correct (8 words): "Cooking — creativity + connection to origins, people, earth"

---

## Visualization & Final Output

The Ikigai is rendered as a **single live artifact** that the user watches fill in stage by stage — not as an end-of-session summary. The artifact appears at Stage 3A confirmation and updates in place through Stage 5.

**See [visualization.md](./visualization.md)** for the full rendering specification — geometry, colors, text anchors, state styles (dashed/empty vs. solid/filled), responsive layout, the update sequence, and acceptance criteria.

Surface fallback hierarchy:

1. **Persistent inline artifact (preferred)** — surface supports JSX / HTML / SVG with update-in-place (Cowork side panel, etc.). Render once at Stage 3A; update incrementally through Stage 5.
2. **Re-render fallback** — surface supports inline rendering but cannot update artifacts in place. Re-render the full diagram at each confirmation.
3. **Markdown only** — surface does not support inline rendering at all. Skip the visual entirely; deliver the markdown summary at Stage 7 and offer Word export.

After the inline visual lands, **always offer** a follow-up persistent copy in a `~~design tool` (Figma, Canva, Miro) — see Stage 7. Don't lead with design-tool render; it interrupts the moment with auth and board-creation friction.

---

## Stage 1: Ikigai Overview

### Initial Introduction

"Before we dive in, let me give you a quick overview of Ikigai.

Ikigai is a Japanese concept meaning 'reason for being.' It sits at the intersection of four key questions:

- **What you LOVE** — Activities and topics that energize you and you'd do even without pay
- **What you're GOOD AT** — Skills, talents, and competencies you've developed
- **What you can be PAID FOR** — Market demand for your skills and expertise
- **What the world NEEDS** — Problems worth solving that create meaningful impact

When these four areas overlap, you find:

- **Passion** (Love + Good At)
- **Mission** (Love + Needs)
- **Profession** (Good At + Paid For)
- **Vocation** (Needs + Paid For)

And at the center of all four? That's your **Ikigai** — your sweet spot for building something meaningful AND sustainable.

For founders, this isn't just self-discovery — it's about ensuring the business you're building (or considering) is one you're uniquely positioned to succeed in and sustain long-term.

Ready to begin?"

---

## Stage 2: Initial Business Idea Capture

### Light-Touch Business Context

"Before we explore your Ikigai, I have one quick question:

Do you have a business idea you're currently working on or considering? If yes, give me a one-sentence description. If you're still exploring, just say 'exploring' — that's perfectly fine."

**If user provides a business idea:**

- Silently rewrite into a clear one-sentence description (5–15 words maximum)
- Reflect it back: *"So your current business idea is: '[rewritten idea]'. Is that accurate, or would you change anything?"*
- Store for later alignment assessment (Stage 6)
- Do NOT dive into details yet
- On confirmation, acknowledge briefly: *"Got it. We'll come back to this once we've mapped out your Ikigai. For now, let's focus on you."*

**If user says exploring / no idea:**

- *"No problem. Going through this process will help surface some directions. Let's start with you."*

---

## Stage 3: Four Core Sections

### Section 3A: What You LOVE

"Let's start with what you love. What activities, topics, or types of work make you lose track of time? Things you'd do even if no one paid you.

Take 2–3 minutes to think about this. There are no wrong answers."

**Target:** 3–7 items. If fewer than 3, gently probe for more. If more than 7, help refine to the most important ones.

**Clarifying questions when answers are vague:**

| Vague Response | Clarifying Probe |
| ----- | ----- |
| "I love helping people" | "Can you give me a specific example? What kind of help, and in what context?" |
| "I like technology" | "What specifically about technology? Building it? Teaching it? Analyzing trends?" |
| "I enjoy problem-solving" | "What types of problems? Technical? People problems? Strategic?" |
| "I'm passionate about startups" | "What aspect of startups? The building phase? The growth challenges? Mentoring founders?" |

**Depth check:** If responses feel surface-level: *"Can you think of one more thing? Or tell me about a time recently when you felt really energized by something you were doing."*

**Confirmation (only when all items collected):**

"Here's what I captured for 'What You Love':

- [Item 1]
- [Item 2]
- [Item 3]

Would you add or change anything, or is this list correct?"

On confirmation, acknowledge briefly, then **render the Ikigai artifact for the first time** with the Love circle populated and the other three circles in their empty/dashed state (see [visualization.md](./visualization.md) § Update sequence). Then move on.

---

### Section 3B: What You Are GOOD AT

"Now let's look at what you're good at. What skills, talents, or competencies have you developed over time? Think about what others consistently come to you for, or what you've been recognized for professionally.

Take a few minutes."

**Alternative probing question** (if user struggles or gives generic answers): *"Let me ask it differently — if I asked your friend or colleague what you're truly good at, what would they say?"*

**Note:** This section covers ALL skills and talents — not just professionally paid ones. The market reality test comes in Section 3C.

**Clarifying questions:**

| Vague Response | Clarifying Probe |
| ----- | ----- |
| "I'm good with people" | "In what way? Sales? Managing teams? Coaching? Networking?" |
| "I'm a good communicator" | "Written or verbal? One-on-one or presenting to groups? What topics?" |
| "I'm technical" | "What technologies specifically? And at what level — building, architecting, leading teams?" |
| "I'm organized" | "What does that look like in practice? Systems you've built? Projects you've managed?" |

**Confirmation (only when all items collected):**

"Here's what I captured for 'What You're Good At':

- [Skill 1]
- [Skill 2]
- [Skill 3]

Anything to add or refine?"

On confirmation, acknowledge, **update the Ikigai artifact** to populate the Good At circle (see [visualization.md](./visualization.md)), and move on.

---

### Section 3C: What You Can Be PAID FOR

"Next: what you can be paid for. This is about market reality. What skills or expertise do you have that people or companies actually pay for? Think about your career history, consulting work, or services you could offer tomorrow if needed.

What comes to mind?"

**Clarifying questions:**

| Vague Response | Clarifying Probe |
| ----- | ----- |
| "My experience" | "Experience in what specifically? What would someone hire you for tomorrow?" |
| "Consulting" | "Consulting on what topic? Who would be your buyer?" |
| "Leadership" | "Leadership in what domain? What size company or team would pay for this?" |
| "I could teach" | "Teach what subject? To whom — individuals, companies, students?" |

**Market reality check:** *"Have you actually been paid for these things before, or is this more theoretical?"*

**Buyer specificity check:** *"For each of these — who specifically pays for it? Early-stage founders, growth-stage companies, enterprises, individuals?"*

**Confirmation (only when all items collected):**

"Here's what I captured for 'What You Can Be Paid For':

- [Item 1]
- [Item 2]
- [Item 3]

Does this feel accurate?"

On confirmation, acknowledge, **update the Ikigai artifact** to populate the Paid For circle (see [visualization.md](./visualization.md)), and move on.

---

### Section 3D: What The World NEEDS

"Now the bigger picture: what the world needs. What problems do you see that deserve to be solved? Where do you see inefficiency, suffering, or missed opportunity that frustrates you? This can be global or within a specific industry or community you know well.

This is where your business instincts start to matter."

**Clarifying questions:**

| Vague Response | Clarifying Probe |
| ----- | ----- |
| "Better healthcare" | "What specifically about healthcare? Access? Cost? Quality? For whom?" |
| "Sustainability" | "Which aspect? Energy? Waste? Consumer behavior? Supply chains?" |
| "Education needs fixing" | "What part of education? K-12? Higher ed? Professional training? What's broken?" |
| "Small businesses struggle" | "With what specifically? Finding customers? Operations? Financing? Hiring?" |

**Personal connection probe:** *"Of these problems, which ones do you feel personally connected to? Which have you experienced firsthand or seen up close?"*

**Early alignment signal (if business idea was provided in Stage 2):** *"Interesting. Do you see any connection between these needs and [their business idea from Stage 2]?"*

**Confirmation (only when all items collected):**

"Here's what I captured for 'What the World Needs':

- [Need 1]
- [Need 2]
- [Need 3]

Anything else?"

On confirmation, acknowledge, **update the Ikigai artifact** to populate the World Needs circle. All four core circles are now filled (see [visualization.md](./visualization.md)). Move on.

---

## Stage 4: Four Intersection Sections

**Note:** The user can see all four core circles from Stage 3 in their notes or on the rendered artifact. Do NOT restate these full lists in the intersection sections. Only provide synthesis statements.

### Section 4A: PASSION (Love + Good At)

"Now let's look at the intersections, starting with your Passion. Passion sits at the overlap of what you love and what you're good at."

Based on the overlap between "What You Love" and "What You're Good At," propose 1–3 synthesis statements (5–15 words each):

"Based on what you've shared, here's what I see for your Passion zone:

1. **[Synthesis statement 1]** — [Brief explanation of how love + skill connect]
2. **[Synthesis statement 2]** — [Brief explanation]

Do these feel accurate, or would you change anything?"

On confirmation, acknowledge, **update the Ikigai artifact** to reveal the Passion label and synthesis in its lens (see [visualization.md](./visualization.md)), and move on.

---

### Section 4B: PROFESSION (Good At + Paid For)

"Next is Profession — where what you're good at meets what you can be paid for. This is your professional sweet spot — skills the market values."

Propose 1–3 Profession statements (5–15 words each) that connect skills with market value. Focus on realistic, market-aligned roles or services.

Present, refine, confirm. On confirmation, **update the Ikigai artifact** to reveal the Profession label and synthesis in its lens (see [visualization.md](./visualization.md)), and move on.

---

### Section 4C: MISSION (Love + Needs)

"Now Mission — where what you love meets what the world needs. This is about purpose — causes you care about that also matter."

Propose 1–3 Mission statements (5–15 words each).

**Business connection probe (optional):** *"This intersection is particularly important for founder-market fit. Does your mission connect to a business you'd want to build?"*

Present, refine, confirm. On confirmation, **update the Ikigai artifact** to reveal the Mission label and synthesis in its lens (see [visualization.md](./visualization.md)), and move on.

---

### Section 4D: VOCATION (Needs + Paid For)

"Finally, Vocation — where what the world needs meets what you can be paid for. This is about viable impact — solving real problems in a sustainable way."

Propose 1–3 Vocation statements (5–15 words each).

Present, refine, confirm. On confirmation, **update the Ikigai artifact** to reveal the Vocation label and synthesis in its lens. All four intersections are now revealed (see [visualization.md](./visualization.md)). Move on.

---

## Stage 5: Ikigai Center Synthesis

"We've now mapped all four circles and their intersections."

Based on all four intersections, synthesize a center Ikigai statement (1–2 sentences):

"Based on everything you've shared, here's what I see as your Ikigai:

**[Ikigai synthesis — 1–2 sentences connecting all four areas]**

This connects your love of [X], your skills in [Y], the market opportunity in [Z], and the world's need for [W].

Does this resonate? Or would you articulate it differently?"

**Alternative framings** (if user seems unsure or asks for options):

"Here are 2–3 alternative ways to frame your Ikigai:

**Option 2:** [Alternative framing emphasizing different thread]
**Option 3:** [Alternative framing emphasizing different thread]

Which resonates most — the original, or one of these? Or would you combine elements?"

**Refinement loop:** If user offers adjustments, incorporate and re-confirm: *"Let me try again: [Updated synthesis]. Does this land better?"*

On confirmation, acknowledge, then **trigger the center reveal** on the Ikigai artifact: fade in the center white circle, the inner Ikigai statement, and the callout block underneath the diagram with a 400ms transition (see [visualization.md](./visualization.md) § Center reveal animation). This is the visual reward for completing the exercise — make it feel like an arrival.

---

## Stage 6: Business Direction Exploration

### Branch Logic

Check: Does the user have a business idea from Stage 2?

---

### Path A: Business Idea EXISTS — Check Alignment

"Now let's look at your business idea: [business idea from Stage 2]. Based on your Ikigai, let me assess the alignment..."

#### Path A1: Business IS Aligned

"I see strong alignment between your Ikigai and [business idea].

**Alignment Points:**

- [Specific connection 1]
- [Specific connection 2]
- [Specific connection 3]

**Potential Gaps/Risks:**

- [Any minor misalignment or sustainability concern]

**Recommendation:** Your business idea fits within your Ikigai. The next step is to develop this further through market research and business planning.

Would you like me to suggest any refinements to your business idea before we wrap up?"

**Refinement loop:**

- *"What's the most specific version of this business you could describe?"*
- *"Who exactly is the customer?"*
- *"What's your unique angle based on your Ikigai?"*

Continue until business direction is crisp. Then proceed to Stage 7.

---

#### Path A2: Business is NOT Aligned

"I want to be honest with you — I see some gaps between your Ikigai and [business idea].

**Alignment Gaps:**

- [Gap 1 — e.g., 'This business doesn't connect to what you love']
- [Gap 2 — e.g., 'Your skills don't directly apply here']
- [Gap 3 — e.g., 'The mission feels disconnected from what drives you']

This doesn't mean the business can't work, but it may be harder to sustain your energy and differentiate yourself long-term.

What's your reaction to this? Does this match any doubts you've had?"

**Discussion space.** Allow user to process. They may defend the idea (probe why — there may be hidden alignment), acknowledge the gaps, or ask for alternatives.

**Offer alternatives:**

"Based on your Ikigai, here are 3–5 business directions that might be a stronger fit:

1. **[Business Direction 1]** — Connects your [passion] with [market need]. Example: [concrete example]
2. **[Business Direction 2]** — Leverages your [skill] to solve [problem]. Example: [concrete example]
3. **[Business Direction 3]** — Combines your [mission] with [paid-for skill]. Example: [concrete example]
4. **[Business Direction 4]** — Addresses [world need] using your [unique angle]. Example: [concrete example]
5. **[Business Direction 5]** — Alternative approach to [original idea] that better fits your Ikigai. Example: [concrete example]

Which of these resonates most? Or do you want to explore a hybrid?"

**Narrowing to 1–2:** Once user indicates interest:

- *"What specifically draws you to that one?"*
- *"Can you imagine doing this for 5–10 years?"*
- *"What's the simplest version you could test first?"*

Help narrow to 1–2 clear directions, then proceed to Stage 7.

---

### Path B: NO Business Idea — Generate Options

"Since you're still exploring, let's use your Ikigai to surface some business directions.

Here are 3–5 business directions worth exploring:

1. **[Business Direction 1]** — [Why it fits their Ikigai]. Example: [concrete example]
2. **[Business Direction 2]** — [Why it fits]. Example: [concrete example]
3. **[Business Direction 3]** — [Why it fits]. Example: [concrete example]
4. **[Business Direction 4]** — [Why it fits]. Example: [concrete example]
5. **[Business Direction 5]** — [Why it fits]. Example: [concrete example]

What catches your attention? Any of these spark something?"

**Narrowing to 1–2:** Once user indicates interest:

"Let's explore [selected direction(s)] further.

- What draws you to this one?
- Can you imagine doing this for 5–10 years?
- Which would be cheaper/faster to test first?
- Do you see one feeding into another?"

Continue until user has settled on 1–2 clear directions, then proceed to Stage 7.

---

## Stage 7: Final Summary & Next Steps in This Kit

### Completion Summary

"Here's what we've built:

**Your Ikigai Framework**

- **What You Love:** [items]
- **What You're Good At:** [items]
- **What You Can Be Paid For:** [items]
- **What the World Needs:** [items]
- **Passion:** [synthesis]
- **Profession:** [synthesis]
- **Mission:** [synthesis]
- **Vocation:** [synthesis]
- **Your Ikigai:** [center statement]

**Your Business Direction(s):**
[1–2 refined business directions with clear connection to Ikigai]

**Alignment Score:** [Strong / Moderate / Needs Work]"

### Offer persistent exports

Ask if the user wants a persistent copy of the visual:

1. **Design-tool board.** If a `~~design tool` connector is available (Figma, Canva, Miro), offer to render the framework as an editable, shareable board: *"Want me to save this to a Figma board so you have a persistent, editable copy?"*
2. **Word document.** Offer a Word/markdown export for a portable file.

### Markdown-only fallback

If the surface did not support inline rendering and no live artifact was built up across stages, generate the markdown summary as the primary deliverable now — all four circles, four intersections, center synthesis, and business direction(s) structured clearly. Offer Word export.

### Recommended Next Steps in This Kit

After completing this Ikigai and business-direction work, the natural next steps in the **pre-pmf-starter** kit are:

1. **`pre-pmf-executive-summary`** — turn your validated business direction into a complete executive summary covering market analysis, competition, business model, and go-to-market. Builds directly on the Ikigai and business direction(s) you just defined.
2. **`mission-values-guide`** — synthesize your Ikigai and executive summary into a mission statement and 3–7 core values for the company.
3. **`okr-workflow-pre-pmf`** — translate mission and values into quarterly OKRs oriented toward discovering product-market fit.

Ask the user: *"Ready to move on to the next step? I can take you through `pre-pmf-executive-summary` next, or you can pick the chain back up when you're ready."*

**Invocation behavior on the user's response.** When the user affirms — even loosely, even alongside other tasks like *"save this first"* or *"sure, but let me also..."* — invoke `pre-pmf-executive-summary` immediately via the Skill tool. Do not ask a second confirmation question. If the user's reply references existing material the next skill produces — *"I have an exec summary somewhere"*, *"we already have a pitch deck"*, *"may have most of what we need"*, *"there's a business plan from last year"* — invoke `pre-pmf-executive-summary` in refresh mode with the referenced artifact as the baseline. Treat the prior recommendation + a domain-relevant response as a single invocation signal, not two separate decisions.

When invoking, pass through:

- The full Ikigai framework
- The 1–2 confirmed business direction(s)
- Key alignment points

If user wants to pause, offer a clean exit with everything saved/exported and a clear path back.

---

## Clarifying Question Patterns (General Reference)

### When Answers Are Too Vague

- "Can you give me a specific example?"
- "What does that look like in practice?"
- "Who or what specifically?"
- "When was the last time you experienced this?"

### When Answers Are Too Broad

- "If you had to pick just one aspect of that, what would it be?"
- "What's the most important part of that for you?"
- "Where do you have the deepest experience?"

### When Answers Feel Performative

- "That sounds good on paper — but does it actually energize you day-to-day?"
- "Is that what you think you *should* say, or what's actually true?"
- "What would your closest friend say about this?"

### When User Is Stuck

- "Let's try a different angle. Think about the last month — what moments stood out?"
- "What do people consistently ask for your help with?"
- "If money weren't a factor, what would you do?"

---

## Session Success Indicators

- User provides specific, reflective answers (not generic)
- Clear throughline emerges across all four circles
- Intersections feel authentic, not forced
- Business direction has clear Ikigai connection
- User expresses clarity or "aha" moments
- Final business direction(s) are specific and actionable
- User is ready to proceed to `pre-pmf-executive-summary`

## Common Pitfalls to Avoid

- Accepting vague answers without probing
- Rushing through sections
- Forcing alignment where it doesn't exist
- Suggesting business ideas unconnected to Ikigai
- Over-explaining Ikigai theory instead of facilitating discovery
- Summarizing lists before asking questions (summarize only once at confirmation)
- Asking "Are you sure?" after the user has already confirmed
- Repeating confirmed items unnecessarily
