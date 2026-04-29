---
name: personal-ikigai
description: Guide a person through a personal Ikigai discovery process — surface what they love, what they are good at, what they can be paid for, and what the world needs, then synthesize the four intersections (Passion, Profession, Mission, Vocation) into a personal Ikigai statement. Use when someone wants to clarify personal alignment with their role or work, articulate what they uniquely bring to a team or network, or surface their strengths and purpose. Output renders as a Figma or Miro board if those connectors are available, otherwise as an inline four-circle diagram or a clean markdown summary that can be exported to Word.
---

# Personal Ikigai Guide

**Purpose:** Guide a person through a personal Ikigai discovery process to surface their unique alignment of passion, skill, market value, and purpose.
**Duration:** 60–90 minutes
**Prerequisites:** None — works for anyone, with or without prior reflection on these themes
**Output:** Completed Ikigai framework with all four circles, four intersections, and a center synthesis statement

---

## When to Use This Skill

- User wants to explore personal alignment with their role or work
- User asks about Ikigai, personal purpose, or "what should I focus on?"
- User is onboarding into a team or network and wants to articulate what they uniquely bring
- User mentions keywords like "Ikigai", "alignment", "purpose", "passion", "what am I good at", "where should I focus my energy"
- User wants to understand the connection between their strengths, the market, and what they care about

---

## Prerequisite Search Protocol

Before beginning, see if there is existing context that could enrich the session. See [CONNECTORS.md](../../CONNECTORS.md) for the placeholder-to-server mapping used below.

1. **Check the current project or workspace.** If running inside a Cowork project or a connected workspace, search the project's knowledge base, files, and prior conversations for related Ikigai work, personal development notes, or role descriptions.

2. **Check connected connectors.** If any of the following are available, offer to search them for prior context:
   - `~~knowledge base` — for prior Ikigai sessions, personal development docs, journals
   - `~~cloud storage` — for personal bios, prior assessments, reflection notes

3. **Ask the user directly.** Whether or not anything turned up, ask: "Have you done an Ikigai (or similar) reflection before? If so, would you like to share notes or paste anything to start from?"

4. **Use what you find to accelerate, not replace.** Prior context can speed up sections where the user has already articulated passions, skills, or purpose — but never skip sections entirely. The value is in the in-session reflection, not just the final output.

If nothing is connected and the user has no prior context, just begin from Stage 1.

---

## Use Cases

- Someone joining a new team, network, or expert community and wanting to articulate their unique contribution
- A person exploring personal alignment with their existing role
- Someone seeking clarity on where to focus their energy and skills
- Anyone wanting a structured framework to surface their unique combination of strengths, interests, and purpose

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

**One section at a time.** Focus only on the current section. Do not jump ahead. If the user shares information relevant to a future section, acknowledge it — "Noted, I'll bring that back when we get there" — then return to the current section.

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

When the framework is complete, render it visually for the user. Default to **inline rendering** so the user stays in the conversation, then offer design-tool export as a follow-up.

1. **Inline rendering (default).** If the surface supports JSX/HTML rendering in a side panel (e.g. Cowork), render the four-circle Ikigai diagram as SVG or a CSS Venn so the user sees the structure live alongside the conversation.
2. **Markdown summary (fallback).** If inline rendering is not supported, generate a clean, structured markdown document with all four circles, four intersections, and the center synthesis. Offer to export as a Word document for a portable file.
3. **Design-tool export (optional follow-up).** After the inline or markdown version lands, ask: *"Want me to also save this to a Figma board (or Canva, Miro) so you have a persistent, editable copy you can share?"* If the user says yes and a `~~design tool` connector is available, render it there.

Hierarchy: live in the conversation first, persistent design board second. Do not lead with a design-tool render — it interrupts the moment with auth and board-creation friction.

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

And at the center of all four is your **Ikigai** — your sweet spot where what you uniquely bring meets what the world wants.

Ready to begin?"

---

## Stage 2: Four Core Sections

### Section 2A: What You LOVE

"Let's start with what you love. What activities, topics, or types of work make you lose track of time? Things you'd do even if no one paid you.

Take 2–3 minutes to think about this. There are no wrong answers."

**Target:** 3–7 items. If fewer than 3, gently probe for more. If more than 7, help refine to the most important ones.

**Clarifying questions when answers are vague:**

| Vague Response | Clarifying Probe |
| ----- | ----- |
| "I love helping people" | "Can you give me a specific example? What kind of help, and in what context?" |
| "I like technology" | "What specifically about technology? Building it? Teaching it? Analyzing trends?" |
| "I enjoy problem-solving" | "What types of problems? Technical? People problems? Strategic?" |
| "I'm passionate about my field" | "What aspect of it? The doing? The teaching? The mentoring? The systemic change?" |

**Depth check:** If responses feel surface-level: "Can you think of one more thing? Or tell me about a time recently when you felt really energized by something you were doing."

**Confirmation (only when all items collected):**

"Here's what I captured for 'What You Love':

- [Item 1]
- [Item 2]
- [Item 3]

Would you add or change anything, or is this list correct?"

On confirmation, acknowledge and move on.

---

### Section 2B: What You Are GOOD AT

"Now let's look at what you're good at. What skills, talents, or competencies have you developed over time? Think about what others consistently come to you for, or what you've been recognized for professionally.

Take a few minutes."

