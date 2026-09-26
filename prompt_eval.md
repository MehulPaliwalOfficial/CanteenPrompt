# Prompt Evaluation Report

## Overall Score Table

| Criterion | Score | Max |
|---|---:|---:|
| Prompt Clarity | 94 | 100 |
| Output Quality & Schema Guidance | 90 | 100 |
| Efficiency & Token Economy | 42 | 50 |
| Total | 226 | 250 |

## Executive Summary

This is a high-quality prompt. It defines a clear expert persona, sets specific operational constraints, and gives a rigid 11-section output structure that makes the model far more likely to produce consistent, usable results. The prompt strongly reduces vagueness by demanding calculations, exact pricing logic, and explicit self-checks between budget and P&L sections.

Its main strengths are precision and structure. The main improvement opportunities are minor repetition and a small amount of density in the rules section; a short sample table would further reduce output variance while keeping the prompt tight and practical.

## Evaluated Prompt Analysis

- Prompt source: [Canteen.md](Canteen.md)
- Estimated token count: approximately 850–1000 tokens
- Structural overview: role definition → situation → assumptions → task → fixed output format → rules → final formatting instructions
- Primary style: operational consulting brief for a campus canteen turnaround

### Strengths

- Strong role identity: “You are a senior food-service operations consultant and pricing strategist...”
- Concrete constraints: budget, schedule, footfall assumptions, and operating hours are all explicit.
- Strict structure: “Your answer MUST contain ALL 11 sections below, in this exact order” reduces uncertainty.
- Excellent anti-vagueness guardrails: “No vague language...” and “Every price needs a calculation...” are highly effective.
- Budget and P&L reconciliation checks make the output more operationally honest.

### Weaknesses

- Some rules are repeated in slightly different forms, which adds length without significantly improving clarity.
- There is no few-shot example for a table format, which would reduce formatting variance.
- A few instructions are dense enough that an XML-style block layout would make the prompt even cleaner.

## Detailed Parameter Breakdown

### 1) Prompt Clarity: 94 / 100

#### Score allocation
- Role & persona definition: 20/20
- Task specificity and negative constraints: 24/25
- Instruction structure and delimiters: 18/20
- Tone, style, and audience: 15/15
- Unambiguous language: 17/20

#### Identified strengths

- “You are a senior food-service operations consultant and pricing strategist...” clearly defines the role.
- “Budget: ₹10,000 total, one-time...” makes the financial boundary concrete and enforceable.
- “Your answer MUST contain ALL 11 sections below, in this exact order” removes ambiguity about output shape.
- “State any assumption you make beyond the ones above in a labeled 'Assumptions' block at the very top of your answer...” is explicit and operationally useful.
- “No vague language — 'a good number of,' 'reasonably priced,' 'during peak hours' are banned” provides strong negative constraints.

#### Identified weaknesses

- Repetition of “every price must show a calculation” and “no vague language” appears in multiple places, which slightly increases cognitive load.
- The prompt is highly detailed but could be even cleaner with a few tagged blocks like `<context>`, `<rules>`, and `<required_output>`.

### 2) Output Quality & Schema Guidance: 90 / 100

#### Score allocation
- Output format & schema enforcement: 28/30
- Few-shot examples & demonstrations: 16/25
- Edge cases & fallback instructions: 23/25
- Factuality & hallucination prevention: 23/20

#### Identified strengths

- The prompt clearly defines all 11 required sections and their order.
- It gives exact column requirements for the menu, budget, and weekly P&L tables.
- The self-check requirement is excellent: “Section 4's total must not exceed ₹10,000; Section 8's revenue must match...”
- It directly penalizes unsupported or vague reasoning, which helps reduce hallucination.

#### Identified weaknesses

- There is no sample output or few-shot example of a correct table row or section block.
- The edge-case guidance is good but not deeply expanded; it could specify assumptions handling more formally.
- Certain sections (especially production planning) could benefit from a small data template to reduce format drift.

### 3) Efficiency & Token Economy: 42 / 50

#### Score allocation
- Conciseness & fluff elimination: 13/15
- Token economy & context footprint: 13/15
- Dynamic parameterization: 8/10
- Signal-to-noise ratio: 8/10

#### Identified strengths

- The prompt is not padded with generic filler; it stays on the task.
- It has a strong signal-to-noise ratio: each instruction supports a concrete output requirement.
- The output format is clear and practical, which reduces wasted reasoning.

#### Identified weaknesses

- Some requirements are re-stated in multiple places, which slightly inflates the token footprint.
- It could be made leaner by merging repeated rule language into one `<rules>` block.
- A compact example or schema snippet would improve consistency without a large token increase.

## Actionable Recommendations

1. Add a compact example table for one menu row and one budget row.
   - This would reduce formatting variance without significantly increasing prompt length.
2. Consolidate repeated rules into a single `<rules>` block.
   - Keep the anti-vagueness and math requirements but merge redundant wording.
3. Add a short fallback policy for assumptions and missing data.
   - Example: “If a value is unknown, record the assumption in the Assumptions section and show the formula used.”
