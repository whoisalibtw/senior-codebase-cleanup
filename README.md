# Senior Codebase Cleanup

A portable Agent Skill for aggressively cleaning, simplifying, and restructuring existing codebases for experienced human engineers.

It is designed to remove:

* AI-generated code slop
* unnecessary abstractions
* excessive indirection
* duplicated logic
* dead code
* artificial fragmentation
* vague architecture
* pointless wrappers
* excessive defensive code
* type-system overengineering
* comment and logging spam

while preserving intended application behavior.

## The goal

This skill does not try to make code "look human."

It makes code **understandable by humans**.

The standard is simple:

> Another experienced engineer should be able to open the repository, understand the architecture, trace the important behavior, and safely modify the code without needing an AI assistant to explain every subsystem.

## What it does

The skill instructs an AI coding agent to:

1. Inspect the repository broadly.
2. Reconstruct the actual architecture.
3. Trace important execution paths.
4. Identify unnecessary complexity.
5. Identify common AI-generated coding patterns.
6. Find duplication and dead code.
7. Improve module boundaries.
8. Simplify unnecessary abstractions.
9. Improve naming where it materially improves comprehension.
10. Refactor incrementally.
11. Preserve intended behavior.
12. Run the project's existing validation tools.
13. Perform a final maintainability audit.

## What it does NOT do

It does not blindly rewrite a repository.

It does not redesign a product simply because the existing implementation is unfamiliar.

It does not introduce abstractions just to make code appear architecturally sophisticated.

It does not worship DRY.

It does not optimize for minimum line count.

It does not replace one kind of AI slop with another.

## Skill format

This repository follows the portable Agent Skills format.

```text
skills/
└── senior-codebase-cleanup/
    └── SKILL.md
```

The `SKILL.md` file contains the skill metadata and instructions.

Compatible agents can discover or load the skill according to their own supported skill installation mechanism.

## Compatibility

The skill is intentionally written without vendor-specific instructions.

It is intended for Agent Skills-compatible coding agents such as:

* Claude Code
* OpenAI Codex
* Gemini CLI
* Cursor
* GitHub Copilot
* other agents supporting the `SKILL.md` Agent Skills format

Individual agents may use different directories or installation commands for discovering skills.

## Typical use

Once installed into a compatible coding agent, invoke it when a repository needs serious cleanup or structural refactoring.

Example requests:

```text
Clean up this entire codebase using the senior-codebase-cleanup skill.

Remove the AI-generated slop and unnecessary abstractions.

Go through the repository and restructure it so experienced engineers can maintain it.

Do a senior-level maintainability pass over the entire project.
```

The agent should inspect the repository before making substantial changes.

## Philosophy

The skill prefers:

**simple over clever**

**explicit over magical**

**cohesive over fragmented**

**direct over unnecessarily abstract**

**understandable over impressive**

**boring over complicated**

Good software does not need to look sophisticated.

It needs to make sense.

## Scope

This skill is designed for existing software repositories where maintainability matters.

It is particularly useful after:

* heavy AI-assisted development
* rapid prototyping
* multiple developers working independently
* rushed feature development
* large-scale generated code
* long-lived projects that accumulated abstractions

## License

MIT
