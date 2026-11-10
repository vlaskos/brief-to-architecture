# Design strategies per quality attribute

Once a high-priority quality scenario exists (`scenarios-and-priorities.md`), the question is *how* you would satisfy it. This note sketches the common, well-established design strategies for each major quality attribute, with a note on what each one costs, because every strategy buys one quality at the expense of another, and naming the cost is what keeps the analysis honest.

This is a practitioner's map of widely known techniques, not an exhaustive catalogue. For a rigorous, comprehensive taxonomy of architectural tactics, see the Further reading at the end.

## A rule that applies to all of them

**Every strategy has a cost, and the cost is usually another quality attribute.** Caching buys latency and spends consistency and memory. Redundancy buys availability and spends cost and operational complexity. An abstraction layer buys flexibility and spends simplicity and often performance. Write the cost next to the strategy, always. A strategy proposed without its cost is a sales pitch, not an analysis.

## Performance (latency, throughput)

- **Do less work:** caching, precomputation/materialised views, pagination, cheaper algorithms and data structures. *Cost:* staleness, memory, invalidation complexity.
- **Spread the work:** horizontal scaling, load balancing, partitioning/sharding, async processing and queues. *Cost:* coordination, eventual consistency, operational surface.
- **Manage contention:** connection/thread pooling, backpressure, rate limiting, bounded concurrency. *Cost:* rejected or delayed work under overload (which must itself be specified).

## Reliability (availability, fault tolerance, recoverability)

- **Redundancy and failover:** multiple instances, replicas, multi-AZ/region, health checks and automated failover. *Cost:* money, data-consistency challenges, failover testing burden.
- **Contain failure:** circuit breakers, bulkheads (isolate resource pools), timeouts and retries with backoff, graceful degradation. *Cost:* added moving parts; retries can amplify load if naive.
- **Recover:** backups, point-in-time restore, idempotent operations, replayable event logs. *Cost:* storage, recovery-time engineering, discipline to test restores.

Tie the chosen reliability strategy back to the availability budget in `feasibility-check.md`: the number of nines dictates how far up this list you must climb.

## Security (confidentiality, integrity, accountability)

- **Keep attackers out and limit blast radius:** authentication, least-privilege authorisation, network segmentation, secrets management. *Cost:* latency, friction, operational care.
- **Protect data:** encryption in transit and at rest, tokenisation, data minimisation and residency controls. *Cost:* key management, performance, complexity.
- **Detect and account:** audit logging, tamper-evident trails, monitoring and alerting. *Cost:* storage, privacy considerations, noise if untuned.

## Maintainability (changeability, testability)

- **Modularity and boundaries:** clear interfaces, high cohesion, low coupling, separation of concerns. *Cost:* up-front design effort; over-modularisation adds indirection.
- **Defer and localise change:** configuration over code, feature flags, dependency inversion, anti-corruption layers at integration points. *Cost:* indirection, more moving parts to reason about.
- **Make change safe:** automated tests, clear contracts, observability. *Cost:* build and maintenance time that pays back over the system's life.

## Flexibility and scalability

- **Scale out, not just up:** statelessness, externalised session/state, partitioning, elastic infrastructure. *Cost:* distributed-system complexity, consistency trade-offs.
- **Portability and replaceability:** standard interfaces, containerisation, avoiding deep coupling to one provider's proprietary services. *Cost:* you may forgo the convenience and performance of those proprietary services.

## Using this in the analysis

For each high-priority scenario, name one or two candidate strategies, state what each would cost, and where it matters, trace it back to the requirement it serves and forward to the quality attribute it spends. That traceability (requirement → scenario → strategy → cost) is what turns "we'll make it scalable" into a defensible plan and a defensible estimate.

## Further reading

For the comprehensive, named catalogue of architectural tactics organised by quality attribute, see Bass, Clements & Kazman, *Software Architecture in Practice* (4th ed., Addison-Wesley). This note is a condensed, independent practitioner's map; the book is the thorough reference.
