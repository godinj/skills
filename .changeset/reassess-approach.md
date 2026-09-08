---
"mattpocock-skills": minor
---

Add a model-invoked `reassess` skill for reassessing progress and working assumptions during ongoing work. Agents can reach for it autonomously, and `implement` and `wayfinder` now call it when progress stalls or evidence challenges the approach. Each reassessment ends with a verdict and a concrete next step within the user's scope.

For repeated repair cycles, the coordinator checks whether local repair evidence predicts progress through the actual workflow before dispatching another repair or attempt. It distinguishes fixture-supplied answers from behavior the real actor must produce, preserves recurring obstacles across tasks, and can reconsider chosen mechanisms within existing authority.

The skill lives in the productivity bucket and includes both harness metadata and human-facing documentation. It retains "zoom out" as a discovery trigger; the removed `zoom-out` skill mapped unfamiliar code rather than reassessing ongoing work.
