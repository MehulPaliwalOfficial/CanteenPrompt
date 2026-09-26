# Prompt Evaluation Report

## Overall Score

| Criterion | Score | Max | Notes |
|---|---:|---:|---|
| Prompt Clarity | 84 | 100 | Strong role framing and mission clarity; some crowded instructions and repeated constraints. |
| Output Quality & Schema Guidance | 75 | 100 | Rich deliverables and decision logic are requested, but the prompt lacks strict output schema and examples. |
| Efficiency & Token Economy | 33 | 50 | Dense and useful, but includes redundancy, repeated caveats, and extra verbosity. |
| Total | 192 | 250 | Well-scoped but would benefit from tighter structure and explicit formatting rules. |

## Executive Summary

This prompt is strong in intent and business specificity. It clearly defines a senior consultant persona, the budget constraints, and the required deliverables. The prompt gives a clear operational objective: increase footfall, reduce waste, manage queue pressure, and remain within a hard ₹10,000 budget.

The main weakness is not content quality but structural discipline. The prompt asks for many outputs without a consistent schema, which raises the chance of inconsistent formatting, missing assumptions, or uneven response quality. There is also some repetition across sections, especially around constraints, budget, and crowd-management goals. A tighter XML-style structure and explicit output format would make the prompt substantially more reliable and efficient.

## Evaluated Prompt Analysis

- Prompt source: [Canteen.md](Canteen.md)
- Estimated token count: ~650–800 tokens
- Structural overview: role + situation + goal + requirements + rules + close-out statement
- Primary style: operational consulting brief for a campus food-service turnaround

### What works well

- Clear persona: “Act like a senior food-service consultant...”
- Concrete constraints: “₹10,000, one-time...” and “Monday to Sunday, 8am to 6pm”
- Business-specific requirements: menu, pricing logic, daily prep quantities, crowd management, P&L, risks, marketing, KPI tracking
- Strong anti-vagueness rule: “Every price needs the math behind it...” and “Every quantity needs the demand logic behind it too.”

### Key issues

- The prompt is trying to produce too many detailed artifacts in one pass without a final response contract.
- It lacks explicit output schema guidance such as a table format for menu items, a pricing section format, or a fixed KPI section.
- There are repeated reminders to avoid vague phrasing and uncertain assumptions, which adds length without improving clarity much.
- It contains a few ambiguous instructions, such as “If you need to assume anything beyond this, state it upfront and keep going” which is reasonable, but it could be framed more explicitly as a required assumptions section.

## Detailed Parameter Breakdown

### 1) Prompt Clarity: 84 / 100

#### Strengths

- Strong role anchoring: “Act like a senior food-service consultant who's actually turned around college canteens before...”
- Specific operating context: “₹10,000, one-time... Monday to Sunday, 8am to 6pm”
- Explicit business parameters: “roughly 1800–2200 students... ₹40–80 a day...”
- Very clear output asks: “1. A menu ... 2. The actual pricing logic ... 3. Exactly how the ₹10,000 splits...”
- Good negative constraints: “No top-ups mid-week”, “No vague phrases...”

#### Weaknesses

- The prompt is long and dense. The user request list is comprehensive but can be overwhelming without a final response structure.
- It repeats the same high-level theme (“be specific”, “no vague terms”, “math behind it”) several times, which slightly reduces clarity efficiency.
- There are no explicit formatting delimiters for sections; the prompt relies on natural-language sequencing rather than XML headings or a strict template.

#### Score rationale

This category scores high because the goal, constraints, and required outputs are mostly clear and operationally specific. The main drag is verbosity and repetition rather than conceptual ambiguity.

### 2) Output Quality & Schema Guidance: 75 / 100

#### Strengths

- It defines a rich set of expected deliverables: menu, pricing logic, budget split, prep plan, crowd flow, calendar, P&L, risks, marketing, KPIs.
- It includes a strong constraint that the answer must be numeric and evidence-based.
- It tells the model to “double-check” budget and P&L consistency, which is a good grounding instruction.

