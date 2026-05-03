# Reference

## Dependency Categories

When assessing a candidate for deepening, classify its dependencies:

### 1. In-process

Pure computation, in-memory state, no I/O. Always deepenable — just merge the modules and test directly.

### 2. Local-substitutable

Dependencies that have local test stand-ins (e.g., PGLite for Postgres, in-memory filesystem). Deepenable if the test substitute exists. The deepened module is tested with the local stand-in running in the test suite.

### 3. Remote but owned (Ports & Adapters)

Your own services across a network boundary (microservices, internal APIs). Define a port (interface) at the module boundary. The deep module owns the logic; the transport is injected. Tests use an in-memory adapter. Production uses the real HTTP/gRPC/queue adapter.

Recommendation shape: "Define a shared interface (port), implement an HTTP adapter for production and an in-memory adapter for testing, so the logic can be tested as one deep module even though it's deployed across a network boundary."

### 4. True external (Mock)

Third-party services (Stripe, Twilio, etc.) you don't control. Mock at the boundary. The deepened module takes the external dependency as an injected port, and tests provide a mock implementation.

## Testing Strategy

The core principle: **replace, don't layer.**

- Old unit tests on shallow modules are waste once boundary tests exist — delete them
- Write new tests at the deepened module's interface boundary
- Tests assert on observable outcomes through the public interface, not internal state
- Tests should survive internal refactors — they describe behavior, not implementation

## Architecture Friction Score

Score the current repo state from **0 to 100**, where **100 means no meaningful architectural friction** and **0 means severe friction that blocks safe change**. The score should communicate significance before implementation begins, not create false precision.

Use this rubric:

- **90-100**: Architecture is deep, local, and easy to test. Improvements are polish or isolated cleanup.
- **75-89**: Healthy architecture with some shallow modules or awkward seams. Deepening opportunities are useful but not urgent.
- **60-74**: Noticeable friction. Understanding common changes requires bouncing across modules, and tests do not always match real behavior.
- **40-59**: High friction. Important concepts are spread across shallow modules, seams leak implementation detail, and changes carry integration risk.
- **20-39**: Severe friction. Callers coordinate too much behavior, boundaries are unclear, and test coverage provides weak safety for refactors.
- **0-19**: Critical friction. The architecture actively blocks safe change; deepening work should start with the smallest high-confidence seam.

Deduct mainly for:

- Shallow modules whose interfaces are nearly as complex as their implementations
- Concepts split across many files without a deep owning module
- Tests that force internal knowledge instead of exercising a stable interface
- Leaky seams where callers must understand ordering, invariants, or dependency setup
- Duplicate orchestration logic across callers
- Hard-to-substitute dependencies that prevent realistic boundary tests

Do not overfit the score to file count, test count, language, or style. A small codebase can have severe friction; a large codebase can score well if concepts are deep and local.

## Implementation Summary Template

Use this template in the final response after implementing the selected concurrent subset. Do not file it with GitHub.

<implementation-summary-template>

## Problem

Describe the architectural friction:

- Starting architecture friction score and confidence
- Which modules are shallow and tightly coupled
- What integration risk exists in the seams between them
- Why this makes the codebase harder to navigate and maintain

## Final Interface

The implemented interface design:

- Interface signature (types, methods, params)
- Usage example showing how callers use it
- What complexity it hides internally

## Dependency Strategy

Which category applies and how dependencies are handled:

- **In-process**: merged directly
- **Local-substitutable**: tested with [specific stand-in]
- **Ports & adapters**: port definition, production adapter, test adapter
- **Mock**: mock boundary for external services

## Testing Strategy

- **New boundary tests to write**: describe the behaviors to verify at the interface
- **Old tests to delete**: list the shallow module tests that become redundant
- **Test environment needs**: any local stand-ins or adapters required

## Concurrent Execution

- **Implemented candidates**: list the independent candidates completed in parallel
- **Skipped candidates**: list candidates not selected for concurrent implementation and why
- **Conflict checks**: note any shared files, naming overlap, or sequencing concerns reviewed during integration

## Implementation Recommendations

Durable architectural guidance that is NOT coupled to current file paths:

- What the module should own (responsibilities)
- What it should hide (implementation details)
- What it should expose (the interface contract)
- How callers should migrate to the new interface

</implementation-summary-template>
