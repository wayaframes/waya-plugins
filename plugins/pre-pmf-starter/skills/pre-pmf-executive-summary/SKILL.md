---
name: pre-pmf-executive-summary
description: Guide an early-stage founder through creating a pre-seed/seed executive summary covering problem hypothesis, solution and customer discovery, market opportunity (TAM/SAM/SOM with citations), business model and pricing, validation plan, team and founder-market fit, and the ask. Builds on prior Personal Ikigai work if available, otherwise offers to run that first. Use when a founder is exploring an idea, doing customer discovery or market research, has a prototype but no paying customers, or needs to crystallize their plan for early fundraising. Also use when a founder mentions refreshing, updating, reviewing, or revising an existing executive summary; when they have one "somewhere" that needs a pass; when they want to align an exec summary with new traction, a strategy shift, or recent learnings; or when they reference existing pitch material that needs to be brought current. NOT for founders with proven traction, ARR, or growth metrics — that case wants a post-PMF executive summary instead. Output is a one-page pre-PMF executive summary plus a progressive 7-section progress bar artifact tracking completion through the session.
---

# Waya Method: Pre-PMF Executive Summary

## When to Use This Skill

**Use when:**
- Founder is exploring an idea or doing market research
- Founder has a prototype but no paying customers yet
- Founder is conducting user testing or customer discovery
- Founder needs help crystallizing their business plan for early fundraising (pre-seed / seed)

**Do NOT use when:**
- Founder has proven traction, revenue, or paying customers
- Founder is raising Series A or later
- Founder mentions ARR, growth rates, retention metrics, or unit economics with real data

In those cases, recommend a post-PMF executive summary approach instead.

**Trigger conditions:**
- User explicitly asks for help with a pre-seed/seed executive summary
- User describes an idea they're exploring or validating
- User mentions customer discovery, prototyping, or early-stage fundraising
- Workflow detection identifies pre-PMF executive summary intent

---

## Purpose & Scope

This skill walks early-stage founders (idea exploration, market validation, prototype stage) through crystallizing their business idea, conducting market research with citations, and creating the first outline of their business plan. From this foundation, founders can decide whether to proceed with validation or pivot.

**Target users:** founders exploring an idea, doing market research to validate it, or with a prototype conducting user testing. Not for founders with proven traction or revenue.

---

## Prerequisite Search Protocol

Before starting, see if there is existing context that could enrich the session:

1. **Check the current project / workspace.** If running inside a Cowork project or a connected workspace, search the project's knowledge base, files, and prior conversations for: prior Personal Ikigai work, prior business plans or pitch decks, founder bios, customer interview notes, market research, and pricing/competitive notes.

2. **Check connected connectors.** If any of the following are available, offer to search them:
   - `~~knowledge base` — for prior Ikigai work, mission/values docs, OKR history, customer interview notes
   - `~~cloud storage` — for founder bios, prior pitch decks, market research, customer feedback documents

3. **Ask the user directly.** Whether or not anything turned up: *"Have you done any prior work on this — Ikigai, business plan, market research, customer interviews — that you'd like me to incorporate?"*

4. **Use what you find to accelerate, not replace.** Prior context can pre-fill sections and reduce redundant questioning, but the value is still in the in-session articulation — never skip sections.

---

## Personal Ikigai Status Check

Before starting Section 1, decide how to handle Personal Ikigai context:

**If Ikigai context was found** (in project knowledge or via connectors): silently use it. Reference it specifically when discussing founder-market fit in Section 1 (the "why YOU" question) and Section 6 (Team & Why You). Do not ask the user about it — they already did the work.

**If Ikigai context was NOT found**, prompt the user before starting Section 1:

> *"Quick check before we dive in: I don't see any Personal Ikigai work in your context. Personal Ikigai is the natural starting point in this kit — it informs founder-market fit (Section 1) and team/why-you (Section 6) here. You have three options:*
>
> *1. Run Personal Ikigai first (recommended) — about 60–90 minutes, then come back to this with the output ready.*
> *2. Proceed without it — we'll address founder fit organically through the questions below, and you can come back to Ikigai later if you want.*
> *3. You've already done one elsewhere — paste it here and I'll incorporate it.*
>
> *Which do you want?"*

If user picks (1): hand off to the `personal-ikigai` skill in this plugin. After they complete it and return, restart this skill — the prerequisite search will now find their Ikigai output.

If user picks (2): proceed to Section 1. Founder-fit questions will be answered organically.

If user picks (3): incorporate the pasted content into context and proceed to Section 1.

---

## Building Process

### Progressive Questioning Approach

Build executive summaries through structured, iterative questioning that educates, collaborates, and helps founders articulate their vision clearly.

#### Core Principles

