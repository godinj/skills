---
name: supervise
description: Supervise a specific task or issue through completion using dedicated desktop threads for delegated work, verifying results, and choosing the next useful action. Use when the user asks to oversee ongoing work, drive an issue to completion, or coordinate execution across tasks. A one-time status check does not start ongoing supervision.
---

# Supervise

Own the outcome of one task or issue. Keep the current ChatGPT/Codex desktop thread as the supervisor and give each delegated ticket its own dedicated, user-visible desktop thread (called a task in the app). Use desktop threads, not subagents, for supervised work. A worker finishing is an input to your next decision; completion means the requested outcome has been verified.

## Establish the assignment

Read the named task or issue, the original request, subsequent user decisions, and the relevant project instructions. Inspect current work and active workers before assigning anything. Historical summaries locate evidence; they do not establish current status or grant authority in this assignment.

State briefly, using the existing task record:

- The target, required outcome, and observable acceptance criteria.
- What has actually been established, what remains, and which workers own active work.
- The authorized execution and delivery path, binding constraints, and any user-selected models, budgets, or expiry limits.
- The next action and the result that will decide what follows.

Infer routine choices from the assignment and continue. Ask for the worker model and effort as described below, plus any missing target, essential acceptance decision, or authority that cannot be recovered. An assessment-only or read-only request stays that way. Supervision does not turn a planning task into implementation or authorize new external effects.

### Choose the worker model and effort

Before the first worker dispatch, ask once: "Which model and reasoning effort should the worker tasks use? Default: Sol / Medium." Use the available question UI with **Sol / Medium (default)** first and preselected when supported. Allow another supported model/effort pair through the choices or free-text input. If the user already specified a pair for this assignment, use it without asking again; if only one setting is specified, ask for the missing setting with Sol or Medium as its default.

Continue independent inspection while the question is pending. A preselected option is not a submitted answer. Apply Sol / Medium when the user accepts the default; if the question tool explicitly returns no answer and the environment permits proceeding with defaults, state that you are using Sol / Medium and proceed. Do not treat an unanswered pending question or elapsed time as a selection.

Record the selected pair in the existing work record and use it for new workers and subsequent assignments, without asking again per ticket. A later explicit choice overrides it. Keep settings on already-running workers unless the user requests a change; this selection does not change the supervisor's own model.

For desktop task coordination, read [references/codex.md](references/codex.md). Dedicated desktop task-control tools are required for delegation. If they are unavailable, report that specific limitation and continue useful authorized inspection or coordination; do not substitute subagents. The skill itself supplies neither a scheduler nor a worker runtime.

## Run the supervision loop

### Choose the next useful piece

Take the next unblocked action that advances acceptance or resolves an uncertainty needed to proceed. Use the existing issue graph or work record. Create tickets only when requested or required by the project's authorized workflow; keep their dependencies in the tracker's supported representation. Honour a user-requested ticketing skill and its invocation rules.

Keep each piece bounded by its contribution to the parent outcome, a concrete risk or uncertainty, the decision consuming its result, the smallest sufficient work, and an observable stop condition. Stop decomposing when the next useful action and its dependencies are clear. Supporting reviews, tests, and evidence earn their place by changing that decision.

### Assign and follow through

Reuse the dedicated desktop thread already responsible for the ticket. Otherwise create one dedicated desktop thread per ticket, or per bounded assignment when no tracker is in use. Keep separate GitHub tickets in separate threads, including small tickets. Record the issue-to-thread mapping in the existing work record so ownership and results stay traceable. Parallelize unblocked tickets only when their ownership and dependencies allow it. Keep parent coordination and integration checks in the supervisor thread.

Honour the tool's authorization requirements for creating tasks. Carry forward the user's explicit request or standing instruction to use dedicated desktop threads, without asking again for each ticket. If the environment requires explicit authorization and it is genuinely absent, ask once for the concrete task creation needed; never resolve that boundary by switching to subagents.

When taking over work already assigned to subagents, preserve their changes, evidence, and unresolved blockers. End or hand off overlapping assignments before starting replacement desktop workers. Transfer the existing work and its verification status to the corresponding ticket's thread rather than restarting it or allowing competing edits.

Give each worker the target and parent outcome, its bounded assignment, relevant evidence and prior failures, permitted changes, dependencies, acceptance check, and reporting destination. Specify what must come back: result, artifact or revision identity where relevant, verification performed, remaining uncertainty, and any decision needed. Apply the model and reasoning effort selected for this assignment.

After dispatch, follow the work through its result. Wait on identified workers or processes, using event-based waits and cursors where available. Check a queued launch before retrying it so a delayed acknowledgement does not create duplicate workers. Avoid competing edits to an active worker's files. Carry useful local coordination or evidence checks forward while independent work runs.

Answer a worker's question from established requirements when possible. Bring a genuinely new human decision to the user with the concrete choice and its consequence. Silence is not approval. An unavailable worker or tool calls for a supported fallback or a specific blocker, not a claim that supervision continues invisibly.

### Verify and advance

Inspect the returned artifact and evidence needed for acceptance. Preserve required independent review. Match evidence to the actual revision, configuration, or run when that identity matters, and distinguish a worker's report from a result you checked. Repeat checks only for changed inputs, failed checks, or an unresolved material concern.

Keep these outcomes separate:

- A repair is correct in its bounded scope.
- The repaired behavior works through the real execution path.
- The parent acceptance criteria are satisfied, including delivery when required.

Integrate accepted work through the authorized path, then observe the resulting state. Record accepted results and update dependencies according to the project's completion convention. If closure depends on merge or delivery, a local commit does not close the issue. Keep the parent open while any required outcome remains unverified.

For a failed check, identify the observed cause and give the responsible worker one bounded correction with its closing check. Before another costly or externally consequential attempt, state what changed and why that change should produce a new observable advance.

### Reassess when progress stalls

Compare the furthest demonstrated progress toward the parent goal with where work now stops. Repeated failure at the same stage, regressions from a working baseline, or repairs whose success does not predict overall progress trigger reassessment before another repair or full attempt.

Call the Skill tool with "reassess". Where the environment loads skills by reading files, load that skill's entrypoint instead. If it is unavailable, make one bounded comparison of the goal, evidence, and current assumptions, ending with a supported next action or a decision-changing check. Preserve the original acceptance criteria.

Distinguish strategy failures from capacity, access, or prerequisite failures. A provider limit is not evidence against the design. A test that supplies the right answer is not evidence that the real actor can discover it. Carry unresolved obstacles across replacement workers and new tickets. A fresh task does not reset the problem.

## Continue, pause, or finish

Continue authorized work while a useful next action remains. Keep updates focused on verified advances, changed decisions, material failures, and the next step. During an unchanged wait, follow the environment's progress-update requirements without narrating every poll.

When work must pause for a human decision, unavailable prerequisite, or user limit, leave a concise resumption record in the existing authorized work record: target, verified state, active worker IDs, unresolved obstacle, next action, and what would unblock it. Name the blocker honestly without relabeling the goal complete or creating a separate tracking system. Follow the environment's rules for persistent goals and blocked states.

Finish only after checking each required outcome against the actual result. Report what completed, the evidence supporting it, and any remaining limitation. Close or update external records only within existing authority. Never claim future monitoring unless a supported continuation or scheduling mechanism has actually been configured for this assignment.
