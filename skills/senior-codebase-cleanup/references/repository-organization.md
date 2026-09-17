# Repository Organization

Use this reference when evaluating and improving the physical structure of a repository.

The filesystem is part of the architecture.

An experienced engineer should be able to inspect the repository tree and understand the major boundaries, responsibilities, and organization before reading most of the implementation.

## Reorganize when necessary

Do not preserve a poor directory structure simply because it already exists.

Evaluate:

* file and folder naming
* directory hierarchy
* module placement
* grouping by responsibility
* grouping by domain or feature
* shared versus feature-specific code
* application versus infrastructure code
* configuration placement
* test placement
* reusable utilities
* public entry points
* obsolete directories

Move files when their location does not match their actual responsibility.

Group related code together.

Separate unrelated responsibilities that have been incorrectly grouped together.

## Prefer meaningful structure

A good repository structure should make important architectural boundaries obvious.

Prefer organization that lets an engineer quickly answer:

* Where does this feature live?
* Where does business logic live?
* Where is persistence handled?
* Where are external integrations?
* Where are shared components?
* Where are configuration and environment boundaries?
* Where do tests belong?
* What code is reusable versus feature-specific?

Do not create folders merely to make the tree appear organized.

## Avoid excessive fragmentation

Do not create:

* arbitrary one-file directories
* unnecessary nesting
* folders for trivial concepts
* duplicate directory structures
* layers that exist only for naming symmetry

Use the shallowest structure that clearly communicates responsibility.

## Domain and responsibility boundaries

When appropriate, organize code around meaningful responsibilities or domains rather than the historical order in which files were created.

For example, prefer a coherent feature boundary when it improves discoverability:

```text
features/
  projects/
  billing/
  authentication/
```

over scattering one feature across unrelated generic directories.

However, do not force domain-driven organization onto a project when the existing architecture clearly benefits from another coherent structure.

The correct structure depends on the application.

## Shared code

Shared code should genuinely be shared.

Do not move code into `shared`, `common`, `utils`, or similar directories simply because its ownership is unclear.

Before moving something into a shared area, determine whether multiple independent parts of the application actually depend on the concept.

Avoid turning shared directories into dumping grounds.

## Infrastructure boundaries

Make important infrastructure boundaries visible where practical.

Examples:

```text
app/
domain/
infrastructure/
lib/
components/
scripts/
tests/
```

The exact names do not matter.

The responsibility they communicate does.

Do not introduce these directories merely to imitate a pattern.

## Configuration

Place configuration where its ownership is obvious.

Do not scatter configuration throughout unrelated modules.

Do not move configuration simply for aesthetics.

Preserve framework-required locations.

## Tests

Keep tests discoverable and consistent with the repository's existing conventions.

Do not move tests merely to satisfy a preferred testing layout.

When reorganizing tests, preserve test discovery and tooling behavior.

## Moving files safely

When moving files:

1. identify all imports and references
2. update affected paths
3. update scripts and configuration
4. update tests
5. update documentation when necessary
6. run relevant validation
7. inspect the resulting tree

Do not leave compatibility copies solely because moving a file is inconvenient.

## Avoid unnecessary churn

Do not reorganize every directory simply because it could be arranged differently.

Prioritize structural changes that materially improve:

* discoverability
* ownership
* dependency boundaries
* maintainability
* onboarding
* navigation

Avoid large cosmetic filesystem changes with little engineering value.

## Final structure test

After reorganization, inspect the repository tree and ask:

> Could an experienced engineer understand the major architecture from the directory structure without first opening dozens of files?

If not, improve the structure where the missing architectural signal is most important.

The goal is not a universally "correct" folder layout.

The goal is a repository whose physical structure communicates the actual software architecture clearly.
