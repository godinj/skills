---
name: reassess
description: Reassess the approach and mental model behind work already underway. Use when the user asks to reassess, zoom out, or reconsider the approach, local fixes stop producing progress, a previously working approach regresses after redesign, evidence contradicts a working assumption, or repair tasks succeed while the overall goal remains stuck.
---

# Reassess

Interrupt tunnel vision. Reconstruct the problem from the user's goal and the evidence, then decide whether to continue, adjust, or replace the approach, or separate its uncertainties into testable subgoals.

## When to reach for it

Use this autonomously when you observe:

- Repeated fixes around the same detail without improved results or new information.
- A result that contradicts an assumption the current approach depends on.
- A previously working capability becomes unreliable after changes to its design or workflow.
- Completed steps or growing supporting work whose contribution to the overall goal is unclear, including successful repair tasks followed by repeated failure at the same stage.

Long-running work offers useful checkpoints after a meaningful result or before another costly attempt. Look for those signals there; elapsed time, a routine failed test, or the existence of another possible design alone does not warrant a reassessment. Honour an explicit user request even when the approach appears healthy.

## Reassess

Pause the next local edit or retry while you do one bounded pass:

1. **Recover the goal.** Read the original request and subsequent user decisions, plus the current spec or map when present. State the required outcome and its success criteria separately from the means chosen to achieve it. In a long effort, distinguish the current step's objective from the overall destination. Treat agent-authored plans as interpretations; if essential context is missing, name the gap rather than reconstructing it as fact.
2. **Account for progress.** Inspect the relevant work and results. Summarize the current approach, what it has established, and what remains unexplained. Distinguish activity from progress toward the success criteria. Use existing evidence first and fetch only what bears on the questionable assumption. Choose and state the assessment level using the guidance below.
3. **Challenge the model.** State the assumption that makes the current approach seem promising and what would disprove it. Check the whole problem's constraints, dependencies, and required behaviour. Identify assumptions shared by repeated failed attempts. Before recommending a smaller goal or further decomposition, distinguish difficulty inherent in the problem from complexity introduced by the solution. Where the evidence warrants it, compare a plausible alternative explanation or approach; include continuing the current approach as a real candidate. Effort already spent is not evidence that an approach is correct.
4. **Choose the next move.** Decide to continue, adjust, or replace the approach, or decompose tangled uncertainties into testable subgoals using the guidance below. If the evidence cannot distinguish the candidates, choose the smallest check that would change that decision, with the expected observations and a finite stop condition. Before an expensive attempt, check the next handoff as described below. Run a check if it is cheap and already authorized; otherwise leave it as the concrete next step. A missing decision or access can be the next step too.

## Choose the assessment level

Orient briefly to the overall goal, then locate where the work has been concentrated. Start at the narrowest level that can explain the observed pattern; these are scopes to choose among, not stages to exhaust in order.

| Level | What gets questioned | Example |
| --- | --- | --- |
| Local tactic | An immediate operation or implementation choice | Does this condition or retry address the symptom? |
| Approach | The algorithm, model, or strategy behind those choices | Can advancing this pointer safely discard candidates? |
| Interactions | How parts, actors, or stages fit together | Does the next actor receive and use the repair's feedback? |
| Problem framing | The decomposition, assumed constraints, and chosen architecture | Have added responsibilities made the problem unnecessarily difficult? |
| Goal | The desired outcome, scope, and acceptance criteria | Is this the right first milestone, and what would make it practical? |

Repeated local patches usually warrant examining the approach; successful tasks followed by repeated overall failure warrant examining interactions. Start farther out when the evidence already implicates that level or the user requests it.

State the level and reason in one sentence, for example: "I'm reassessing the author-reviewer interaction because local repairs pass while the campaign repeatedly fails before implementation."

Move outward when an explanation depends on an untested assumption outside the chosen level, or fixes there keep reproducing the same failure. Stop widening once there is a supported explanation or a concrete check that distinguishes the alternatives, then return to the level where the next action belongs. A wider assessment expands what you examine, not your authority to change it.

