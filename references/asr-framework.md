# What makes a requirement architecturally significant

Most requirements in a brief could be satisfied a dozen ways and none of the dozen would change the system's shape. A few requirements are different: satisfying them forces a structural decision, rules out options, or sets a bar that an obvious implementation would miss. Those are the **architecturally significant requirements (ASRs)**, and they are what this analysis is for.

## Signals that a requirement is significant

A requirement is probably architecturally significant if it shows one or more of these signals. None is conclusive alone; the more that stack up, the more significant it is.

- **It sets a demanding quality bar.** A target that a naive, first-attempt implementation would not meet — a latency ceiling, an availability figure, a throughput number, a time-to-market — forces you to design *for* it rather than discover it later.
- **It trades off against something else.** The requirement pulls in the opposite direction from another one: strong consistency versus low latency, rich auditability versus storage cost, flexibility versus simplicity. Where requirements fight, the architecture is where the fight is resolved — so those requirements are significant.
- **Its reach is wide.** It cannot be satisfied inside one module; it touches many parts of the system, or every part. Cross-cutting requirements (security, observability, multi-tenancy, internationalisation) are significant precisely because they are everywhere.
- **It is expensive to reverse.** If getting it wrong means a rewrite rather than a patch — the data model, the consistency model, the trust boundary, the choice of synchronous vs event-driven — then the decision it drives is one you want to make deliberately and early.
- **It breaks an assumption.** It contradicts something you would otherwise have taken for granted ("all users are in one region", "the dataset fits in memory", "traffic is steady"). Assumption-breakers are easy to miss and costly when missed.
- **It is important but hard to pin down.** Stakeholders clearly care about it, yet it resists precise statement ("it must feel instant", "it has to scale"). Significance and vagueness often travel together — the vagueness is a reason to analyse, not to ignore.

## Why they hide in a brief

ASRs are rarely labelled as such. They are typically:

- **stated as features** — "a live dashboard" is really a set of latency, freshness, and concurrency requirements;
- **embedded in business context** — "we run flash sales" is a peak-load and oversell-prevention requirement;
- **left unstated because they are assumed** — the client never says "it must comply with their data-residency law" because to them it is obvious;
- **phrased as a solution** — "we need Kafka" hides the real requirement (throughput, decoupling, replay) behind a chosen mechanism.

## How to surface them while reading

Read the raw input with these prompts in mind and the ASRs tend to fall out:

- **Scan for numbers** — and for the numbers that *should* be there but are missing. Every quantity (users, requests/sec, data volume, latency, uptime, budget) is a candidate ASR; every quality claim with no number is a question to ask.
- **Look for change over time** — growth, peaks, seasonality, "eventually we'll…". These are scalability and extensibility requirements.
- **Look at the edges** — external systems, regulators, third parties, other teams. Boundaries are where constraints and integration requirements live.
- **Listen for absolutes** — "always", "never", "immediately", "no downtime", "fully auditable". Absolutes are expensive and usually significant.
- **Translate solutions back into needs** — whenever the brief names a technology, ask what requirement motivated it and record *that*.

See `quality-model.md` for the quality dimensions to check against, `brief-smells.md` for the warning patterns, and `scenarios-and-priorities.md` for turning a significant requirement into a testable scenario.

## Further reading

For a research-grounded treatment of how practitioners characterise architecturally significant requirements, see Chen, Ali Babar & Nuseibeh, "Characterizing Architecturally Significant Requirements," *IEEE Software* 30(2), 2013.
