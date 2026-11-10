# brief-to-architecture

A Claude skill that analyses a raw brief the way an architect does before estimating. It finds the requirements that shape the system, makes them testable and catches contradictions before anyone commits to an estimate.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude skill](https://img.shields.io/badge/Claude-skill-8A5CF6.svg)](https://docs.claude.com/en/docs/claude-code/skills)

## What it does

Hand Claude a brief, an RFP, discovery-call notes, or a feature spec, and this skill runs it through the analysis a software architect does before estimating or designing:

1. **Extract** the real requirements, including the ones hiding inside features and offhand business facts.
2. **Classify** them into functional, quality-attribute, and constraint, using the ISO/IEC 25010 quality model so nothing is missed.
3. **Sharpen** each into something unambiguous and testable, with its architectural implication.
4. **Prioritise** by business value and architectural impact, so you design hard for the few that matter.
5. **Check feasibility**: catch requirements that quietly contradict each other, including the arithmetic impossibilities.
6. **Specify** measurable quality scenarios and the design strategies (with their costs) that would meet them.

You can defend the analysis, so you can defend the estimate built on it.

## What it's built on

- **ISO/IEC 25010**: the international product-quality model, used to classify quality attributes and cover all of them.
- **Scenario-based quality specification**: turns adjectives ("fast", "reliable") into measurable scenarios.
- A practical catalogue of **brief smells**, a **feasibility-check** method (including the availability "nines" budget and arithmetic contradiction checks), and a map of **design strategies with their costs**.

This is an original work. The architecturally-significant-requirements concept and the scenario/tactics ideas it builds on are credited under [Further reading](#further-reading); no copyrighted templates, taxonomies, or text are reproduced here.

## Structure

```
SKILL.md                              the six-step pipeline and routing
references/
  asr-framework.md                    what makes a requirement architecturally significant
  quality-model.md                    the ISO/IEC 25010 quality characteristics
  brief-smells.md                     warning patterns in briefs and the questions they raise
  feasibility-check.md                logical + arithmetic contradiction checks; availability table
  scenarios-and-priorities.md         writing quality scenarios; prioritising them
  design-strategies.md                design approaches per quality attribute, with costs
  output-template.md                  structuring the written deliverable
```

## Install

**Claude Code (CLI):**

```bash
git clone https://github.com/vlaskos/brief-to-architecture.git \
  ~/.claude/skills/brief-to-architecture
```

Claude Code discovers skills under `~/.claude/skills/`. The skill activates when you ask it to analyse a brief, find what's architecturally significant, or assess requirements before estimating.

**Claude Desktop / claude.ai:** zip the skill folder and upload it as a skill in the app's skills/capabilities settings.

## Use it

Ask naturally, for example:

- "Analyse this brief. What's architecturally significant and what could go wrong?"
- "Is this set of requirements even feasible together?"
- "Turn these quality goals into testable scenarios and prioritise them."
- "What should I ask the client before I estimate this?"

## Further reading

- ISO/IEC 25010, *Systems and software engineering — SQuaRE — Product quality model.*
- Chen, Ali Babar & Nuseibeh, "Characterizing Architecturally Significant Requirements," *IEEE Software* 30(2), 2013.
- Bass, Clements & Kazman, *Software Architecture in Practice* (4th ed., Addison-Wesley), the reference for quality-attribute scenarios, utility trees and the architectural-tactics catalogue.

## License

[MIT](LICENSE) © 2026 Vladyslav Kosyi