#### Weaknesses

- There is no explicit response schema. For example, there is no required output format for the menu table, no fixed fields for each item, and no template for the day-by-day calendar or P&L section.
- The prompt does not include a sample output or a few-shot example, which would help align formatting and assumptions.
- Because the prompt asks for so much in one answer, there is a greater chance of inconsistent data structures across sections.
- It does not specify what to do when assumptions are required, beyond “state them upfront.” A clearer standard assumption section would reduce drift.

#### Score rationale

This is a strong content brief, but it does not steer output shape closely enough for highly consistent generation. The result may still be good, but it is more likely to vary in structure and detail than a schema-first prompt.

### 3) Efficiency & Token Economy: 33 / 50

#### Strengths

- High signal-to-noise ratio in the core business requirements.
- The instructions avoid fluff in most places and move directly into operational needs.
- It focuses on measurable outcomes rather than generic “be helpful” language.

#### Weaknesses

- Repetition: “Every price needs the math behind it...” and “Every quantity needs the demand logic behind it too...” appear multiple times in several forms.
- The prompt includes repeated guidance on vagueness, assumptions, and budget consistency, which is important but not necessary to repeat so often.
- The user request section is dense and could be shortened by combining grouped requirements into a single structured template.
- Lack of parameterization means the model must infer where assumptions belong and how to format sections, increasing cognitive load.

#### Score rationale

This is a solid but not lean prompt. It is efficient enough to be actionable, but it would benefit from a more compositional format and less repetition.

## Actionable Recommendations

1. Add a strict response template and section order.
   - Use named blocks such as `<assumptions>`, `<menu>`, `<pricing_logic>`, `<budget_allocation>`, `<prep_plan>`, `<crowd_management>`, `<daily_calendar>`, `<p_and_l>`, `<risks>`, and `<kpis>`.

2. Add a required output schema for the menu and P&L sections.
   - Example: a table with columns for Item, Unit Cost, Selling Price, Gross Margin %, Daily Prep, Daily Revenue, and Notes.

3. Add a sample few-shot snippet.
   - One short example of a menu row or a daily-prep table would dramatically reduce formatting ambiguity.

4. Consolidate repeated anti-vagueness instructions.
   - Merge the requirements into a single “non-negotiable rules” section instead of repeating them in multiple places.

5. Define a standard assumptions protocol.
   - Example: if a value is assumed, place it under `<assumptions>` and state the reason and the effect on the model’s calculations.

6. Split the prompt into “must do” vs. “nice-to-have” instructions.
   - This reduces overloading and helps preserve the high-priority business constraints.

## Optimized Prompt Rewrite (Production-Ready)

