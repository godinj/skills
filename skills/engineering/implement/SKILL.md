---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

When repeated local fixes stop producing progress, results contradict the approach's assumptions, or repair tasks pass while the required behavior remains blocked, call the Skill tool with "reassess" before the next attempt. Resume implementation from its verdict within the agreed scope and seams; bring any required change to an explicit user decision back to the user.

Once done, use /code-review to review the work.

Commit your work to the current branch.
