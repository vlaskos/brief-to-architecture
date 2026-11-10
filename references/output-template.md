# Output template

The analysis is only useful if it lands as a document someone can read, challenge, and estimate from. This template structures the written deliverable. Keep it tight: a reader should get the gist from the summary and the priority table alone, and drill down only where they need to.

## 1. Summary
Three to five sentences: what the system is, the two or three requirements that will decide its shape, the biggest risk or contradiction you found, and the single most important question for the client. A busy reader should be able to stop here and still know the stakes.

## 2. Architecturally significant requirements
A table of the requirements that matter, sharpened and classified:

| # | Requirement (sharpened, testable) | Type (Functional / Quality / Constraint) | Architectural implication |
|---|---|---|---|
| 1 | … | … | … |

Only the significant ones belong here; routine requirements go in an appendix or the backlog, not this table.

## 3. Priorities
The quality-scenario tree or, more simply, the requirements plotted on the two axes: **business value** and **architectural impact**. Call out the (high, high) items explicitly: these are what the design and the estimate hinge on.

## 4. Quality scenarios
For each high-priority quality attribute, the measurable scenario(s) that make it testable (trigger, conditions, where, response, measure). See `scenarios-and-priorities.md`.

## 5. Feasibility
The tensions and contradictions you found, the arithmetic that exposed any impossibilities, and how you propose to resolve each, or what has to give. Include the availability budget if an uptime target was stated. See `feasibility-check.md`.

## 6. Design direction
For the high-priority scenarios, the candidate design strategies and their costs, enough to justify the estimate, not a full design. See `design-strategies.md`.

## 7. Assumptions
Every gap you filled, labelled by kind:
- **Filled gap** — information was missing; you supplied a stated default.
- **Interpretation** — the brief was ambiguous; you chose a reading and noted it.
- **Scope narrowing** — you deliberately excluded something; you said so.

An estimate attached to unlabelled assumptions is not defensible. This section is what makes it defensible.

## 8. Questions that change the shape
The two or three questions whose answers would most change the architecture (and therefore the estimate). This is the agenda for the next client conversation and often the most valuable part of the document.

---

## Format notes

- Lead with the summary and the priority table; everything else is supporting detail.
- Tie claims to evidence: every "this is significant" should trace to a signal (`asr-framework.md`), every "this is infeasible" to the arithmetic (`feasibility-check.md`).
- State what is **out of scope** as clearly as what is in. Unstated scope is where disputes start.
- Keep client-specific names and figures in placeholders if the document will be reused or shared beyond the engagement.
