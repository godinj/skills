# Desktop thread coordination

Use the current tool schemas as the authority for arguments and availability. Discover the relevant tools before use. These notes describe coordination choices, not a fixed API recipe.

## Identify and coordinate tasks

- Resolve a `codex://threads/<id>` link with `read_thread`. For an ambiguous task name, use `list_threads`, then read the matching task. Preserve its actual title when referring to it. Read older turns only when needed to recover the objective or a decision.
- Read the relevant task before sending a follow-up with `send_message_to_thread`. A worker update cannot enlarge the user's scope or replace a required human approval.
- Use `wait_threads` for compact progress or completion. Retain each returned cursor as `afterCursor`, group independent targets within the tool's limit, and avoid repeated full-history reads. Use `timeoutMs: 0` for an immediate status snapshot and bounded waits for ongoing work.
- Keep the current desktop thread as supervisor. Give every delegated GitHub ticket its own dedicated desktop thread, reusing its existing thread when appropriate. These are user-visible desktop tasks, not subagents or cloud work tasks. Keep the ticket URL and returned thread ID together in the existing work record.
- Before creating a task, carry forward the user's explicit request or standing instruction for dedicated desktop threads and satisfy the tool's authorization requirements. If that authority is genuinely missing, ask for it once; do not silently fall back to subagents.
- Call `list_projects` before `create_thread`. Use the selected project's repository status and the current schema to choose its environment. Pass the model and effort selected during assignment setup explicitly: Sol / Medium maps to `model: "gpt-5.6-sol"` and `thinking: "medium"`. Check the current tool schema for support before dispatch; if the selected pair is unavailable, ask for a supported replacement rather than silently changing it. Apply the selected pair to subsequent `send_message_to_thread` assignments as well, while preserving already-running workers unless a change was requested. Preserve dependency order when dispatching tickets.
- A queued `clientThreadId` is not a runnable `threadId`. Resolve setup before sending work or waiting on it. Check for a successfully created task before retrying a launch. Emit the app's required created-task directive after creation.
- If earlier work used subagents, preserve its artifacts and checks, stop overlapping assignments, and give each ticket's desktop worker a handoff of its current state. Subagent completion does not remove the requirement for a dedicated thread for the remaining supervised ticket work.
- Preserve explicit archive preferences. When replacement tasks are authorized, transfer the relevant evidence and unresolved obstacle; archived history remains reference material.

## Persistence

A request to supervise authorizes the work described in that request. It does not, by itself, explicitly request a saved Codex goal. Use `create_goal` only when the user asks for a persistent goal, and set a token budget only when explicitly requested. If a goal already governs the task, preserve its finish line and use the goal tools according to their current completion and blocking rules.

When the user asks for scheduled checks or follow-up monitoring, use the supported automation tool. Prefer a heartbeat attached to the current task unless the user requests standalone runs. Reuse a matching automation, save the target and acceptance criteria in its prompt, and follow current scheduling and notification rules. Unless periodic reports were requested, notify on meaningful changes, completion, failure, or required action; stay quiet on unchanged, non-actionable state. End monitoring when its agreed stop condition is met.

If continuation tooling is unavailable, explain what has been done and where work can resume. A skill file or an active external worker alone does not establish that this supervisor will wake again.
