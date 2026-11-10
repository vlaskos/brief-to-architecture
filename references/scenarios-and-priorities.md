# Quality scenarios and how to prioritise them

A quality requirement written as an adjective ("fast", "reliable", "secure") cannot be designed for or tested. The fix is to turn each one into a **quality scenario**: a concrete, measurable statement of what should happen when the system is put under a specific stress. Then, because you cannot optimise for everything, you prioritise the scenarios and design hard only for the ones that matter most.

## Writing a quality scenario

A usable scenario answers five questions. Keep it to a sentence or two; this is a specification tool, not an essay.

1. **Trigger** — what event or condition exercises the quality? (A burst of traffic, a node failure, a malicious request, a new feature to add.)
2. **Conditions** — what state is the system in when it happens? (Normal operation, peak load, degraded/failover, startup.)
3. **Where** — which part of the system is involved? (The checkout service, the data store, the public API.)
4. **Expected response** — what should the system do? (Serve the request, fail over, reject and log, keep data consistent.)
5. **Measure** — the threshold that makes it pass or fail, with a number and a unit. (p95 under 300 ms; recover within 30 s; zero oversell; 99.9% of the month.)

**Example.** *Trigger:* a product goes viral and request rate hits 40× baseline. *Conditions:* peak sale period. *Where:* the catalogue read path. *Response:* requests are served from cache without hitting the primary database. *Measure:* p95 latency stays under 400 ms and error rate under 0.1% for the duration of the spike.

Written this way, the requirement is testable: you can build a load test that either passes or fails it. Every quality attribute you keep (from `quality-model.md`) should produce at least one scenario like this.

## Prioritising with a quality-scenario tree

List every scenario and you have a flat pile with no sense of what the architecture is actually *for*. Organise them into a small tree and tag each by importance, and the design priorities become visible.

- **Group by quality characteristic.** Make a branch per ISO 25010 characteristic that is in play (performance, reliability, security, maintainability, …). Hang the relevant scenarios under each branch. This also exposes empty branches — a characteristic with no scenario is either out of scope (say so) or an unasked question.
- **Tag each scenario on two axes**, the same two used in step 4 of the pipeline:
  - **Business value** — how much the client's outcome depends on it (High / Medium / Low).
  - **Architectural impact** — how much it constrains the design and how costly it is to reverse (High / Medium / Low). This is about *irreversibility and reach*, not effort.
- **Read the corners.** The scenarios tagged **(High business value, High architectural impact)** are where the architecture is decided — design for them first and deliberately. (High value, low impact) are features you can satisfy later without structural risk. (Low value, high impact) are traps — expensive to build in, little payoff; push back on them. (Low, low) can wait.

The tree does two jobs at once: it forces every quality requirement to become a testable scenario, and it tells you which handful of scenarios deserve the design effort. It is also the natural agenda for a prioritisation conversation with the client: walk the high-impact branches together and confirm the rankings.

## From scenarios to design

Each high-priority scenario is then the input to step 6: choose the design strategy that would satisfy it, and note that strategy's cost. See `design-strategies.md`.

## Further reading

The idea of eliciting and prioritising quality-attribute scenarios in a tree is central to scenario-based architecture evaluation; for the original formulation (the "utility tree" and the ATAM method built around it) see Bass, Clements & Kazman, *Software Architecture in Practice* (Addison-Wesley).
