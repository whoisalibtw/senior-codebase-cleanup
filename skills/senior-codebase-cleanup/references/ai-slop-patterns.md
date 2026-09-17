# AI Slop Patterns

Use this reference when analyzing a codebase for generated, over-engineered, fragmented, or unnecessarily complicated code.

Do not assume any pattern below is automatically bad. Determine whether it provides real architectural value before changing it.

## Unnecessary wrappers

Look for:

* services that only forward to one function
* managers around another manager
* adapters around a single direct call
* factories that create one known implementation
* interfaces implemented by one trivial class without a real architectural reason
* functions whose only purpose is calling another function

Remove layers that add no meaningful behavior.

Keep layers that represent real boundaries.

## Artificial fragmentation

Look for:

* tiny files containing one trivial function
* one-function modules
* excessive folder nesting
* helpers used once
* pointless index or barrel files
* unnecessary wrapper components
* components split only to reduce file length

Consolidate when that improves comprehension.

Do not split code merely to make files smaller.

## Generic abstractions

Be suspicious of vague abstractions such as:

* Manager
* Handler
* Processor
* Engine
* Helper
* Utility
* Provider
* Coordinator
* Orchestrator

The name alone is not evidence of a problem.

Determine whether the abstraction represents a meaningful concept.

Prefer precise responsibilities and domain-oriented names.

## Over-engineering

Look for unnecessary:

* factories
* strategy layers
* adapters
* dependency injection
* configuration systems
* state layers
* event plumbing
* generic frameworks
* abstraction layers
* indirection

Prefer direct code when it communicates the same behavior more clearly.

## Duplication

Look for duplicated:

* business rules
* validation
* transformations
* authorization checks
* API calls
* persistence logic
* state logic
* constants
* configuration

Consolidate genuine conceptual duplication.

Do not combine unrelated concepts merely because their implementations look similar.

## Comment sludge

Remove comments that merely describe obvious code.

Examples:

```text
// Check if user exists
// Return the user
// Loop through items
// Set the value
```

Keep comments that explain:

* why unusual code exists
* non-obvious invariants
* security decisions
* compatibility requirements
* external system limitations
* difficult algorithms
* business rules that cannot be clearly expressed in code

## Defensive-programming spam

Look for repeated guards and defensive branches that duplicate the same assumption across many layers.

Do not blindly remove validation.

Determine where validation belongs and keep it close to the relevant boundary.

Avoid repeatedly checking invariants that have already been established.

## Type-system abuse

Look for:

* unnecessary generic parameters
* giant conditional types
* redundant interfaces
* duplicate type definitions
* excessive type assertions
* meaningless type aliases
* `any` used to hide errors
* types harder to understand than the code they describe

Simplify types when the simpler representation expresses the same contract.

## Error-handling theater

Look for error handling that adds no recovery or useful context.

Avoid patterns where code merely catches an error and throws an equally vague error.

Preserve useful error information.

Transform errors when crossing a meaningful boundary or adding meaningful context.

## Logging spam

Look for:

* function-entry logging everywhere
* duplicate logging
* development debugging left in production
* secrets or sensitive values
* logs with no operational value

Keep meaningful diagnostic and operational logging.

## Configuration theater

Look for configuration exposed solely to create the appearance of flexibility.

Examples include:

* options that are never varied
* flags with one effective value
* configuration wrappers around constants
* elaborate configuration objects for trivial behavior

Prefer explicit code when flexibility is not real.

## Magic indirection

Look for chains where understanding a simple operation requires jumping through many wrappers, callbacks, adapters, or utilities.

Prefer a shorter and more direct path when no meaningful boundary is being crossed.

## AI-generated verbosity

Look for generated code that is technically valid but unnecessarily verbose:

* repetitive branches
* duplicated conversions
* excessive temporary variables
* obvious helper functions
* verbose object transformations
* repeated null checks without distinct meaning
* explanations encoded as unnecessary code rather than clear structure

Simplify only when behavior remains clear and correct.

## AI-generated consistency theater

Be suspicious of code that applies the same abstraction pattern everywhere simply for symmetry.

Examples:

* every operation wrapped in a service
* every value given an interface
* every module given an index file
* every API call wrapped by multiple layers
* every small operation turned into a class

Consistency is useful only when it reflects a meaningful architectural convention.

## What to do with findings

For every suspicious pattern:

1. identify what purpose it serves
2. determine who depends on it
3. determine whether it represents a real boundary
4. determine whether removing it changes behavior
5. prefer the simplest implementation that preserves the actual responsibility

Do not refactor based on appearance alone.