## Compare with a working baseline

When an earlier approach worked, use it as a comparison:

- Establish what it actually handled and the evidence of success. Compare a representative workload and relevant constraints; an easier historical task does not establish a regression on today's task.
- Trace the responsibilities, representations, and handoffs added since then. For each addition implicated in the failure, identify the current requirement and consumer it serves. Look for machinery whose main purpose is supporting other added machinery.
- Consider restoring or simplifying the working approach alongside repairing the current one. Use a bounded comparison to test the suspected regression while preserving required safeguards; historical success alone does not justify a rollback.

## Decompose into testable subgoals

After checking for introduced complexity and a working baseline when available, consider decomposition when failures leave several uncertainties tangled together. Split into the smallest useful set of testable behaviors or questions, rather than defaulting to software modules or more repair tickets. For each subgoal, state:

- What it would establish toward the original goal, including any prerequisite assumptions.
- The smallest meaningful check and observable success or failure, using existing mechanisms where possible.
- How the result changes the next decision or action.

Retain a representative integration check: passing subgoals must compose under compatible assumptions and establish the original outcome. State what remains unproved. A smaller workload must not conceal an unresolved regression, and changing agreed acceptance criteria needs the user's decision.

Stop splitting once the next useful check and its dependencies are clear. Resume authorized work from that check. If the user wants the decomposition turned into tracked execution tickets, tell them to run `/to-tickets`, which is user-invoked.

## Repeated repair cycles

The coordinating agent owns reassessment across tasks. Before dispatching another repair or releasing another attempt, compare the furthest observed progress toward the goal with where attempts now stop. Local fixes can be correct while the overall strategy remains ineffective. Distinguish a strategy failure from an external capacity or access block, which may call for restoring a prerequisite or waiting.

State the next observable advance, the change expected to cause it, and the evidence connecting them. Check what a test supplied versus what the actual person, model, or component must discover or do. A manually corrected input or synthetic judgment can validate a mechanism without establishing that the real actor receives useful feedback and acts on it. A nearby reproduced defect is not necessarily the cause of the observed failure.

Choose the smallest check on the existing path that distinguishes the explanations. If only a full run can expose the uncertainty, make it one bounded experiment with a predicted observation and a result that would make repeating it unjustified. Reconsider agent-selected mechanisms within existing authority while preserving required outcomes and binding constraints. End with a supported next action or a specific decision needed to change course; additional evidence work must serve that decision.

## Check the next handoff

Before an expensive attempt, trace the next intended advance through the consumer that must accept its result. For example, successful worker startup may still leave completed work unable to pass admission because of incompatible resource limits or output requirements.

Inspect only prerequisites that could prevent that advance and are cheap to check using existing configuration, source, retained results, or focused checks. Establish which component enforces each relevant condition and how it interprets the values. The finding must change whether or how to proceed.

Resolve known contradictions within existing authority and name what remains uncertain; some questions require the real attempt. Stop when the next attempt is justified or a specific blocker is identified. Widen only when a directly related dependency requires it. This supports the next action, without requiring proof of every downstream stage or a new validation framework.

## Return to the work

Report briefly: **goal, evidence, verdict, next step**. Name the assumption retained or revised, and the observable result that will count as progress. Scale the explanation to the decision; a sound approach may need only a few sentences.

Resume authorized work at that next step. If the user requested assessment only, end with the recommendation. Preserve the user's scope, constraints, and explicit decisions; a change that requires revising them needs a specific user decision. When another skill invoked this one, return to its workflow and completion rules, including any planning-only, human-input, or per-session limits.

For work spanning sessions, put any changed assumption, unresolved obstacle, and next step into the existing work record used by the next session, when updating it is authorized. A new ticket or attempt does not reset a recurring obstacle. Keep evidence and uncertainty distinguishable there. Use the current ticket, map, or handoff rather than creating a separate tracking system.

This pass ends once there is a supported verdict or a concrete check or decision needed to obtain one. Reassess again only when new evidence, renewed lack of progress, or a user request warrants it. Keep useful work whose premises still hold.