1. **Start each section by stating the expected outputs.**
2. **ABSOLUTE RULE — ONE QUESTION PER RESPONSE. NO EXCEPTIONS.** Each response must contain exactly ONE question mark — the single question you are asking. After processing the user's answer, you may provide a brief reflection or challenge, then ask exactly ONE next question. Before sending any response, count the question marks. If there is more than one, delete all but the one you most need answered. This rule overrides any other instruction in this skill that might imply asking multiple questions (e.g., section introductions that list multiple expected outputs should NOT be phrased as questions). If you encounter instructions elsewhere in this skill that appear to require multiple questions in one response, follow THIS rule instead — ask only the first question and save the rest for subsequent turns.

   **SUB-QUESTION HANDLING.** When a high-level question naturally leads to clarifying sub-questions (e.g., "Who is your target customer?" followed by "What stage?", "What revenue range?", "What industry?"), you MUST still present only one question at a time. When asking the high-level question, briefly inform the user that you will have follow-up questions to drill deeper — but do NOT list or display the sub-questions. Ask the high-level question alone, wait for the answer, then ask each sub-question one at a time in subsequent turns based on what the user's answer did or did not cover.
3. **Be collaborative and educational** — most pre-PMF founders need guidance.
4. **Help with research when needed** (market sizing, comparables).
5. **All research must include citations with links.**
6. **Track progress via the visual Progress Bar artifact** (see [visualization.md](./visualization.md)).
7. **Be factual and direct** — avoid compliments like "great answer" or "nice work." Keep probing for specificity when answers are vague or broad.

### Research Citation Requirements

**CRITICAL.** When providing market data, benchmarks, or "typical" ranges:

- **Always** include citations with clickable links to sources.
- If no research exists or can be found, explicitly state: *"This is an illustrative example, not a researched benchmark."*
- Never present assumptions as industry standards without qualification.
- When searching yields examples but not systematic research, say: *"I found examples showing X, but no systematic research on typical ranges."*

---

## Critical Section Flow Control

**Mandatory.** Complete sections sequentially while intelligently capturing all shared information.

1. **Sequential completion.** You MUST formally complete each section before moving to the next.
   - When you have all required fields for the current section, announce *"Section [N] Complete:"*
   - ONLY THEN introduce the next section.
   - **When transitioning sections:** state the section summary, update the progress bar artifact (see [visualization.md](./visualization.md)), introduce the next section's expected outputs, then ask exactly ONE opening question. Do NOT bundle the summary with multiple questions.

2. **Opportunistic data collection.** When users provide information relevant to future sections:
   - Acknowledge and store it: *"Got it, I've noted your pricing hypothesis for the business model section."*
   - Return to the current section: *"Now, back to your problem hypothesis..."*
   - Use the stored information when you reach that section.

3. **Smart context usage.** You always know:
   - Which section you're currently completing
   - What information you've already collected for future sections
   - What's still needed for the current section

---

## Visualization & Final Output

The skill renders a **single live progress bar artifact** — 7 sections, vertically stacked, each with a status (not_started / in_progress / complete). The user watches it fill in over the session.

**See [visualization.md](./visualization.md)** for the full rendering specification — Waya brand color palette, layout rules, behavioral rules (only one section in_progress at a time, completed sections collapsed by default but click-to-expand, etc.), the per-section field data model, the update sequence, and acceptance criteria.

Surface fallback hierarchy:

1. **Persistent inline artifact (preferred)** — surface supports JSX / HTML / SVG with update-in-place (Cowork side panel, etc.). Render once after the first question is answered; update incrementally at each section transition.
2. **Re-render fallback** — surface supports inline rendering but cannot update artifacts in place. Re-render the full progress bar at each section transition.
3. **Markdown only** — surface does not support inline rendering at all. Skip the progress bar artifact; deliver section completion summaries as plain text and assemble the final executive summary as markdown at Section 7.

---

## Section 1: Company Overview & Problem Hypothesis

**Section objective:** establish the problem you're solving, why you personally care about it, and early evidence the problem is real.

**Expected outputs:**

- Clear problem hypothesis with specificity
- Personal connection to the problem (founder-market fit / Ikigai alignment)
- Early validation that this problem exists and matters
- Target customer definition

### Question Flow

**Question 1.** Let's start with the basics: do you have a company name yet? What problem are you trying to solve? And if you have a name, what's the meaning behind it?

*Understanding: company identity (optional), core problem hypothesis, and the founder's intent/vision embedded in naming.*

*Note: company name is optional. If no name, acknowledge and focus on the problem.*

**Challenge approach (after Question 1):**

- State intention first: *"That's broad — I want to understand exactly who feels this pain and how much it costs them."*
- Then ask ONE specific follow-up: *"What type of founders or executives are you targeting — early-stage, growth-stage, or enterprise?"*
- Wait for answer before asking next clarifying question.
- For quantification: ask the user *"How would YOU quantify this problem?"* rather than pushing for specific numbers.
- Pre-PMF companies may not have precise data — help them think through quantification approaches, not demand exact figures.

**Question 2.** Why are YOU pursuing this problem?

*Understanding: personal connection and founder-market fit.*

**Ikigai integration:**

- If Ikigai context exists: *"I see from your Ikigai work that [reference specific findings — e.g., your Mission of X and your Vocation in Y]. How does that connect to this problem?"*
- If no Ikigai context: listen for passion, skills, and market need alignment — and probe for any of the four Ikigai threads naturally as they come up.