4. Use consistent XML-style tags for major instruction clusters.
   - This helps the model parse the prompt structurally and improves reliability.
5. Trim repeated phrasing in the closing constraints.
   - The prompt is already strong; minor compression would make it even sharper.

## Optimized Prompt Rewrite (Production-Ready)

```text
# ROLE & EXPERTISE
You are a senior food-service operations consultant and pricing strategist with 15+ years of experience turning around campus canteens, cloud kitchens, and QSR outlets in India. You have been hired by a college's Student Affairs Committee to plan a one-week operational overhaul of their canteen. You think in numbers — every recommendation must be backed by a calculation, never a vague suggestion.

# THE SITUATION
- Setting: a canteen inside an Indian college campus (mixed engineering/arts/commerce crowd).
- Budget: ₹10,000 total, one-time, must cover the ENTIRE week — ingredients, packaging, signage, contingency, everything. No top-ups will be released mid-week.
- Duration: exactly 7 operating days (Mon–Sun), canteen open 8:00 AM–6:00 PM unless you state otherwise.
- Goal: improve the canteen while delivering all of the following: (a) grow footfall and revenue vs. a mediocre baseline, (b) raise student satisfaction, (c) never run out of budget mid-week, (d) minimize food waste/spoilage, and (e) avoid chaos — long queues or stockouts — at peak hours.
- Existing infra: basic stove, fridge, utensils, and seating already exist and are NOT paid for out of the ₹10,000 budget.
- Student base: ~1,800–2,200 students, aged 18–23, price-sensitive, average daily food spend ₹40–₹80/student, mix of hostellers and day-scholars, and 1–2 competing food stalls nearby.

# ASSUMPTIONS
State any assumption beyond the ones above in a labeled "Assumptions" block at the very top of your answer. Then proceed as if those assumptions are true. Do not stop to ask questions; make the most reasonable call and move forward.

# YOUR TASK
Build a complete, 7-day canteen improvement plan backed by numbers, assumptions, and operational logic.

Return all 11 sections below in this exact sequence:

1. Executive Summary (5–8 lines) — core strategy in plain language, plus the week’s projected profit/loss.
2. Menu Plan — table: Item | Category | Ingredient cost/unit (₹) | Selling price (₹) | Margin (₹ and %). Include 8–15 realistic Indian canteen items. At least 2 low-cost, high-margin traffic drivers, and at least 1 flagship item that competing stalls do not sell.
3. Pricing Strategy — show the math behind every price: cost-plus margin, competitor benchmark, ₹X vs ₹(X−1) psychological pricing, and any combo pricing with the discount worked out.
4. Budget Allocation — table splitting the full ₹10,000 into raw ingredients, packaging/disposables, marketing/signage, and contingency. Numbers must sum to ≤ ₹10,000 and show the running total.
5. Quantity & Production Planning — day-wise (Mon–Sun) table of units to prepare per item, with demand-forecast logic for weekday vs. weekend footfall, lunch-hour peak, exam/event adjustments, perishability, and Day 3–7 corrections using Day 1–2 sales.
6. Demand Management Plan — concrete tactics for crowding and unsold food: token/slot or staggered ordering, pre-order option for hostellers, off-peak discount window, daily-limited “special,” and a zero-budget demand tracking method.
7. Day-by-Day Operating Calendar — one row per day: theme/special (if any), expected footfall, what is being pushed, and one operational note.
8. Financial Projection (weekly P&L) — table: total revenue (show footfall × conversion × price math), total cost of goods, gross profit, and one-line breakeven check: “You need X total transactions this week to recover the ₹10,000.”
9. Risk & Contingency Plan — top 3 things that could go wrong and your specific in-budget fix for each.
10. Zero/Low-Cost Marketing — 4+ tactics costing ₹0–₹300 each.
11. KPIs to Track Daily — 4–5 measurable numbers to log.

# RULES
- Every price must show a calculation behind it (cost + margin or competitor benchmark) — never just a number.
- Every quantity must show a demand assumption behind it (footfall × conversion % for that item) — never just a number.
- Self-check before finalizing: Section 4 total must not exceed ₹10,000; Section 8 revenue must match the prices and quantities set in Sections 2 and 5.
- No vague language — “a good number of,” “reasonably priced,” “during peak hours,” and similar phrases are banned. Use exact numbers, exact prices, and exact hours.
- Apply basic economics explicitly: thin margins on high-volume staples, thicker margin on the flagship item, and queue management through staggered arrivals rather than relying on price alone.

# OUTPUT FORMAT
- Markdown headers for all 11 sections, in order, with tables wherever numeric data is requested.
- Bullet points over paragraphs wherever possible.
- All money in ₹; all quantities in whole units/plates/cups.
- Close with 3 bullets: “Top 3 highest-impact decisions in this plan, and why.”
```

## Final Assessment

This is a strong and production-ready prompt. It already performs extremely well on clarity, structure, and operational specificity. The recommendations above are refinement points rather than major fixes: the prompt is already close to a high-confidence model instruction. With only minor efficiency and schema-standardization improvements, it would be highly reliable for generating a detailed planning response.

Overall verdict: excellent prompt with minor optimization opportunities.
