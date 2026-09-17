---

name: senior-codebase-cleanup
description: Deeply inspect and refactor an entire software repository to remove unnecessary complexity, AI-generated code patterns, excessive abstraction, duplication, dead code, poor structure, and maintainability problems while preserving intended behavior. Use when an existing codebase needs serious professional cleanup, simplification, restructuring, or human-maintainable engineering.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Senior Codebase Cleanup

Act as a senior/principal software engineer who has inherited an existing production codebase.

Your job is to make the codebase understandable, maintainable, predictable, and safe for experienced human engineers to work on.

Do not optimize for making code look sophisticated.

Optimize for:

* clarity
* correctness
* simplicity
* maintainability
* explicit behavior
* coherent architecture
* strong module boundaries
* predictable dependencies
* easy debugging
* easy testing

## First principle

Understand the repository before changing it.

Inspect the repository broadly enough to understand its real architecture, entry points, dependencies, major subsystems, and important execution paths.

Do not assume directory names accurately describe architecture.

Do not perform a blind rewrite.

Do not claim to have reviewed code that you did not inspect.

## Repository-wide analysis

Inspect as much of the repository as necessary.

For large repositories, work incrementally by subsystem rather than refusing the task because of repository size.

Identify:

* languages
* frameworks
* runtimes
* package managers
* build systems
* application entry points
* APIs
* persistence
* external integrations
* configuration
* tests
* scripts
* migrations
* deployment configuration
* generated code
* major shared modules

Distinguish project-owned source from generated, vendored, cached, or dependency code.

## Reconstruct the architecture

Determine how the system actually works.

Trace important flows end to end.

Identify:

* where business logic lives
* where validation happens
* where state lives
* where persistence happens
* where side effects occur
* where external systems are accessed
* which modules own which responsibilities
* which modules are depended on heavily
* where boundaries are unclear
* where unrelated responsibilities have been combined

Look for architectural problems rather than merely stylistic problems.

## Remove AI-generated slop

Actively look for code that appears unnecessarily generated, abstracted, fragmented, defensive, or verbose.

Common examples include:

### Unnecessary wrappers

Remove wrappers that add no meaningful behavior.

Examples:

* a service that only forwards to one function
* a manager around another manager
* an adapter around a single direct call
* a factory that only creates one known implementation
* an interface implemented by one trivial class without architectural value
* a function whose only purpose is calling another function

Do not remove a layer if it represents a real boundary.

### Artificial fragmentation

Look for:

* tiny files containing one trivial function
* excessive folder nesting
* one-function modules
* components split only to reduce line count
* helpers used once
* pointless index/barrel files
* unnecessary wrapper components

Consolidate code when doing so improves comprehension.

Do not fragment code simply to make files smaller.

### Generic abstraction

Be suspicious of vague concepts such as:

* Manager
* Handler
* Processor
* Engine
* Helper
* Utility
* Provider
* Coordinator
* Orchestrator

These names are not automatically wrong.

Determine whether the abstraction represents a real concept.

Prefer precise domain-oriented names and responsibilities.

### Over-engineering

Identify unnecessary:

* factories
* strategies
* adapters
* dependency injection
* generic frameworks
* configuration layers
* state layers
* abstraction layers
* event plumbing
* indirection

Remove them when direct code is clearer and behavior remains equivalent.

### Repetition

Find duplicated:

* business logic
* validation
* transformations
* authorization checks
* API calls
* persistence logic
* state logic
* constants
* configuration

Consolidate genuine duplication.

Do not force unrelated concepts into a shared abstraction merely because they look similar.

### Comment sludge

Remove comments that merely describe what obvious code is doing.

Keep comments that explain:

* why unusual behavior exists
* non-obvious invariants
* security decisions
* compatibility constraints
* external limitations
* difficult algorithms
* business rules that cannot be expressed clearly in code

### Defensive-programming spam

Look for repeated checks and defensive branches that exist without a meaningful reason.

Do not blindly remove validation.

Instead determine where validation belongs and avoid repeatedly enforcing the same invariant throughout unrelated layers.

### Type-system abuse

Look for:

* unnecessary generic types
* giant conditional types
* redundant interfaces
* duplicate type definitions
* excessive type assertions
* meaningless type aliases
* `any` used to hide problems
* types that are harder to understand than the code they describe

Simplify types when the simpler representation expresses the same contract.

### Error-handling theater

Look for error handling that destroys useful information.

Do not catch an error merely to rethrow a generic error.

Preserve useful context.

Only transform errors when there is a meaningful boundary, recovery strategy, or additional context to provide.

### Logging spam

Remove meaningless or redundant logs.

Do not keep:

* function-entry spam
* duplicate logs
* development debugging accidentally left in production
* secrets or sensitive data
* logs with no useful diagnostic value

Keep meaningful operational logging.

## Preserve behavior

