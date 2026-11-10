# Feasibility check

The most dangerous briefs are not the vague ones; a vague brief you can question. The dangerous ones are internally contradictory: every requirement looks reasonable on its own, and the impossibility only appears when you hold two or three of them up together. Check feasibility *before* you design, because a design built on a contradiction fails late and expensively.

There are two kinds of contradiction to hunt: **logical** (two requirements pull in opposite directions) and **arithmetic** (the numbers, multiplied out, don't fit reality).

## Logical contradictions

Some quality attributes are in natural tension. When a brief demands both ends of one of these tensions at full strength, flag it:

- **Consistency vs latency vs partition tolerance** — strong global consistency and very low write latency across regions cannot both be maximised; a network partition forces a choice.
- **Availability vs consistency** — "never down" and "never serve stale or conflicting data" fight during failures.
- **Security vs usability / performance** — every check, hop, and encryption step costs latency and friction; "frictionless" and "zero-trust everywhere" need an explicit balance.
- **Flexibility vs simplicity** — "infinitely configurable" and "works out of the box with no setup" are opposite design centres.
- **Retention vs cost** — "keep everything forever, instantly queryable" and "minimal storage spend" don't reconcile without tiering.
- **Scope vs quality vs deadline** — the classic triangle; fixing all three over-constrains the project.

For each tension present in the brief, decide which side wins (and by how much), or surface it as the key client question. The architecture *is* the resolution of these tensions, and naming them is half the design.

## Arithmetic contradictions

Numbers that are individually fine can be jointly impossible. Multiply (or divide) the hard numeric requirements out and sanity-check the result against physical reality. A few recurring checks:

- **Throughput × payload = bandwidth.** 50,000 requests/sec × 200 KB average response ≈ 10 GB/s ≈ 80 Gbps of egress. If the brief also implies a modest cloud budget, you have found a contradiction.
- **Volume/day × retention = storage.** 500 GB ingested per day × 7 years retained ≈ 1.25 PB before replication. "Keep raw events forever" plus "small footprint" rarely survive this line.
- **Latency budget, decomposed.** A 100 ms end-to-end p95 must be split across every hop: network, gateway, service calls, database, serialisation. If five sequential calls each "usually take 30 ms", the budget is already blown before you add the tail. Latency adds up the slow way (tails compound), not the average way.
- **Concurrency = arrival rate × service time** (Little's Law). 2,000 requests/sec each holding a connection for 200 ms means ~400 in flight at all times — size pools, threads, and limits for that, not for the average.
- **Work per unit vs deadline.** "Process 10 million records in a 1-hour nightly window" ⇒ ~2,800 records/sec sustained. Is one record's processing cheap enough to hit that on the planned hardware? Multiply it out.

The method is deliberately crude: take the two or three requirements that are both high-value and high-impact, express each as a number, combine them, and ask "is the result physically and financially possible?" Crude arithmetic catches most impossible briefs before any whiteboard appears.

## The availability table

Availability targets are stated casually ("we need high availability", "five nines") and are among the most expensive requirements to meet. Translate the words into a downtime budget before accepting them:

| Target | Downtime per year | Downtime per month | Downtime per day |
|---|---|---|---|
| 99% ("two nines") | ~3.65 days | ~7.2 hours | ~14.4 min |
| 99.9% ("three nines") | ~8.76 hours | ~43.8 min | ~1.44 min |
| 99.95% | ~4.38 hours | ~21.9 min | ~43 s |
| 99.99% ("four nines") | ~52.6 min | ~4.38 min | ~8.6 s |
| 99.999% ("five nines") | ~5.26 min | ~26 s | ~0.86 s |

Each additional nine typically multiplies cost and complexity: redundancy, automated failover, multi-region, and the operational maturity to deploy and recover within that budget. When a brief says "five nines", show this table and ask whether the business case justifies the jump from, say, three, because that jump is where a large share of the architecture (and the estimate) goes.

## Output of the check

The feasibility check produces three things: the **tensions** you identified and how you propose to resolve them, any **impossibilities** you found and what has to give, and the **questions** whose answers would settle the rest. Feed all three into the written analysis (`output-template.md`).
