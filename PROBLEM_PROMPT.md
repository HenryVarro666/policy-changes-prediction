# Reusable problem-framing prompt

Read this repository's instructions, README, relevant implementation, and existing evidence. Explain the problem before describing the solution, using the repository's language. Keep the opening concise.

> **Under [real constraints], can [method or decision] improve [observable outcome] over [credible baseline], while preserving [important constraint]?**

Then explain:

- **Why it matters:** who encounters the failure, its concrete consequence, and what an answer would enable.
- **Central tension:** the useful objectives that may conflict, or the practical constraint. Label an unmeasured tradeoff as a hypothesis.
- **Current approaches and gap:** the closest credible approach and the specific missing evidence. Distinguish scientific novelty from unfinished engineering integration.
- **Hypothesis or design assumption:** an observable prediction and, when relevant, a plausible competing explanation.
- **Decisive test:** comparator, data split, controlled budget, primary metric, and a negative result that would change the plan.

Separate observed facts, external evidence, hypotheses, and unknowns. Do not invent results, benefits, throughput, novelty, or clinical/product efficacy. For requested novelty assessments, inspect primary papers and official implementations, record the search date, and bound the conclusion; a failed search is not proof that no prior work exists. A quick framing request does not require a full literature review.

Use engineering acceptance tests for engineering projects. Link a full research plan separately when requested. Preserve existing evidence, ownership disclosures, language variants, and document conventions. Modify only the authorized scope; framing alone does not authorize publication, deployment, or expensive training.

Start with this repository's [problem statement](PROBLEM.md). The conceptual checklist is informed by [DARPA's Heilmeier Catechism](https://www.darpa.mil/about/heilmeier-catechism). A personal Codex skill, when installed, can be invoked as `$frame-research-problem`; this prompt also works without that skill.