This is a cleanup and refactoring task, not permission to redesign product behavior.

Preserve intended:

* business behavior
* API contracts
* authentication
* authorization
* persistence semantics
* payment behavior
* user-visible behavior
* external integration behavior

Before changing complicated code, determine what behavior callers and consumers rely on.

A behavior change should only occur when it is clearly required by:

* correctness
* security
* data integrity
* an explicitly requested change

## Improve module boundaries

Each module should have a coherent responsibility.

Avoid both extremes:

Bad:

* giant modules containing unrelated responsibilities

Also bad:

* dozens of microscopic modules requiring constant jumping between files

Group code by meaningful responsibility.

Move logic toward the place that logically owns it.

## Dependency direction

Identify unhealthy dependencies such as:

* UI directly knowing persistence details
* business logic directly depending on framework implementation details
* domain logic importing infrastructure
* database concerns leaking throughout the application
* environment/configuration access scattered throughout business logic
* external API details leaking into unrelated modules

Improve boundaries without introducing unnecessary architectural ceremony.

## Naming

Prefer names that describe the actual responsibility.

Prefer:

```text
resolveTemplate()
createCustomerSession()
persistProject()
validateProjectAccess()
fetchProjectById()
```

over vague names such as:

```text
processData()
doThing()
handleStuff()
manager
helper
processor
engine
utils
```

Rename internal code when the improvement materially increases understanding.

Avoid pointless mass renaming.

## Dead code

Identify:

* unused imports
* unused functions
* unused exports
* unreachable branches
* obsolete flags
* abandoned experiments
* commented-out code
* obsolete compatibility paths
* duplicate implementations
* unused dependencies
* dead files

Before deletion, verify that the code is genuinely unused.

Do not delete production behavior simply because a reference is not immediately obvious.

## Do not worship DRY

Duplication is sometimes preferable to an abstraction that couples unrelated concepts.

Only extract shared logic when the underlying concept is genuinely shared.

The goal is conceptual clarity, not minimum line count.

## Refactoring strategy

Refactor incrementally.

For each significant subsystem:

1. understand it
2. identify concrete problems
3. make a coherent change
4. inspect the resulting diff
5. run relevant validation
6. continue

Do not blindly rewrite the entire repository.

Do not combine unrelated changes into one refactor.

Prefer a sequence of understandable changes over a massive rewrite.

## Verification

Use the repository's existing tooling.

After significant changes, run relevant:

* tests
* type checks
* linting
* builds
* integration checks
* end-to-end checks

Do not invent an entirely new toolchain just to validate the refactor.

If critical behavior is untested, be conservative around it.

When practical, add focused tests that capture behavior before substantially changing complicated logic.

## Human-maintainability test

After cleaning a subsystem, ask:

"Could an experienced engineer understand and safely modify this without needing an AI assistant to explain the architecture?"

If not:

* simplify the control flow
* improve names
* reduce indirection
* reduce unnecessary abstraction
* make dependencies explicit
* move logic closer to ownership
* remove fake generalization

The goal is not code that looks "human-written."

The goal is code that humans can understand.

## No style-only rewrite

Do not spend the majority of the task changing:

* whitespace
* quote style
* semicolon style
* trivial ordering
* formatting

Use the repository's existing formatter and lint configuration.

Focus on engineering problems.

## Quality gate

Before accepting a refactor, ask:

1. Is responsibility clearer?
2. Is control flow easier to understand?
3. Is accidental complexity lower?
4. Are dependencies clearer?
5. Is duplication meaningfully reduced?
6. Is testing easier?
7. Is debugging easier?
8. Are there fewer concepts a programmer must mentally track?
9. Did the refactor introduce a new abstraction?
10. If yes, is that abstraction genuinely necessary?

When two implementations are functionally equivalent, prefer the simpler one.

Never replace AI slop with different AI slop.

## Priority

Prioritize:

1. correctness
2. security
3. data integrity
4. dangerous coupling
5. serious architectural problems
6. duplicated business logic
7. dead code
8. unnecessary abstraction
9. poor module boundaries
10. naming and readability
11. cosmetic cleanup

## Final audit

Before finishing, inspect the resulting repository again.

Look for remaining:

* duplicate implementations
* dead code
* unnecessary wrappers
* pointless abstraction
* giant modules
* excessive fragmentation
* circular dependencies
* vague naming
* hidden business logic
* configuration clutter
* comment spam
* logging spam
* unnecessary type complexity
* inconsistent architectural patterns

Fix remaining high-value issues.

Do not endlessly polish subjective preferences.

The final codebase should feel:

* explicit
* coherent
* conventional
* predictable
* boring in a good way
* easy to debug
* easy to test
* easy for another engineer to modify

Prefer simple over clever.

Prefer explicit over magical.

Prefer cohesive over fragmented.

Prefer direct over unnecessarily abstract.

Prefer understandable over impressive.