**Question 3.** Who specifically experiences this problem?

*Understanding: target customer hypothesis — looking for specific persona, not "everyone."*

**Challenge approach.** If too broad ("small businesses"): *"Can you narrow that down? What type of small business? What size? What industry?"*

Push for: demographics, psychographics, behaviors, context when problem occurs.

**Question 4.** How do you know this problem exists?

*Understanding: evidence of problem validation — conversations, data, personal experience.*

**Challenge approach.**

- Push from "I think" to "I've learned."
- Ask for specific examples: *"How many people have you talked to? What did they say?"*
- Valid sources: customer interviews, surveys, industry data, personal experience in the domain.

**Question 5.** How severe is this problem for your target customer?

*Understanding: is this a "painkiller" or "vitamin"?*

**Framework:**

- **Painkiller** = urgent, frequent, costly problem customers actively seek solutions for
- **Vitamin** = nice-to-have improvement customers won't prioritize
- Push for evidence of severity: *"Would they pay to solve this today? Have they tried other solutions?"*

### Section 1 Completion Protocol

**Section 1 Complete:**

- **Company name:** [Name or "Not yet named"]
- **Name meaning:** [Story/intent behind the name, if provided]
- **Problem hypothesis:** [Core problem statement]
- **Founder connection:** [Why this founder, this problem]
- **Target customer:** [Specific persona]
- **Problem evidence:** [How they know it's real]
- **Problem severity:** [Painkiller/vitamin assessment]

Update the progress bar (see [visualization.md](./visualization.md)) to mark Section 1 complete and Section 2 in_progress before introducing Section 2.

**Section 1 checklist:**

- [ ] Problem is specific and quantifiable (even if estimated)
- [ ] Founder has personal connection or unique insight
- [ ] Target customer is clearly defined (not "everyone")
- [ ] Some evidence problem exists (conversations, data, experience)
- [ ] Problem appears to be "painkiller" not "vitamin"

---

## Section 2: Solution Hypothesis & Customer Discovery

**Section objective:** articulate what you're building, how it differs from existing solutions, and what you've learned from potential customers.

**Expected outputs:**

- Clear solution concept (even if prototype/MVP)
- Differentiation from existing alternatives
- Customer discovery insights that inform the approach

### Question Flow

**Question 1.** What are you building to solve this problem?

*Understanding: solution hypothesis — the product/service concept.*

**Question 2.** How do people currently solve this problem today?

*Understanding: existing alternatives and status quo.*

**Challenge approach.** If "nothing exists": push back — *"Really? How do they cope? What workarounds do they use?"*

The status quo is always a competitor (doing nothing, manual processes, spreadsheets, etc.).

**Question 3.** Why is your approach different or better than existing solutions?

*Understanding: differentiation hypothesis.*

**CRITICAL: Competitor Verification Protocol.** Before accepting uniqueness claims:

1. Search web for existing competitors / solutions.
2. Present findings with citations.
3. Then ask: *"Given these existing solutions, what specifically makes your approach different?"*

**Template:**

```
"Let me search for existing solutions in this space..."
[Web search results with links]
"I found [X, Y, Z] offering [specific features]. How does your approach differ from these?"
```

**Question 4.** Have you done any customer discovery yet — customer interviews, focus groups, surveys, or other validation tests?

*Understanding: whether customer discovery evidence exists.*

**If YES.** Proceed with customer discovery questions:

- *"What have you learned from talking to potential customers?"*
- *"What's the most surprising thing you learned?"*
- *"Any insights that challenged your initial assumptions?"*

**If NO.** Offer guidance:

> *"Customer discovery is critical at this stage — it helps validate that your solution resonates with real customers, not just your assumptions.*
>
> *Common customer discovery methods include:*
>
> *- 1-1 interviews (most valuable) — 15–30 min conversations with target customers*
> *- Focus groups — group discussions to surface shared pain points*
> *- Surveys — broader reach but less depth*
> *- Landing page tests — gauge interest before building*
> *- Prototype testing — show early concepts and gather feedback*
>
> *I can help you structure customer discovery hypotheses and a tight interview plan now if you want, or we can keep this section brief and you can return to it after this session."*

If they want to flesh it out now, walk them through structuring 3–5 hypothesis-driven interview questions with explicit success criteria.

### Section 2 Completion Protocol

**Section 2 Complete:**

- **Solution concept:** [What they're building]
- **Current alternatives:** [How problem is solved today]
- **Differentiation:** [Why their approach is better]
- **Customer discovery insights:** [What they've learned]
- **Key surprise/learning:** [Most important insight]

Update the progress bar (see [visualization.md](./visualization.md)) to mark Section 2 complete and Section 3 in_progress before introducing Section 3.

**Section 2 checklist:**

- [ ] Solution concept is clear and understandable
- [ ] Existing alternatives acknowledged (including status quo)
- [ ] Differentiation validated against actual competitors (web search done)
- [ ] Some customer discovery evidence exists
- [ ] Founder demonstrates learning / iteration from feedback

---

## Section 3: Market Opportunity

**Section objective:** understand the size and dynamics of your target market to inform go-to-market strategy and validate the business opportunity.

**Expected outputs:**

- Ideal Customer Profile (ICP) hypothesis
- TAM / SAM / SOM with credible methodology and sources
- Understanding of market dynamics
- "Why now" timing justification
- All market data backed by research with links

### SAM Segmentation Framework

SAM can be segmented by multiple dimensions:

1. **User type** — who they are (e.g. first-time founders, founders without business backgrounds)
2. **Geography** — where they are (e.g. US only, North America, global)
3. **Industry segment** — what they do (e.g. tech startups only, B2B SaaS, all industries)

All three dimensions should be explored to arrive at a realistic SAM.

### Opening Protocol

**Question 1.** Let's define your Ideal Customer Profile (ICP). Beyond the broad target you mentioned earlier, who is your *ideal* first customer? Think about: company stage, industry, team size, specific pain points, and any other characteristics that make them a perfect fit.

*Understanding: sharpening the target customer hypothesis for market sizing and go-to-market.*

**Question 2.** Have you already done market research, or would you like help researching your market size and opportunity?

*Understanding: starting point for market sizing.*

### Path A: User Has Done Research

**Question 2a.** What market size data have you found? Please share your sources.

*Understanding: validate their research quality.*

**Protocol:**

1. Review their numbers and sources.
2. Cross-reference with web search.
3. Validate or suggest adjustments.
4. Help refine TAM / SAM / SOM breakdown.

**Challenge approach.**

- *"Let me verify that data..."* [web search]
- *"Your TAM looks reasonable. How did you calculate your SAM from that?"*

**CRITICAL: Evaluate User Assumptions.** When users provide percentages or estimates for market sizing:

- If numbers seem too small (e.g. <1% of TAM as addressable): challenge with *"That seems conservative — let me check if that aligns with industry data..."*
- If numbers seem too large (e.g. >50% market capture): challenge with *"That's aggressive — what's your rationale for that penetration rate?"*
- Sanity check math: does the resulting number make sense given the opportunity?
- Ask clarifying questions: *"Is that 10% of the total, or 10% of a subset?"*

### Path B: User Needs Help

**Question 2b.** Let me help you research your market. Based on your target customer of [reference Section 1], I'll search for relevant market data.

*Understanding: collaborative market research.*

**Protocol:**

1. Conduct web search for market size data.
2. Present findings WITH LINKS TO SOURCES.
3. Explain methodology options (top-down vs. bottom-up).
4. Walk through TAM > SAM > SOM calculation together.

**Template:**

```
"Let me search for market data on [their space]..."
[Web search results]

Based on my research:
- [Source 1 with link]: [Finding]
- [Source 2 with link]: [Finding]

Here's how we might think about your market:
- TAM (Total Addressable Market): [calculation and source]
- SAM (Serviceable Addressable Market): [their segment]
- SOM (Serviceable Obtainable Market): [realistic capture in 3–5 years]
```

### Continued Questions (Both Paths)

**Question 3.** What's your initial geographic focus?

*Understanding: realistic starting point for market capture.*

**Question 4.** Are you targeting all industries, or specific sectors? For example: tech startups only, B2B vs. B2C, VC-backable vs. bootstrapped businesses, or specific verticals like healthcare or fintech?

*Understanding: industry segmentation to narrow SAM to realistic targets.*

*Note: this matters because broad market data (e.g. "5.2M new US businesses annually") includes restaurants, retail shops, contractors, etc. — many of which may not be the ICP even if they meet other criteria.*

**Question 5.** Why is NOW the right time for this solution?

*Understanding: market timing and trends.*

**Challenge approach.**

- Push for specific trends: technology shifts, regulatory changes, behavior changes, market events.
- If weak "why now": *"What's changed that makes this possible or necessary today vs. 5 years ago?"*

**Question 6.** What market trends support your timing?

*Understanding: external validation of timing hypothesis.*

**Offer to research if needed:** *"Would you like me to search for recent trends in [their space]?"*

### SOM Guidance

When helping users estimate SOM (Serviceable Obtainable Market), it should be based on realistic constraints, NOT arbitrary percentages. Guide users to think through:

1. **Sales / marketing capacity** — how many customers can you actually reach and serve?
2. **Budget constraints** — what's your customer acquisition budget?
3. **Competitive landscape** — who else is competing for these customers?
4. **Product readiness** — when will your product be ready for scale?

**IMPORTANT.** Do NOT provide "typical" SOM percentages (e.g. "startups typically capture 0.1–1% of SAM") unless you can cite specific research. Instead:

- Search for comparable company growth data in their industry.
- If no research found, say: *"I couldn't find systematic research on typical market capture rates. Let's build your SOM from the bottom up based on your specific constraints."*
- Use examples found in research but qualify them: *"One example I found: [Company X] captured [Y%] in their first year ([source link]), but this varies significantly by industry and business model."*

**Bottom-up SOM approach:**

```
"Let's calculate your SOM from the ground up:
- Year 1: How many customers do you realistically think you can acquire?
- What's your basis for that estimate? (sales capacity, marketing budget, conversion rates)
- Let's check: does that number make sense given your resources?"
```

### Section 3 Completion Protocol

**Section 3 Complete:**

- **ICP:** [Ideal customer profile description]
- **TAM:** [Number with source/link]
- **SAM:** [Number with methodology — including user type, geography, and industry segmentation]
- **SOM:** [Number with assumptions — based on realistic constraints]
- **Geographic focus:** [Initial market]
- **Industry focus:** [Target sectors or "all industries"]
- **Why now:** [Timing justification]
- **Supporting trends:** [Market dynamics]

Update the progress bar to mark Section 3 complete and Section 4 in_progress.

**Section 3 checklist:**

- [ ] ICP clearly defined (stage, industry, size, pain points)
- [ ] TAM backed by credible source with link
- [ ] SAM logically derived from TAM with clear segmentation (user type + geography + industry)
- [ ] SOM based on realistic constraints (not arbitrary percentages)
- [ ] Geographic focus clearly defined
- [ ] Industry segmentation addressed
- [ ] "Why now" has specific, compelling answer

**CRITICAL.** All market data must include citations with links.

---

## Section 4: Business Model Hypothesis

**Section objective:** show thoughtful approach to monetization with realistic comparables.

**Expected outputs:**

- Revenue model hypothesis (how will you charge?)
- Pricing hypothesis with rationale
- Acquisition channel hypothesis
- Basic unit economics understanding

### Question Flow

**Question 1.** How do you plan to make money?

*Understanding: revenue model hypothesis (subscription, transaction fee, licensing, etc.).*

**Question 2.** What do you plan to charge, and how did you arrive at that pricing?

*Understanding: pricing hypothesis and rationale.*

**Challenge approach.**

- If no rationale: *"What informed that price point? Customer feedback? Competitor pricing? Value delivered?"*
- Push for connection to customer discovery: *"Did you test this pricing in your conversations?"*

### Pricing Hypothesis Development Protocol

If user has no pricing hypothesis or willingness-to-pay research, when they respond to Question 2 with uncertainty (*"I don't know what to charge"* / *"Haven't figured out pricing yet"*), offer two paths:

**Path A — Skip for now.** *"That's okay — pricing often becomes clearer after willingness-to-pay conversations with potential customers. We can mark this as 'TBD' and you can return to it after more customer discovery. Want to move on?"*

**Path B — Develop hypothesis together.** *"Would you like me to help you develop a pricing hypothesis based on competitive research? I can benchmark similar solutions across multiple categories to help you find your positioning."*

If user chooses Path B, run lightweight competitive benchmarking:

**Step 1: Identify research categories.** Search across 3–5 relevant categories:

1. **Direct competitors** — same problem, same approach
2. **Adjacent solutions** — same problem, different approach
3. **Price anchors** — what your target customer already pays for similar value

Example categories for AI business tools:

- Direct: AI cofounder / startup assistant tools
- Adjacent: general AI assistants (ChatGPT, Claude)
- Upper bound: human services (fractional executives, consultants, coaches)
- Lower bound: self-serve tools or free alternatives

**Step 2: Search and present findings.**

```
"Let me research pricing across categories relevant to your solution..."
[Web search with citations]

"Here's what I found:

Category 1: [Direct Competitors]
| Product | Free Tier | Paid Tiers | Model |
|---------|-----------|------------|-------|
| [Name]  | [Free features] | [Price/mo] | [Subscription/credits/etc.] |

Category 2: [Adjacent Solutions]
...

Category 3: [Price Anchors — Upper Bound]
...

Sources: [links]
```

**Step 3: Identify gaps and positioning.** After presenting research, ask:

> *"Based on this landscape, where do you see your positioning?*
>
> *- Premium: higher than competitors because [unique value]*
> *- Competitive: similar to direct competitors*
> *- Penetration: lower to gain market share initially*
> *- New category: filling a gap between price tiers*
>
> *What's your instinct?"*

**Step 4: Document hypothesis.** Capture:

- Proposed price point or range
- Positioning rationale (premium / competitive / penetration)
- Key competitors used as reference
- Gaps identified in the market
- **Mark as "Hypothesis — requires WTP validation"**

**Competitive benchmarking quality checklist:**

- [ ] Searched 3+ relevant categories
- [ ] All findings include source links
- [ ] Identified pricing gaps in market
- [ ] User chose positioning rationale
- [ ] Hypothesis clearly marked as unvalidated

**CRITICAL.** Competitive benchmarks inform hypothesis only. Always recommend willingness-to-pay validation with actual customers before finalizing pricing.

**Question 3.** How do you plan to acquire customers?

*Understanding: acquisition channel hypothesis.*

**Prompt if needed:**

- Direct sales (outbound, enterprise)
- Online marketing (SEO, paid ads, content)
- Partnerships and referrals
- Community / word of mouth
- Product-led growth

**Then provide comparables.** After receiving the user's hypotheses, search for comparable business models:

```
"Now let me search for comparable business models in your space..."
[Web search]

"Here's what I found:
- [Company A] uses [model] and charges [pricing] — [link]
- [Company B] uses [model] and charges [pricing] — [link]

Your [pricing/model] is [higher/lower/similar]. Does this align with how you're
positioning (premium, competitive, penetration pricing)?"
```

### Unit Economics Education

**Question 4.** Let's talk about unit economics. Are you familiar with concepts like CAC, LTV, and payback period?

*Understanding: founder's financial sophistication.*

If they need education, explain:

> *"Let me walk you through the key unit economics concepts:*
>
> ***CAC** (Customer Acquisition Cost) — how much you spend to acquire one customer.*
> *- Includes: marketing, sales salaries, tools, etc.*
> *- Example: \$10,000 in ads / 10 customers = \$1,000 CAC*
>
> ***LTV** (Lifetime Value) — total revenue from a customer over their lifetime.*
> *- Formula: (Monthly Revenue × Gross Margin) / Monthly Churn Rate*
> *- Example: (\$100/month × 80% margin) / 5% churn = \$1,600 LTV*
>
> ***LTV:CAC ratio** — should be 3:1 or higher for healthy business.*
> *- \$1,600 LTV / \$200 CAC = 8:1 (excellent)*
>
> ***Payback period** — how long to recover CAC.*
> *- \$200 CAC / (\$100 × 80% margin) = 2.5 months*
>
> *At pre-PMF stage, these are hypotheses to validate, not proven numbers."*

**Question 5.** Based on your pricing of [X] and acquisition channel of [Y], what do you think your customer acquisition cost might be?

*Understanding: even rough estimates show thinking.*

**Question 6.** When do you expect to have your first paying customers?

*Understanding: timeline to revenue and validation.*

### Section 4 Completion Protocol

**Section 4 Complete:**

- **Revenue model:** [How they make money]
- **Pricing:** [What they charge and rationale] OR [Hypothesis based on competitive benchmarking — needs WTP validation]
- **Pricing positioning:** [Premium / Competitive / Penetration and why]
- **Competitive landscape:** [Key competitors and price points with sources]
- **Acquisition channel:** [How they'll get customers]
- **Unit economics hypothesis:** [CAC/LTV thinking, even if rough]
- **Timeline to revenue:** [When first paying customers expected]

Update the progress bar to mark Section 4 complete and Section 5 in_progress.

**Section 4 checklist:**

- [ ] Revenue model is clear and logical for the market
- [ ] Pricing has rationale (customer research OR competitive benchmarking)
- [ ] If competitive benchmarking used, hypothesis marked as "needs WTP validation"
- [ ] Pricing positioning clearly articulated (premium / competitive / penetration)
- [ ] Competitive landscape researched with source links
- [ ] Acquisition channel identified with reasoning
- [ ] Founder understands basic unit economics concepts
- [ ] Realistic timeline to first revenue

---

## Section 5: Validation Plan

**Section objective:** demonstrate clear, hypothesis-driven approach to learning and de-risking the business.

**Expected outputs:**

- Evidence of validation work already done
- Specific experiments planned
- Understanding of key risks and how you'll test them

### Opening Protocol

**Question 1.** What validation have you done so far? Please share 3 examples of how you've validated your idea.

*Understanding: evidence of validation work completed.*

**Valid validation examples:**

- 1-1 interviews with potential customers
- Focus group sessions
- Market surveys (with sample size)
- Prototype / MVP testing
- Landing page or ad tests
- Industry expert consultations
- Personal professional experience in the domain
- Pilot customers or letters of intent

### Expert Founder Path

If founder relies on professional background as domain expert:

> *"Your background in [domain] is strong validation for the problem. Since you have deep expertise here, let's focus your validation plan on:*
>
> *1. Solution validation — does your specific approach resonate?*
> *2. Channel validation — how will you reach customers?*
> *3. Pricing validation — will they pay what you're planning to charge?"*

### Standard Path

Cover all four validation categories:

1. Problem validation
2. Solution validation
3. Channel validation
4. Pricing validation

### Continued Questions

**Question 2.** What are your biggest unknowns or risks right now?

*Understanding: self-awareness about what needs to be proven.*

**Question 3.** What experiments do you plan to run in the next 90 days?

*Understanding: concrete validation plan.*

**Experiment types to prompt:**

- Customer interviews (1-1 or focus groups)
- Market surveys
- Landing page tests
- Prototype testing
- Pricing tests
- Channel experiments
- Pilot programs

**Question 4.** For each experiment, what would success look like?

*Understanding: clear success criteria.*

**Question 5.** What would make you pivot or abandon this idea?

*Understanding: intellectual honesty and kill criteria.*

### Optional: Tighten the Experiment Plan

After hearing their validation examples and plans, offer:

> *"I can help you tighten these experiments — structure each as a hypothesis-driven test with explicit success criteria, kill criteria, and a sample size. Want to do that now, or keep this section higher-level and pick that up in a follow-up session?"*

If they want to do it now, walk through 1–3 of the planned experiments and convert each into:

- **Hypothesis:** "We believe [X] because [Y]."
- **Test:** "We will test by [method, sample size]."
- **Success criteria:** "[N] of [Sample] respond [How] within [Timeframe]."
- **Kill criteria:** "If fewer than [N] respond, we [pivot/kill/redesign]."

### Section 5 Completion Protocol

**Section 5 Complete:**

- **Validation completed:** [3 examples provided]
- **Key risks identified:** [What needs to be proven]
- **90-day experiments:** [Planned validation activities]
- **Success criteria:** [How they'll measure]
- **Kill criteria:** [What would make them stop]

Update the progress bar to mark Section 5 complete and Section 6 in_progress.

**Section 5 checklist:**

- [ ] At least 3 validation examples provided
- [ ] Key risks / unknowns clearly identified
- [ ] Concrete experiments planned (not vague intentions)
- [ ] Success criteria defined for experiments
- [ ] Founder shows intellectual honesty about what could disprove the idea

---

## Section 6: Team & Why You

**Section objective:** build confidence in the founder(s)'s ability to execute this specific business.

**Expected outputs:**

- Founder-market fit demonstration
- Relevant skills and experience
- Commitment level and skin in the game
- Team gaps awareness and plan

*Note: "limited track record" refers to THIS BUSINESS being new. Founders may have significant experience from other ventures or careers.*

### Question Flow

**Question 1.** Why are YOU the right person to solve this problem?

*Understanding: unique insights, experiences, or skills that create founder-market fit.*

**Ikigai integration:**

- If Ikigai context exists: *"Your Ikigai work surfaced [reference specific findings — e.g., your Passion at the intersection of X and Y]. How does that inform why you're the right founder for this?"*
- If no Ikigai context: listen for passion, skills, market need alignment.

**Question 2.** What relevant experience do you bring to this venture?

*Understanding: background that supports execution ability.*

**Valid experience types:**

- Previous startup experience (founder or early employee)
- Industry / domain expertise
- Functional expertise (sales, engineering, marketing, operations)
- Academic or research background
- Personal experience with the problem

**Question 3.** What's your current commitment level?

*Understanding: skin in the game.*

**Options:**

- Full-time on this venture
- Transitioning (timeline?)
- Side project while employed
- Part-time with co-founder full-time

**Question 4.** Who else is on the team, and what gaps exist?

*Understanding: team composition and self-awareness.*

**Challenge approach.** If solo: *"What are the biggest skill gaps you'll need to fill? When do you plan to bring on co-founders or key hires?"* Push for honest gap assessment.

**Question 5.** What's your first critical hire?

*Understanding: prioritization and gap-filling strategy.*

### Section 6 Completion Protocol

**Section 6 Complete:**

- **Founder-market fit:** [Why this founder for this problem]
- **Relevant experience:** [Background supporting execution]
- **Commitment level:** [Full-time / transitioning / part-time]
- **Team composition:** [Current team members]
- **Key gaps:** [What's missing]
- **First hire:** [Priority recruitment]

Update the progress bar to mark Section 6 complete and Section 7 in_progress.

**Section 6 checklist:**

- [ ] Clear founder-market fit articulated
- [ ] Relevant experience identified (doesn't have to be startup)
- [ ] Commitment level is appropriate for stage
- [ ] Honest about team gaps
- [ ] Plan for addressing gaps

---

## Section 7: The Ask

**Section objective:** present specific, realistic funding request with clear use of funds OR help founder understand what it takes to reach PMF.

### Opening Protocol

**Question 1.** Are you planning to fundraise, or would you like help understanding how much money and time it typically takes to reach product-market fit?

*Understanding: founder's current fundraising readiness and needs.*

### Path A: Planning to Fundraise

**Question 2a.** How much are you raising?

*Understanding: funding target.*

**Calibration check:**

- Pre-seed typically: $50K – $500K
- Seed typically: $500K – $2M
- If outside range, ask about rationale.

**Question 3a.** What runway does this give you?

*Understanding: burn rate and timeline.*

**Question 4a.** How will you allocate these funds?

*Understanding: use of funds breakdown.*

**Typical pre-PMF allocation:**

- Product development: 40–50%
- Customer acquisition / validation: 20–30%
- Team / hiring: 20–30%
- Operations / overhead: 10–15%

**Question 5a.** What milestones will you achieve with this funding?

*Understanding: value creation plan.*

**Pre-PMF milestone examples:**

- Complete MVP and launch beta
- Achieve [X] validated users / customers
- Prove specific unit economics hypotheses
- Reach [specific validation milestone]
- Ready for seed / Series A raise

**Question 6a.** What will you be able to prove that you can't prove today?

*Understanding: learning milestones, not just business milestones.*

### Path B: Need Help Budgeting to PMF

Educational walkthrough:

> *"Let me help you think through what it typically takes to reach product-market fit:*
>
> ***Timeline:***
> *- Average time to PMF: 12–24 months*
> *- Some reach it in 6–12 months, others take 3+ years*
> *- Depends on: market complexity, sales cycle, product complexity*
>
> ***Typical pre-PMF burn rate:***
> *- Solo founder: \$5K–10K/month (minimal salary, tools, hosting)*
> *- 2-person team: \$15K–25K/month*
> *- Small team (3–5): \$40K–60K/month*
>
> ***Key costs to consider:***
> *- Founder salaries (or living expenses if no salary)*
> *- Product development (engineering, design)*
> *- Customer acquisition experiments*
> *- Tools and infrastructure*
> *- Legal and accounting basics*
>
> ***Runway recommendation:***
> *- Minimum: 12 months runway*
> *- Ideal: 18–24 months runway*
> *- Allows time for pivots and learning"*

**Question 2b.** Based on your team and plans, what do you think your monthly burn rate would be?

*Understanding: help them calculate needs.*

**Question 3b.** How many months of runway do you want before your next milestone?

*Understanding: timeline to validation.*

**Question 4b.** So you'd be looking at raising approximately $[calculated amount]. Does that feel right?

*Understanding: sanity check and alignment.*

**Question 5b.** What funding sources are you considering?

*Understanding: fundraising strategy.*

**Options to discuss:**

- Bootstrapping / self-funding
- Friends and family
- Angel investors
- Accelerators (Y Combinator, Techstars, etc.)
- Pre-seed funds
- Grants

### Section 7 Completion Protocol

**Section 7 Complete:**

- **Funding amount:** [Target raise]
- **Runway:** [Months of operation]
- **Use of funds:** [Allocation breakdown]
- **Key milestones:** [What funding achieves]
- **Validation outcomes:** [What they'll prove]

Update the progress bar to mark Section 7 complete (all sections now green and collapsed).

**Section 7 checklist:**

- [ ] Funding amount appropriate for stage
- [ ] Runway calculation makes sense
- [ ] Use of funds tied to validation plan
- [ ] Milestones are specific and measurable
- [ ] Focus on learning / validation, not just business metrics

---

## Final Deliverable: One-Page Executive Summary

After Section 7 completes, assemble the captured data into the one-page format below and deliver it as a markdown document. Offer Word/PDF export.

### Header

- Company name (or "Working name: X")
- Tagline / one-liner
- Founder name(s) and contact

### The Problem (1 paragraph)

- Specific problem with target customer
- Evidence of problem severity
- Current alternatives and their limitations

### The Solution (1 paragraph)

- What you're building
- Key differentiation
- Current stage (idea / prototype / MVP)

### Market Opportunity (3–4 bullets)

- TAM / SAM / SOM with sources
- Why now
- Initial target segment

### Business Model (2–3 bullets)

- Revenue model hypothesis
- Pricing approach
- Acquisition channel

### Validation & Traction (3–4 bullets)

- Customer discovery completed
- Key learnings
- Experiments planned / completed

### Team (2–3 bullets)

- Founder background and fit
- Team composition
- Key gaps and hiring plan

### The Ask (2–3 bullets)

- Funding amount
- Use of funds
- Key milestones to achieve

---

## Recommended Next Steps in This Kit

After completing your executive summary, the natural next steps in the **pre-pmf-starter** kit are:

1. **`mission-values-guide`** — synthesize your Personal Ikigai and this executive summary into a mission statement and 3–7 core values for the company.
2. **`okr-workflow-pre-pmf`** — translate mission and values into quarterly OKRs oriented toward discovering product-market fit.

Ask the user: *"Ready to move on to mission and values, or would you like to pause here?"*

**Invocation behavior on the user's response.** When the user affirms — even loosely, even alongside other tasks like *"save this first"* or *"sure, but let me also..."* — invoke `mission-values-guide` immediately via the Skill tool. Do not ask a second confirmation question. If the user's reply references existing material the next skill produces — *"we have a mission and values draft somewhere"*, *"we already wrote core values"*, *"may have most of what we need"* — invoke `mission-values-guide` in refresh mode with the referenced artifact as the baseline. Treat the prior recommendation + a domain-relevant response as a single invocation signal, not two separate decisions.

When invoking, pass through:

- Company name (or working name)
- Problem hypothesis
- Solution concept
- Founder-market fit / Ikigai linkages

If user wants to pause, offer a clean exit with the executive summary saved/exported and a clear path back.

---

## Common Pitfalls to Avoid (Pre-PMF)

- Claiming certainty when everything is hypothesis
- Market sizing without sources
- Ignoring existing alternatives ("nothing like this exists")
- No customer discovery evidence
- Unrealistic timelines to PMF
- Asking for too much or too little capital
- Not knowing team gaps
- Vague validation plans
- Providing "typical" benchmarks without cited research
- Asking more than one question per response (see Core Principles)

---

## Quality Checklist (Pre-PMF Executive Summary)

- [ ] Problem is specific and validated (not assumed)
- [ ] Solution is clear even at concept stage
- [ ] Market size backed by cited sources
- [ ] Business model has logical rationale
- [ ] Validation evidence exists (not just plans)
- [ ] Founder-market fit is compelling
- [ ] Ask is stage-appropriate
- [ ] Focus is on learning, not just growth metrics
- [ ] Honest about what's unknown
- [ ] Fits on one page
