# Brief smells

A "smell" is a surface pattern in a brief that signals a buried risk: an unstated requirement, a hidden assumption, or a contradiction waiting to surface during the build. Reading for smells is how you turn a cooperative read ("what do they want?") into a critical one ("what will hurt us?"). Each smell below comes with what it usually hides and the question that flushes it out.

## Numbers that aren't there

**The unquantified superlative.** "Fast", "scalable", "secure", "high availability", "real-time", "huge volumes." Every one is a quality requirement with the number filed off.
→ *Ask:* fast how? measured where, at what percentile? scalable to what, by when? "Real-time" meaning sub-second, or meaning not-batch?

**The number with no unit or no source.** "Up to 10,000 users": concurrent or total? per day or ever? "Handles large files": 10 MB or 10 GB? A number you cannot act on is worse than no number, because it feels like certainty.
→ *Ask:* what is the unit, the time window, and where did this figure come from: measured, projected, or hoped?

**The missing peak.** Averages hide the requirement. A system sized for mean load falls over at the peak that actually matters.
→ *Ask:* what does the worst hour look like (the launch, the sale, the end-of-month run), and how far above normal is it?

## Requirements in disguise

**The solution masquerading as a need.** "We need a microservices architecture" / "use Kafka" / "it should be on Kubernetes." The client has pre-decided the mechanism and buried the requirement.
→ *Ask:* what problem is that meant to solve? Record the underlying requirement; treat the named technology as a constraint only if it is genuinely non-negotiable.

**The feature with a quality hidden inside.** "A live dashboard", "instant search", "offline mode", "export everything." Each implies latency, freshness, concurrency, or volume requirements the feature name doesn't state.
→ *Ask:* how fresh, how fast, how many at once, how much data?

**The throwaway business fact.** "We operate in the EU and the US", "Black Friday is our big day", "our competitors are faster." These are data-residency, peak-load, and performance requirements dressed as context.
→ *Ask:* treat every business fact as a possible requirement and check what it implies.

## Assumptions and silences

**The comfortable default.** The brief is silent on something important, and silence invites you to assume the easy case: one region, steady traffic, trusted users, small data, English only.
→ *Ask:* is this actually true, or am I assuming it because it's convenient? Label the assumption (see the pipeline's assumption discipline).

**The absent non-functional.** No mention of availability, security, backup/recovery, observability, or compliance. Absence rarely means "not needed"; it usually means "not thought about."
→ *Ask:* walk the ISO 25010 list (`quality-model.md`) and raise each silence as a question.

## Contradictions and impossibilities

**The quiet conflict.** Two requirements that cannot both be fully true: "strongly consistent across regions" and "sub-50 ms writes everywhere"; "keep everything forever" and "minimal storage cost"; "fully customisable" and "zero-config." These are the most dangerous smells because each requirement looks reasonable alone.
→ *Ask:* run the high-priority requirements through `feasibility-check.md` before designing.

**The impossible schedule.** The scope, the quality bar, and the deadline cannot coexist. Someone has to give, and better now than at the end.
→ *Ask:* which of scope, quality, or date is the real constraint, and which can move?

## How to use the smells

Don't just note a smell; convert it. Every smell becomes either a **sharpened requirement** (you got the answer), an **assumption** (you chose a reasonable default and labelled it), or a **question for the client** (you couldn't resolve it and it matters). The list of unresolved, high-impact questions is one of the most valuable things your analysis produces.
