## What it does

`supervise` takes responsibility for one task or issue through its acceptance criteria. The current ChatGPT/Codex desktop thread stays the supervisor, and each delegated ticket gets its own dedicated desktop thread. It checks their results and chooses what should happen next. The parent objective stays open until the actual outcome is verified, even when every repair task reports success.

## When to reach for it

Type `/supervise`, or the agent reaches for it automatically when you ask it to oversee work through completion. Supply the task link, issue, or an objective already established in the conversation.

| Your situation | Reach for |
| --- | --- |
| An issue needs someone to coordinate execution and verify completion | `supervise` |
| You want one current status report | Ask for a status check; this does not begin ongoing supervision |
| You want to reconsider the approach in one bounded pass | [reassess](https://aihero.dev/skills-reassess) |
| The effort is too uncertain to specify its execution yet | [wayfinder](https://aihero.dev/skills-wayfinder) |

## Prerequisites

The agent needs access to the target and its relevant work evidence. Delegated execution requires desktop task-control tools. It does not substitute [subagents](https://www.aihero.dev/ai-coding-dictionary/subagent) when those tools are missing. Scheduled monitoring needs a supported scheduler. Missing tools are reported as limits, and permissions come from your assignment.

It uses [reassess](https://aihero.dev/skills-reassess) when progress stalls. With that skill unavailable, it can still make a bounded comparison of the goal, evidence, and assumptions. Project-specific ticketing and completion conventions continue to apply.

## Own the outcome

The useful unit of progress is an observed advance toward acceptance. A worker may fix a defect and pass its tests while the overall workflow still fails before reaching the repaired behavior. The supervisor checks that gap before launching another attempt.

It keeps the next assignment small enough to finish and clear enough to judge. Independent work can run concurrently. Evidence and unresolved obstacles follow the work into replacement tasks, so starting a fresh conversation does not erase a recurring problem.

## Common questions

**Does each GitHub ticket get its own desktop thread?**

Yes. It creates or reuses one dedicated, user-visible desktop task per delegated ticket, including small tickets, and records which thread owns which issue. Subagents do not replace those tasks. Independent tickets can run concurrently; blocked tickets wait for their prerequisites.

Your explicit request or standing instruction to use dedicated threads carries forward without another confirmation for each ticket. If the tool requires authorization that has not been given, the supervisor asks once before creating the tasks. Work already started in subagents is handed over with its changes and evidence preserved.

**Which model and reasoning effort will the workers use?**

Before dispatching the first worker, it asks once, with **Sol / Medium** as the default choice. You can choose another supported pair. If you already specified settings for this assignment, it preserves them and asks only for any missing setting. The selected pair carries forward across tickets; you can change it later without changing the supervisor's own model or interrupting already-running workers.

**Will supervision continue after I leave?**

A saved goal or scheduled monitoring uses the application's supported controls when you ask for it. Dedicated worker threads make their work visible and separately manageable, but the skill alone does not provide background execution or wake the supervisor again.

**Who closes the issue, and where do blocking questions go?**

The supervisor follows the project's completion convention and your authorization. If closure requires a merge or delivery, a worker's local commit is not enough. Questions already answered by your requirements go back to the worker with that answer. New human decisions come to you with the concrete choice, while independent authorized work continues.

## It's working if

- You can see what is verified, who owns active work, and what happens next.
- Each delegated ticket has its own visible desktop thread, linked from the existing work record.
- You choose the worker model and effort once, with Sol / Medium offered by default.
- Worker results are checked against the parent objective before the next assignment starts.
- Repeated failures cause the approach to be reconsidered rather than another unexplained retry.
- A pause names the missing decision or prerequisite and preserves the next action.
- Completion includes evidence for the requested outcome, including delivery when required.

## Where it fits

`supervise` is a reach-for-it-anytime standalone for coordinating execution. [wayfinder](https://aihero.dev/skills-wayfinder) resolves a route through uncertain decisions; supervision can carry an authorized execution effort forward once its next step is clear. [reassess](https://aihero.dev/skills-reassess) supplies the bounded strategy check when progress stalls. [ask-matt](https://aihero.dev/skills-ask-matt) routes over the whole set.
