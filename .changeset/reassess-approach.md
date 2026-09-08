---
"mattpocock-skills": minor
---

Add a model-invoked `reassess` skill for reassessing progress and working assumptions during ongoing work. Agents can reach for it autonomously, and `implement` and `wayfinder` now call it when progress stalls or evidence challenges the approach. Each reassessment ends with a verdict and a concrete next step within the user's scope.

For repeated repair cycles, the coordinator checks whether local repair evidence predicts progress through the actual workflow before dispatching another repair or attempt. It distinguishes fixture-supplied answers from behavior the real actor must produce, preserves recurring obstacles across tasks, and can reconsider chosen mechanisms within existing authority.

The skill lives in the productivity bucket and includes both harness metadata and human-facing documentation. It retains "zoom out" as a discovery trigger; the removed `zoom-out` skill mapped unfamiliar code rather than reassessing ongoing work.

Before recommending a smaller goal, distinguish inherent problem difficulty from complexity introduced by the solution. Where a working baseline exists, compare representative capabilities and added responsibilities, and consider restoration or simplification without assuming a rollback is warranted. Any proposed smaller milestone names what it proves and leaves outstanding; changes to agreed acceptance criteria remain a user decision.

Allow decomposition into testable subgoals as a reassessment outcome. Each subgoal names its contribution, assumptions, observable check, and resulting decision. Retain an integration check for the original outcome and stop splitting once the next useful check and its dependencies are clear. Users can take the decomposition to `to-tickets` for tracked execution work.

Choose an explicit assessment level: local tactic, approach, interactions, problem framing, or goal. Start at the narrowest level that explains the observed pattern, state the reason, and widen when broader assumptions or repeated failure warrant it. Stop at a supported explanation or a discriminating check, then return to action within existing authority.

Before an expensive attempt, check cheaply inspectable prerequisites through the next result's accepting consumer. Resolve known contradictions, state remaining uncertainty, and stop when the attempt is justified or a specific blocker is found.
