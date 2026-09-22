# architecture-to-c4 repository instructions

These instructions apply to the entire repository.

## Repository purpose

* This repository contains a standalone TypeScript tool for converting architecture documentation into a C4 architecture model and generated architecture output.
* Keep the core transformation independent from Yamabiko Table Reorder, WordPress, and other consuming repositories.
* Repository-specific examples, fixtures, or compatibility handling must not become assumptions in the generic architecture model or transformation pipeline.

## Repository boundaries

* `src/` contains the implementation of the architecture parser, model, validation, generation, and CLI responsibilities.
* `docs/development/` contains durable repository-wide development principles and validation guidance.
* Tests and fixtures should stay close to the responsibility they validate unless a concrete cross-cutting test responsibility requires otherwise.
* Add new directories, layers, or abstractions only when a concrete responsibility requires them. Do not create placeholder structure for anticipated features.

## Architecture boundaries

* Preserve the primary transformation flow:

  `Architecture Markdown → Parser → Architecture Model → Validation → Output Generator`

* Keep parsing, architecture semantics, validation, output generation, and CLI concerns separated where they have distinct responsibilities.

* The Architecture Model is the boundary between input parsing and output-specific generation.

* Do not leak Structurizr-specific concepts into generic parsing or architecture-model responsibilities unless they are genuinely part of the repository's supported architecture semantics.

* Do not introduce a generalized backend framework solely for hypothetical future output formats.

* Prefer explicit, deterministic transformations over hidden inference or environment-dependent behavior.

## Input and output behavior

* Treat documented input contracts as part of the public behavior of the tool.
* Reject structurally invalid or ambiguous input rather than silently guessing when the input contract requires a unique interpretation.
* Validation failures must result in a non-successful command outcome.
* Do not report generation or validation as successful when required validation failed.
* Avoid leaving misleading or partially generated output after a failed transformation when the operation can reasonably fail before output is finalized.
* Generated output must be deterministic for equivalent input.

## Development documentation

* Read `docs/development/foundation.md` for repository-wide development principles.
* Read `docs/development/testing.md` before selecting validation commands.
* Keep documentation aligned with the code, commands, dependencies, and directories that exist on the current branch.
* Do not preserve documentation inherited from another repository when its assumptions no longer apply here.

## Communication

* Do not narrate routine file reads, searches, edits, or successful commands unless the information helps the user make a decision or understand an important finding.
* Surface blocking issues, material changes in assumptions, required scope changes, and decisions that require user input.
* Keep communication concise and focused on the requested work.

## Approval requests

* Request approval before taking a destructive, unexpected, or decision-sensitive action that is not already clearly authorized and could materially affect the repository, environment, dependencies, or user data.
* Do not request additional approval for actions already clearly authorized by the user's request and these repository instructions.
* Do not broaden the requested scope while a material decision remains unresolved.

## End-of-turn reports

* When repository work is performed, briefly report the work performed, changed files, validation results, and any open items.
* Never report validation as successful unless it actually ran successfully.
* If validation was not run or was intentionally left to the user, state that clearly.
* When changes are pushed, include a compare URL using the repository state at the start of the work and the pushed SHA.

## Working rules

* Make the smallest change that fully satisfies the current issue.
* Keep implementation, tests, and documentation aligned with the current repository state.
* Do not add dependencies, abstractions, source structure, or documentation structure before a concrete responsibility requires them.
* Do not introduce Yamabiko Table Reorder, WordPress, or other consumer-specific dependencies into the generic implementation.
* Do not commit generated dependencies or build output such as `node_modules/` or `dist/`.
* Do not commit secrets, credentials, personal paths, machine names, or other local-only environment details.

## Code review

* Before raising a review finding, weigh at least the issue's occurrence frequency, user impact, and the complexity introduced by the proposed fix.
* Prioritize findings that can cause incorrect architecture interpretation, invalid or inconsistent generated output, nondeterministic results, silent validation failures, broken CLI behavior, or loss of meaningful architecture information.
* Do not require additional state, abstractions, coordination layers, or framework machinery solely to address low-frequency, low-impact formatting or presentation differences.
* Low frequency does not reduce the importance of issues that can produce incorrect architecture models, invalid output, false-success command results, or unrecoverable loss of source meaning.

## GitHub Actions

* Keep CI, security, and release workflows limited to their intended purpose.
* Do not change workflow permissions, triggers, or jobs solely to run unrelated temporary processing.
* Remove temporary workflows before merge unless the task explicitly establishes a permanent need for them.
* When `.github/workflows/` changes, review the final diff for unrelated changes, obsolete assumptions, or temporary work.

## Documentation responsibilities

* Put direct working instructions in `AGENTS.md` files.
* Put durable repository-wide development principles and rationale in `docs/development/`.
* Update relevant documentation when a command, directory boundary, dependency, input contract, output contract, or development rule changes.
* Avoid duplicating validation command lists. Use `docs/development/testing.md` as the source of truth.

## Validation

* Run only checks applicable to the changed files, as documented in `docs/development/testing.md`.
* For transformation logic, validate both successful generation and relevant failure behavior.
* When generated Structurizr DSL is affected, run the documented Structurizr validation when applicable.
* Documentation-only changes do not require implementation builds or linters unless code or configuration also changes.
* Never report a command as successful unless it actually ran successfully.

## Efficient workflow

* Inspect only the files, documentation, and history required for the requested task.
* Do not inspect dependency, generated, cache, build, distribution, or test-output directories unless the task requires them.
* Prefer the narrowest relevant validation while iterating.
* Do not re-read unchanged files or repeat successful commands unless new evidence makes it necessary.
* Do not broaden the requested scope unless necessary to complete the requested outcome.