```text
ROLE
You are a senior food-service consultant with direct experience turning around college canteens. Your recommendations must be grounded in realistic numbers, operational logic, and cash discipline. Do not give generic advice; every decision must be backed by math, assumptions, and a clear profit rationale.

<goal>
Increase student footfall, improve customer satisfaction, protect the ₹10,000 budget, minimize waste, and reduce lunch-hour queue pressure without running out of money mid-week.
</goal>

<context>
- Budget: ₹10,000 one-time for the full week (Monday–Sunday, 8:00 AM–6:00 PM)
- Includes all ingredients, packaging, signage, promotions, and contingency
- Does not include stove, fridge, utensils, or seating
- College profile: approx. 1,800–2,200 students; 18–23 years old
- Typical spend: ₹40–₹80 per student per day
- Student mix: hostellers and day-scholars
- Competition: 1–2 nearby food stalls serving similar demand
- Operating assumption: no mid-week top-up; use all budget efficiently
</context>

<non_negotiable_rules>
1. Every price must include cost-plus math and a rationale.
2. Every quantity must include demand logic and prep reasoning.
3. Budget must total ₹10,000 or less and must reconcile with your final plan.
4. Final P&L revenue must match the menu prices and quantities used earlier.
5. Do not use vague language such as “reasonably priced,” “good number,” or “during peak hours” without specific numbers.
6. If you need to assume anything beyond the given context, state the assumption clearly in an <assumptions> section and continue.
7. Apply the theory in practice: thin margins on staples, stronger margins on flagship items, and crowd management through staggered demand rather than price alone.
</non_negotiable_rules>

<required_output>
Deliver the answer in this exact section order:

1. <assumptions>
2. <menu>
3. <pricing_logic>
4. <budget_allocation>
5. <daily_prep_plan>
6. <crowd_management>
7. <weekly_calendar>
8. <profit_and_loss>
9. <risk_management>
10. <marketing_ideas>
11. <daily_kpis>
12. <top_3_calls>

Use markdown headings for each section.
</required_output>

<section_requirements>
1. <menu>
   - Include 8–15 real Indian canteen items
   - Include cost per unit, selling price, and gross margin for each item
   - Include at least 2 cheap, high-margin items to pull students in
   - Include 1 flagship item that nearby rivals do not offer
   - Give a short rationale for why the item belongs in the menu

2. <pricing_logic>
   - Explain the cost-plus pricing strategy
   - Compare your prices against likely rival pricing
   - Explain any ₹X vs ₹(X−1) psychological pricing choices
   - Include combo pricing, if used, with exact numbers and math

3. <budget_allocation>
   - Show the exact ₹10,000 budget split across ingredients, packaging, marketing, contingency, and any other relevant category
   - The total must equal ₹10,000 or less

4. <daily_prep_plan>
   - Show how much to prepare for each item on each day (Mon–Sun)
   - Explain your logic by day type: weekday vs weekend, lunch rush, exam-week checks, and perishability constraints
   - Show how prep volumes reduce as perishables age
   - Explain how Day 1–2 sales should influence rest-of-week production

5. <crowd_management>
   - Propose a token or staggered-order system
   - Include a pre-order option for regular hostellers
   - Include a discount window during slow hours
   - Include one limited daily special for urgency without overproduction
   - Include a free daily demand-tracking method such as a tally sheet

6. <weekly_calendar>
   - For each day, specify the special, expected footfall, top-selling push, and one operations note

7. <profit_and_loss>
   - Provide revenue, total cost, gross profit, and break-even transactions
   - Show the formula clearly using your chosen footfall × conversion × price structure

8. <risk_management>
   - Identify the top 3 risks
   - For each risk, give a specific in-budget fix

9. <marketing_ideas>
   - Give at least 4 ideas costing ₹0–₹300 each
   - Include WhatsApp groups, posters, freebies, referral perks, and other practical methods

10. <daily_kpis>
   - Give 4–5 metrics to track daily
   - Include sold vs. prepared, queue time, revenue vs target, and waste %

11. <top_3_calls>
   - End with the three highest-impact decisions in the plan
   - Explain why each one matters most
</section_requirements>

<output_format>
- Use concise but complete markdown.
- Prefer tables for menus, budget, prep volumes, weekly calendar, and P&L.
- Use exact rupee values and formulas.
- Use short explanatory bullets where needed.
- Do not output vague narrative or filler.
- Keep the answer practical, specific, and grounded in real canteen economics.
</output_format>

<final_quality_bar>
The answer should read like a real operating plan a college canteen owner could implement immediately.
</final_quality_bar>
```

## Final Assessment

This is a solid, business-specific prompt with clear purpose and strong operational constraints. It is highly useful as a planning brief, but it would become much more reliable if it were converted into a tighter structured prompt with explicit sections, schema guidance, and a few example output patterns. The biggest gains would come from reducing redundancy and turning the user request into a formal output contract.

Overall verdict: effective but not yet optimized for consistent high-quality model output.
