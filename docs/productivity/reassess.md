## What it does

`reassess` reassesses whether work already underway is advancing the user's goal and whether the assumptions behind the approach still hold. It checks the original request against the work and its results, then returns a verdict and one concrete next step.

Continuing the current approach is a valid outcome. A change of direction needs evidence, and the user's goal remains the reference point throughout.

## When to reach for it

Type `/reassess`, or the agent reaches for it automatically when a task fits. It is useful during code work, research, and planning, including long efforts started with [implement](https://aihero.dev/skills-implement) or [wayfinder](https://aihero.dev/skills-wayfinder).

| What you notice | What gets reassessed |
| --- | --- |
| The same few lines keep changing without better results | The assumption shared by those fixes |
| A result conflicts with what the plan assumes | Whether the current explanation or approach still fits the evidence |
| A capability used to work before redesigns or added workflow layers | What changed relative to a working baseline on a comparable task |
| Tasks keep getting completed but the goal feels no closer | How the current work contributes to the overall outcome |
| Repair tests pass but full attempts keep failing at the same stage | Whether the repair evidence predicts what the real actor will do next |

For a reproducible bug that needs a diagnosis workflow, use [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs). For an explanation that did not make sense, use [wait-what](https://aihero.dev/skills-wait-what).

## Interrupting tunnel vision

**Tunnel vision** can make every failed attempt look like a reason for another small patch. Suppose an algorithm keeps failing edge cases after several pointer adjustments. The useful question may be whether moving that pointer can safely discard candidates at all. Checking that assumption can reveal a flawed algorithm or justify returning to the local condition.

The reassessment stays bounded. When the evidence is inconclusive, it ends by identifying the smallest check that would distinguish the options. Useful work stays in place, and authorized work resumes from the resulting next step.

## Common questions

**What if this used to work before we redesigned it?**

That gives the agent a working baseline to investigate. It checks what the earlier approach actually handled, compares a representative task, and traces the added responsibilities and handoffs involved in the failure. Simplifying or restoring the approach becomes a candidate alongside repairing it, while required safeguards still apply. The comparison must support the suspected regression; an easier historical task is insufficient evidence.

**Should the goal just be broken into smaller pieces?**

First, the agent checks whether the difficulty belongs to the problem or was introduced by the solution. If independent uncertainties remain, it can propose a smaller meaningful milestone and explain what that milestone would prove and leave unfinished. Changing agreed acceptance criteria requires your decision. A smaller task must not hide a regression in a capability that previously worked.

**Why are repair tasks finishing while the overall goal stays stuck?**

A repair can work in isolation while the broader approach still fails. A test that supplies the correct input or judgment proves less than a run in which the real person, model, or component must produce it. The coordinating agent checks that gap before dispatching another repair or releasing another attempt: what should happen differently, what changed, and what evidence connects the two?

The next step is a small check using the existing path. If the uncertainty can only be exposed by a full run, that run is a bounded experiment with a predicted result and a reason to stop repeating it. An external capacity or access block can instead call for restoring a prerequisite or waiting. Reassessment can revisit chosen mechanisms while preserving the required outcome and binding constraints.

**Can an agent use this during a long-running goal without me asking?**

Yes. Both harnesses allow automatic invocation, and `implement` and `wayfinder` include explicit triggers for calling it. The trigger is stalled progress, contradictory evidence, or a weak connection between current work and the destination. Time spent alone is not a reason to interrupt healthy progress. Changed assumptions and the next step carry forward in the existing work record when updating it is authorized.

**How does this relate to the old `zoom-out` skill?**

The earlier user-invoked `zoom-out` skill mapped unfamiliar code's modules and callers. It was removed because it went unused. This version reassesses the direction of ongoing work and is available to agents as well as users.

## It's working if

- The agent identifies the original goal separately from the approach it chose.
- It names a specific assumption and shows which results support or challenge it.
- When an earlier approach worked, it compares actual capabilities and examines added complexity before recommending a smaller goal.
- When repairs pass but the goal stays stuck, the coordinator explains what should change in the real workflow before the next attempt.
- You get a clear verdict and a next step whose result will tell you something useful.
- The agent resumes authorized work without repeatedly reopening the same assessment.
- A proposed change to your requirements comes back to you as a decision.

## Where it fits

`reassess` is a reach-for-it-anytime standalone that can interrupt and return to an existing flow. [implement](https://aihero.dev/skills-implement) uses it to reassess stalled implementation; [wayfinder](https://aihero.dev/skills-wayfinder) uses it when evidence challenges the route to the destination. Their scope and completion rules still apply. [ask-matt](https://aihero.dev/skills-ask-matt) routes over the whole set.
