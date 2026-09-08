---
name: reassess
description: Reassess the approach and mental model behind work already underway. Use when the user asks to reassess, zoom out, or reconsider the approach, repeated local fixes stop producing progress, evidence contradicts a working assumption, or repair tasks keep succeeding while the overall goal remains stuck.
---

# Reassess

Interrupt tunnel vision. Reconstruct the problem from the user's goal and the evidence, then decide whether to continue, adjust, or replace the current approach.

## When to reach for it

Use this autonomously when you observe:

- Repeated fixes around the same detail without improved results or new information.
- A result that contradicts an assumption the current approach depends on.
- Completed steps or growing supporting work whose contribution to the overall goal is unclear, including successful repair tasks followed by repeated failure at the same stage.

Long-running work offers useful checkpoints after a meaningful result or before another costly attempt. Look for those signals there; elapsed time, a routine failed test, or the existence of another possible design alone does not warrant a reassessment. Honour an explicit user request even when the approach appears healthy.

## Reassess

Pause the next local edit or retry while you do one bounded pass:

1. **Recover the goal.** Read the original request and subsequent user decisions, plus the current spec or map when present. State the required outcome and its success criteria separately from the means chosen to achieve it. In a long effort, distinguish the current step's objective from the overall destination. Treat agent-authored plans as interpretations; if essential context is missing, name the gap rather than reconstructing it as fact.
2. **Account for progress.** Inspect the relevant work and results. Summarize the current approach, what it has established, and what remains unexplained. Distinguish activity from progress toward the success criteria. Use existing evidence first and fetch only what bears on the questionable assumption.
3. **Challenge the model.** State the assumption that makes the current approach seem promising and what would disprove it. Check the whole problem's constraints, dependencies, and required behaviour. Identify assumptions shared by repeated failed attempts. Where the evidence warrants it, compare a plausible alternative explanation or approach; include continuing the current approach as a real candidate. Effort already spent is not evidence that an approach is correct.
4. **Choose the next move.** Decide to continue, adjust, or replace the approach using the evidence. If the evidence cannot distinguish the candidates, choose the smallest check that would change that decision, with the expected observations and a finite stop condition. Run it if it is cheap and already authorized; otherwise leave it as the concrete next step. A missing decision or access can be the next step too.

For example, repeated index changes in an algorithm may share the assumption that advancing a pointer can safely discard candidates. Check that invariant against the problem's inputs before patching another boundary condition. A counterexample can reject the algorithm; evidence that the invariant holds can justify returning to the local bug.

## Repeated repair cycles

The coordinating agent owns reassessment across tasks. Before dispatching another repair or releasing another attempt, compare the furthest observed progress toward the goal with where attempts now stop. Local fixes can be correct while the overall strategy remains ineffective. Distinguish a strategy failure from an external capacity or access block, which may call for restoring a prerequisite or waiting.

State the next observable advance, the change expected to cause it, and the evidence connecting them. Check what a test supplied versus what the actual person, model, or component must discover or do. A manually corrected input or synthetic judgment can validate a mechanism without establishing that the real actor receives useful feedback and acts on it. A nearby reproduced defect is not necessarily the cause of the observed failure.

Choose the smallest check on the existing path that distinguishes the explanations. If only a full run can expose the uncertainty, make it one bounded experiment with a predicted observation and a result that would make repeating it unjustified. Reconsider agent-selected mechanisms within existing authority while preserving required outcomes and binding constraints. End with a supported next action or a specific decision needed to change course; additional evidence work must serve that decision.

## Return to the work

Report briefly: **goal, evidence, verdict, next step**. Name the assumption retained or revised, and the observable result that will count as progress. Scale the explanation to the decision; a sound approach may need only a few sentences.

Resume authorized work at that next step. If the user requested assessment only, end with the recommendation. Preserve the user's scope, constraints, and explicit decisions; a change that requires revising them needs a specific user decision. When another skill invoked this one, return to its workflow and completion rules, including any planning-only, human-input, or per-session limits.

For work spanning sessions, put any changed assumption, unresolved obstacle, and next step into the existing work record used by the next session, when updating it is authorized. A new ticket or attempt does not reset a recurring obstacle. Keep evidence and uncertainty distinguishable there. Use the current ticket, map, or handoff rather than creating a separate tracking system.

This pass ends once there is a supported verdict or a concrete check or decision needed to obtain one. Reassess again only when new evidence, renewed lack of progress, or a user request warrants it. Keep useful work whose premises still hold.