**Alternative probing question** (if user struggles or gives generic answers): "Let me ask it differently — if I asked your closest colleague what you're truly good at, what would they say?"

**Note:** This section covers ALL skills and talents — not just professionally paid ones. The market reality test comes in Section 2C.

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

---

### Section 2C: What You Can Be PAID FOR

"Next: what you can be paid for. This is about market reality. What skills or expertise do you have that people or companies actually pay for? Think about your career history, consulting work, or services you could offer tomorrow if needed.

What comes to mind?"

**Clarifying questions:**

| Vague Response | Clarifying Probe |
| ----- | ----- |
| "My experience" | "Experience in what specifically? What would someone hire you for tomorrow?" |
| "Consulting" | "Consulting on what topic? Who would be your buyer?" |
| "Leadership" | "Leadership in what domain? What size company or team would pay for this?" |
| "I could teach" | "Teach what subject? To whom — individuals, companies, students?" |

**Market reality check:** "Have you actually been paid for these things before, or is this more theoretical?"

**Buyer specificity check:** "For each of these — who specifically pays for it? Early-stage founders, growth-stage companies, enterprises, individuals?"

**Confirmation (only when all items collected):**

"Here's what I captured for 'What You Can Be Paid For':

- [Item 1]
- [Item 2]
- [Item 3]

Does this feel accurate?"

---

### Section 2D: What The World NEEDS

"Now the bigger picture: what the world needs. What problems do you see that deserve to be solved? Where do you see inefficiency, suffering, or missed opportunity that frustrates you? This can be global or within a specific industry or community you know well."

**Clarifying questions:**

| Vague Response | Clarifying Probe |
| ----- | ----- |
| "Better healthcare" | "What specifically about healthcare? Access? Cost? Quality? For whom?" |
| "Sustainability" | "Which aspect? Energy? Waste? Consumer behavior? Supply chains?" |
| "Education needs fixing" | "What part of education? K-12? Higher ed? Professional training? What's broken?" |
| "Small businesses struggle" | "With what specifically? Finding customers? Operations? Financing? Hiring?" |

**Personal connection probe:** "Of these problems, which ones do you feel *personally connected to*? Which have you experienced firsthand or seen up close?"

**Confirmation (only when all items collected):**

"Here's what I captured for 'What the World Needs':

- [Need 1]
- [Need 2]
- [Need 3]

Anything else?"

---

## Stage 3: Four Intersection Sections

**Note:** The user can see all four core circles from Stage 2 in their notes or rendered board. Do NOT restate these full lists in the intersection sections. Only provide synthesis statements.

### Section 3A: PASSION (Love + Good At)

"Now let's look at the intersections, starting with your Passion. Passion sits at the overlap of what you love and what you're good at."

Based on the overlap between "What You Love" and "What You're Good At," propose 1–3 synthesis statements (5–15 words each):

"Based on what you've shared, here's what I see for your Passion zone:

1. **[Synthesis statement 1]** — [Brief explanation of how love + skill connect]
2. **[Synthesis statement 2]** — [Brief explanation]

Do these feel accurate, or would you change anything?"

On confirmation, acknowledge and move on.

---

### Section 3B: PROFESSION (Good At + Paid For)

"Next is Profession — where what you're good at meets what you can be paid for. This is your professional sweet spot — skills the market values."

Propose 1–3 Profession statements (5–15 words each) that connect skills with market value. Focus on realistic, market-aligned roles or services.

Present, refine, confirm.

---

### Section 3C: MISSION (Love + Needs)

"Now Mission — where what you love meets what the world needs. This is about purpose — causes you care about that also matter."

Propose 1–3 Mission statements (5–15 words each).

Present, refine, confirm.

---

### Section 3D: VOCATION (Needs + Paid For)

"Finally, Vocation — where what the world needs meets what you can be paid for. This is about viable impact — solving real problems in a sustainable way."

Propose 1–3 Vocation statements (5–15 words each).

Present, refine, confirm.

---

## Stage 4: Ikigai Center Synthesis

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

**Refinement loop:** If user offers adjustments, incorporate and re-confirm: "Let me try again: [Updated synthesis]. Does this land better?"

On confirmation, acknowledge and move on.

---

## Stage 5: Final Summary & Render

### Completion Summary

"Here's what we've built:

**Your Ikigai Framework**

- **What You Love:** [items]
- **What You're Good At:** [items]
- **What You Can Be Paid For:** [items]
- **What the World Needs:** [items]
- **Passion:** [synthesis]
- **Mission:** [synthesis]
- **Profession:** [synthesis]
- **Vocation:** [synthesis]
- **Your Ikigai:** [center statement]"

### Render the Output

Apply the Visualization & Final Output section above:

1. Default to inline rendering if the surface supports it (side panel JSX/HTML).
2. Otherwise generate a markdown summary, with optional Word export.
3. After the user has the visual, ask if they want a persistent copy in a `~~design tool` (Figma, Canva, Miro) for sharing or later editing.

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
- User expresses clarity or "aha" moments
- Final Ikigai statement resonates and is articulable in 1–2 sentences

## Common Pitfalls to Avoid

- Accepting vague answers without probing
- Rushing through sections
- Forcing alignment where it doesn't exist
- Over-explaining Ikigai theory instead of facilitating discovery
- Summarizing lists before asking questions (summarize only once at confirmation)
- Asking "Are you sure?" after the user has already confirmed
- Repeating confirmed items unnecessarily
