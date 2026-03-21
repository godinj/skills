---
name: repo-audit
description: Run a full-repo quality audit covering constitution constraints, test coverage, ARCHITECTURE.md adherence, deep module interfaces, and human documentation coverage. Use when user wants a quality check, repo audit, constitution check, or mentions "audit", "quality gate", or "repo health".
---

# Repo Audit

Full-repo quality audit across five dimensions. Each dimension produces a PASS/FAIL verdict with details.

## Workflow

Run all five checks, then present a unified report. Use parallel agents for independent checks.

### 1. Constitution Constraints

Run the constraint checker and report results:

```bash
cd "$(git rev-parse --show-toplevel)" && bash scripts/check_constitution.sh
```

If the script fails, capture the output and report each failing constraint by name with the violation details.

**Verdict**: PASS if exit code 0, FAIL otherwise.

### 2. Test Coverage

Run tests with coverage across all packages:

```bash
go test -cover ./...
```

For each package, extract the coverage percentage. Flag any package below 60% coverage. Report the repo-wide average.

**Verdict**: PASS if all packages have coverage output and average >= 60%, FAIL otherwise.

### 3. ARCHITECTURE.md Adherence

Read `ARCHITECTURE.md` and verify the repo matches what it describes:

- [ ] **Package map accuracy** — every directory under `internal/` and `cmd/` is listed in the Package Map section; no listed package is missing from disk
- [ ] **Enforced rules hold** — for each rule marked `[enforced]`, confirm the corresponding constraint exists in `.drem/constraints.toml`
- [ ] **Grandfathered files shrinking** — for each `shrink-only` exception in `constraints.toml`, check that the current metric (line count, export count, import count) is at or below the baseline

**Verdict**: PASS if all sub-checks pass, FAIL with specific drift listed.

### 4. Deep Module Interfaces

Evaluate module depth across all `internal/` packages:

- [ ] **Export ratio** — for each package, count exported symbols vs total symbols in non-test `.go` files; flag any package exceeding 15% export ratio (unless grandfathered in `constraints.toml`)
- [ ] **Pass-through functions** — identify functions that simply delegate to another package with no added logic; flag any package with more than 3 pass-throughs (unless grandfathered)
- [ ] **Interface placement** — check that interfaces are defined at consumption sites, not provider sites (per ARCHITECTURE.md "Interfaces at consumption sites" rule)

**Verdict**: PASS if no non-grandfathered violations, FAIL with specific packages listed.

### 5. Human Documentation Coverage

Check that user-facing documentation is current:

- [ ] **README.md exists and is non-empty** at repo root
- [ ] **README sections match repo capabilities** — every package in `internal/` that defines exported types or functions should have a corresponding section or mention in README.md
- [ ] **docs/ directory** — check that feature documentation in `docs/` covers major subsystems (constraints, scoring, orchestrator, memory, merge)
- [ ] **No stale references** — grep README.md and docs/ for references to files, functions, or packages that no longer exist

**Verdict**: PASS if docs exist and no stale references found, FAIL with gaps listed.

## Report Format

Present results as a table:

```
| Dimension        | Verdict | Details                          |
|------------------|---------|----------------------------------|
| Constitution     | PASS    | 12/12 constraints pass           |
| Test Coverage    | FAIL    | avg 58%, agent/ at 32%           |
| Architecture     | PASS    | package map current              |
| Deep Modules     | FAIL    | tui/ export ratio 100% (gf'd)   |
| Documentation    | PASS    | no stale refs                    |
```

After the table, list each FAIL dimension with actionable remediation steps.

## Parallelization

Checks 1, 2, and 5 are independent — run them as parallel agents. Checks 3 and 4 share ARCHITECTURE.md and constraints.toml reads, so run them together in a single agent.
