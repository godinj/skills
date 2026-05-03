---
name: improve-codebase-architecture
description: Explore a codebase to find and implement architecture improvements by deepening shallow modules, preferably as independent concurrent refactors. Use when user wants to improve architecture, find refactoring opportunities, consolidate tightly-coupled modules, make a codebase more testable, or make it more AI-navigable.
---

# Improve Codebase Architecture

Explore a codebase like an AI would, score current architectural friction, surface opportunities for improving testability, and implement a compatible subset of module-deepening refactors concurrently with subagents.

A **deep module** (John Ousterhout, "A Philosophy of Software Design") has a small interface hiding a large implementation. Deep modules are more testable, more AI-navigable, and let you test at the boundary instead of inside.

## Process

### 1. Explore the codebase

Use the Agent tool with subagent_type=Explore to navigate the codebase naturally. Do NOT follow rigid heuristics — explore organically and note where you experience friction:

- Where does understanding one concept require bouncing between many small files?
- Where are modules so shallow that the interface is nearly as complex as the implementation?
- Where have pure functions been extracted just for testability, but the real bugs hide in how they're called?
- Where do tightly-coupled modules create integration risk in the seams between them?
- Which parts of the codebase are untested, or hard to test?

The friction you encounter IS the signal.

### 2. Score current architectural friction

Before proposing changes, give the repo's current architecture a score from **0 to 100**, where **100 means no meaningful architectural friction** and **0 means severe friction that blocks safe change**. This score is a judgment call, not a metric dump. Ground it in the exploration evidence and use [REFERENCE.md](REFERENCE.md) for the scoring rubric.

Present the score before the candidate list:

- **Architecture friction score**: `N/100`
- **Confidence**: low, medium, or high, based on how much of the repo was explored
- **Main deductions**: the 3-5 biggest sources of friction that lowered the score
- **What would move the score most**: the deepening opportunities likely to produce the largest improvement

Use the score to calibrate urgency. A low score means prefer fewer, higher-leverage candidates with strong tests. A high score means only implement candidates whose payoff is clearly worth the churn.

### 3. Present candidates and choose a concurrent subset

Present a numbered list of deepening opportunities. For each candidate, show:

- **Cluster**: Which modules/concepts are involved
- **Why they're coupled**: Shared types, call patterns, co-ownership of a concept
- **Dependency category**: See [REFERENCE.md](REFERENCE.md) for the four categories
- **Test impact**: What existing tests would be replaced by boundary tests
- **Concurrency fit**: whether it can be implemented alongside the other candidates without touching the same files, changing the same public interfaces, or depending on the same migration sequence

Select a subset of candidates that can be implemented simultaneously. Prefer 2-4 candidates that are independent by file ownership, module ownership, public interface changes, migrations, generated files, and test fixtures. Exclude any candidate that creates ordering dependencies or likely merge conflicts.

If the independent subset is obvious and low-risk, proceed without asking. If there are multiple plausible subsets or a candidate has product/design implications, ask the user which subset to implement.

### 4. Frame each selected problem space

Before spawning implementation subagents, write a concise user-facing explanation of the selected subset:

- Why these candidates are safe to implement concurrently
- The constraints each new interface would need to satisfy
- The dependencies each candidate would need to rely on
- The verification command each subagent should run for its slice

Show this to the user, then immediately proceed to Step 5. The user reads and thinks about the subset while the subagents work in parallel.

### 5. Implement selected candidates concurrently

Spawn one implementation subagent per selected candidate in parallel using the Agent tool. Each subagent owns exactly one candidate and must make the smallest correct code change for that candidate.

Prompt each subagent with a separate technical brief:

- Candidate description and file/module ownership
- Coupling details and dependency category
- What complexity should move behind the deepened interface
- Which files are in scope and which concurrent candidates are out of scope
- Required tests to add, update, or delete according to the replace-don't-layer testing strategy
- Verification command for the slice
- Instruction to stop and report if the slice overlaps another candidate or requires a sequencing decision

Each implementation subagent must:

1. Implement the refactor for its candidate.
2. Add or update boundary tests for the deepened interface.
3. Delete or update redundant shallow-module tests only when the new boundary tests replace them.
4. Run the assigned verification command.
5. Return a summary of changed files, the final interface, testing changes, verification result, and any follow-up risk.

### 6. Integrate and verify

After all subagents finish, review their changes together for conflicts, duplicated abstractions, inconsistent naming, and test overlap. Resolve integration issues directly when they are mechanical. If two candidates made incompatible architecture choices, stop and ask the user which direction to keep.

Run the relevant full verification for the touched area, not only each subagent's slice command. Summarize:

- Implemented candidates
- Candidates intentionally skipped from the original list and why
- Starting architecture friction score and expected score movement from the implemented changes
- Final interface changes
- Tests added, updated, or removed
- Verification results
- Remaining risks or follow-up candidates

Do not create GitHub issues, pull requests, or any other GitHub artifact. This skill's output is local code changes plus a final implementation summary.
