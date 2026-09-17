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

Actively look for code that appears unnecessarily generated, abstracted, fragmented, defensive, verbose, or over-engineered.

Use the detailed detection patterns in:

`references/ai-slop-patterns.md`

For each suspicious pattern:

1. determine whether it serves a real purpose
2. identify its consumers and dependencies
3. determine whether it represents a meaningful boundary
4. determine whether removing it could change behavior
5. prefer the simplest implementation that preserves the real responsibility

Do not refactor code merely because it looks unfamiliar or differs from your preferred style.

Do not assume every pattern in the reference is bad.

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

## Verification integrity

Never claim that behavior was preserved, functionality is working, or a change is fully verified unless the relevant behavior was actually inspected, tested, or otherwise directly verified.

Do not use absolute claims such as:

- "100% preserved"
- "everything still works"
- "fully verified"
- "no regressions"
- "all behavior is unchanged"

unless the evidence genuinely supports that claim.

When reporting results, distinguish clearly between:

### VERIFIED
Things directly confirmed through tests, builds, static analysis, execution, or inspection.

### INFERRED
Things that appear correct based on code analysis but were not directly tested.

### NOT VERIFIED
Important behavior that could not be tested or confirmed.

Be honest about uncertainty.

Never fabricate test results, coverage, runtime behavior, successful interactions, or regression status.

## Skill self-protection

The skill instructions and their supporting reference files are tooling, not part of the target application's codebase.

The agent may encounter the skill through a project-local or agent-specific location such as:

- `.agents/skills/`
- `.claude/skills/`
- `.codex/skills/`
- another agent-specific skill directory

Do not modify, refactor, delete, or "clean up" the skill itself unless the user explicitly asks you to manage the skill.

The agent may leave the skill in whatever location the host agent requires for discovery and execution.

When cleaning a repository, distinguish skill infrastructure from the application's source code.

## Final report

At the end of the cleanup, provide a concise engineering report.

Include:

### Changes made
Summarize the highest-value structural and maintainability changes.

### Problems found
Summarize the most important issues discovered in the repository.

### Verification
Report the actual commands, checks, tests, builds, and inspections performed and their results.

### Remaining risk
Identify important areas that remain uncertain, untested, or risky.

### Not changed
Identify significant areas intentionally left untouched and explain why.

Do not produce a long narrative.

Prefer concrete evidence over adjectives.

For example:

- `npm run build` — passed
- `npm test` — 184 passed, 2 failed
- `src/auth/*` — refactored; integration behavior not directly tested
- payment flow — not modified
- runtime browser interactions — not verified

Never turn an inference into a verification claim.


## Non-runtime artifacts

Do not delete documentation, examples, sample configuration, fixtures, assets, migrations, scripts, or other non-runtime files merely because they are not imported by application code.

Before removing such a file, determine whether it serves:

- developer onboarding
- local setup
- documentation
- testing
- deployment
- migration
- debugging
- examples
- design/source assets
- external tooling

Only remove it when there is strong evidence that it is obsolete, misleading, redundant, or intentionally abandoned.

When uncertain, preserve it and report it as a potential cleanup item rather than deleting it.