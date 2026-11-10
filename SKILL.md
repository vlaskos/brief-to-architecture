---
name: asr-analysis
description: Turn a raw brief, RFP, discovery transcript, or feature spec into an architect-grade analysis — the architecturally significant requirements pulled out and split into functional / quality-attribute / constraint, each sharpened into something testable, prioritised by business value and architectural impact, checked for requirements that quietly contradict each other, and turned into measurable quality scenarios with the design strategies that would satisfy them. Use whenever a brief, pre-sales input, RFP, discovery-call notes, kickoff document, or set of requirements needs to be assessed before estimation or design — and whenever someone asks what is architecturally significant here, what could go wrong with these requirements, whether this is even buildable, what to ask the client, or how to architect it. Grounded in the ISO/IEC 25010 quality model.
license: MIT
---

# ASR analysis

A brief is not a specification. It is a pile of wishes, assumptions, and half-stated constraints, and buried inside it are the few requirements that will actually decide the shape, and the cost, of the system. This skill finds those, makes them precise, and checks them against each other before anyone commits to an estimate or a design.

An **architecturally significant requirement (ASR)** is a requirement with a measurable effect on the architecture: meeting it forces a structural choice, constrains a technology, sets a quality bar that is hard to hit, or interacts with other requirements in a way that limits your options. Most requirements in a brief are *not* architecturally significant. The job is to separate the vital few from the many, and to say why each one matters.

The quality-attribute side of this work is anchored in **ISO/IEC 25010**, the international standard product-quality model. Using a standard set of quality characteristics keeps the analysis complete (you check the same dimensions every time) and gives everyone a shared vocabulary. See `references/quality-model.md`.

## The pipeline

Run a brief through six steps. Each produces an artefact the next one uses.

1. **Extract, don't transcribe.** Read the raw input and pull out the real requirements, including the ones stated as features, complaints, or offhand asides. A sentence like "our Black Friday traffic is 40× normal" is not a feature request; it is a performance and scalability requirement in disguise. Interpret. See `references/asr-framework.md` for how to recognise what is architecturally significant.

2. **Classify.** Sort each extracted requirement into one of three buckets:
   - **Functional** — what the system must *do*.
   - **Quality attribute** — how well it must do it (performance, reliability, security, maintainability, …). Use the ISO/IEC 25010 characteristics so you cover the same ground every time — `references/quality-model.md`.
   - **Constraint** — a fixed, non-negotiable boundary (a mandated technology, a regulation, a deadline, an existing system). Constraints are not up for design; they shape everything else.

3. **Sharpen.** Rewrite each significant requirement so it is unambiguous and testable, and state its **architectural implication** — the structural consequence of taking it seriously. Strip out solutions the author smuggled in ("use Kafka" is a proposed mechanism, not a requirement; the requirement is the throughput or decoupling behind it). A requirement you cannot test, you cannot estimate.

4. **Prioritise on two axes.** Not every ASR deserves equal attention. Rank each on:
   - **Business value** — how much the outcome matters to the client.
   - **Architectural impact** — how much it constrains the design and how expensive it is to reverse. (High impact is about *irreversibility and blast radius*, not effort.)
   The requirements that are high on both are where the architecture is really decided. Spend your analysis there. See `references/scenarios-and-priorities.md`.

5. **Check feasibility.** Before designing anything, check that the high-priority requirements can *coexist*. The most dangerous briefs are internally contradictory: a latency target, a consistency target, and a cost ceiling that cannot all be true at once. See `references/feasibility-check.md` for a concrete method, including the arithmetic one for numeric requirements.

6. **Specify scenarios and pick strategies.** For the high-priority quality attributes, write **measurable quality scenarios** (a trigger, the conditions, and a response you can measure), then choose the **design strategies** that would satisfy each, with their cost. See `references/scenarios-and-priorities.md` and `references/design-strategies.md`.

## Discipline that makes the analysis trustworthy

- **Spot the smells.** Briefs have recurring failure patterns: vague superlatives, hidden assumptions, numbers with no unit or no source, requirements that contradict. `references/brief-smells.md` is a catalogue of them and what to ask when you see one.
- **Mark every assumption.** When the brief is silent and you fill a gap, label it: is it a *filled gap* (information missing, you supplied a default), an *interpretation* (ambiguous, you chose a reading), or a *scope narrowing* (you deliberately excluded something)? An estimate built on unlabelled assumptions is a guess wearing a suit.
- **End with the questions that change the shape.** The output of a good analysis includes the two or three questions whose answers would most change the architecture. Those are what the next client conversation should be about.
- **An estimate is only as defensible as the analysis under it.** This is why the analysis comes first: it is what makes the number you give the client something you can stand behind.

## How to use this skill

- Analysing a brief end to end → run the six-step pipeline above.
- Deciding what is architecturally significant → `references/asr-framework.md`.
- Choosing and covering quality attributes → `references/quality-model.md` (ISO/IEC 25010).
- Writing testable quality scenarios and prioritising them → `references/scenarios-and-priorities.md`.
- Choosing design approaches per quality attribute → `references/design-strategies.md`.
- Catching contradictions and impossible combinations → `references/feasibility-check.md`.
- Reading a brief critically → `references/brief-smells.md`.
- Shaping the written deliverable → `references/output-template.md`.
