# The quality model (ISO/IEC 25010)

When you classify requirements, the quality-attribute bucket is the one people under-cover: they remember performance and forget portability, remember security and forget maintainability. Working from a fixed, standard list fixes that: you check the same dimensions every time, and you and the client share a vocabulary.

**ISO/IEC 25010** is the international standard product-quality model. The 2011 edition defines eight characteristics; the 2023 revision renames two and adds Safety. Both are given below; use whichever your organisation standardises on, because the point is the completeness, not the exact label.

## The characteristics

**Functional suitability** — does it do the right things, correctly, completely? (Completeness, correctness, appropriateness.) The bridge between the functional and quality buckets: a feature exists in the functional list; *how correctly and completely* it must behave is a quality requirement.

**Performance efficiency** — behaviour relative to the resources used. Sub-dimensions worth separating: *time behaviour* (latency, response time), *throughput/capacity* (requests/sec, concurrent users, data volume), and *resource utilisation* (CPU, memory, cost). Keep these apart — "fast" and "handles load" are different requirements with different designs.

**Compatibility** — co-existence with other systems and interoperability through shared interfaces and formats. Significant whenever the system lives in an ecosystem it must integrate with.

**Interaction capability** (2023; *Usability* in 2011) — how well people can learn, operate, and recover from errors with the system. Includes accessibility. Often carries hidden performance requirements ("it must feel instant").

**Reliability** — does it keep working? *Availability* (uptime, the "nines"), *fault tolerance* (behaviour when a part fails), *recoverability* (how fast and how completely it recovers). Availability targets are among the most expensive requirements to meet; see `feasibility-check.md` for the nines table.

**Security** — confidentiality, integrity, authenticity, accountability/non-repudiation, and resistance to misuse. Almost always cross-cutting and almost always under-specified in briefs; name the data, the threats, and the obligations explicitly.

**Maintainability** — how cheaply the system can be changed: modularity, reusability, how easy it is to analyse, modify, and test. This is the quality that determines the *second year's* cost, so it is routinely sacrificed and routinely regretted. Make it an explicit requirement when the system will live long or change often.

**Flexibility** (2023; expands *Portability* from 2011) — adaptability to new environments, installability, replaceability, and scalability. (In 2011, scalability sat loosely under performance; 2023 places it here.) Significant when the deployment target, the scale, or the environment is expected to change.

**Safety** (added 2023) — freedom from unacceptable risk of harm to people, property, or the environment. Relevant for systems whose failure has physical or serious real-world consequences.

## Using the model in the pipeline

- **In classification (step 2):** for each requirement in the quality bucket, tag which characteristic it belongs to. Then scan the full list of characteristics and ask "has the brief said anything about this one?" The silences are as informative as the statements — an unstated availability or security requirement is a question for the client, not an assumption to make.
- **In prioritisation (step 4):** you will not design hard for all nine. Identify the two or three characteristics that are both high business value and high architectural impact for *this* system; those drive the design. State the rest as satisfied-by-default or out of scope, explicitly.
- **In scenarios (step 6):** every quality characteristic you keep must become a measurable scenario, or it is just an adjective. See `scenarios-and-priorities.md`.

## Further reading

ISO/IEC 25010, *Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — Product quality model.* The standard's own text defines each characteristic and sub-characteristic precisely.
