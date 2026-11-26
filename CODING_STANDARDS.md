# Coding standards

> Settled with the owner on 2026-11-26 during factory-init. No factory run may change this file.

How the factory uses this file: every implementer is shown every rule. The rules **kept by a check** are decided by code, from the exit code of the command named in `.factory/project.json` (`commands.<name>`); a rule naming a check the project does not have stops the run before it starts. The rules **kept by review** are judged one by one by every reviewer, with the file and line of each place one is broken. A `blocking` rule that fails sends the code back to its implementer; a `minor` one is reported and never blocks. Each run reports every rule as pass, fail, not applicable or not judged.

Keep the table's columns as they are: `scripts/project-check.mjs` reads them. Write each rule so that two reviewers would judge the same code the same way: say what is required, not what is nice.

## Rules

| ID  | Rule                                                                                                                                                                                          | Severity | Kept by          |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------------- |
| S1  | Code is formatted by the project's formatter, with its configuration as committed.                                                                                                            | blocking | check: format    |
| S2  | The linter reports no error and no warning on the whole project.                                                                                                                              | blocking | check: lint      |
| S3  | The type check passes in strict mode.                                                                                                                                                         | blocking | check: typecheck |
| S4  | The whole test suite passes.                                                                                                                                                                  | blocking | check: test      |
| S5  | No way around the checks: no `any`, `@ts-ignore`, `# type: ignore`, `eslint-disable`, `noqa`, skipped or focused test, unless the same line says why and names an issue.                      | blocking | review           |
| S6  | An error is handled or passed on with what was being done; it is never swallowed (an empty `catch`, a `catch` that logs and goes on as if it worked, a returned `null` that hides a failure). | blocking | review           |
| S7  | Every behaviour the change adds or fixes has a test that fails without it, through the public interface of the module; a test does not assert on a mock it set up itself.                     | blocking | review           |
| S8  | No code is left unused: no commented-out code, unused export, unreachable branch, debug output (`console.log`, `print`, `debugger`) or TODO without an issue.                                 | minor    | review           |
| S9  | A name says what the thing is or does, in the words of the domain (`GLOSSARY.md` when there is one), not how it is built (`data`, `info`, `handle`, `manager`, `util`).                       | minor    | review           |
| S10 | A function does one thing and fits on a screen: around 50 lines, nesting no deeper than 3; split it where a reader has to hold more.                                                          | minor    | review           |
| S11 | New code goes where the codebase already puts that kind of code, and reuses its helpers and components rather than adding a near-copy.                                                        | minor    | review           |
| S12 | No new dependency where the standard library, the platform or an existing dependency already does it.                                                                                         | minor    | review           |
| S13 | No value that may differ between environments (URL, key, limit, timeout) is written in the code; it comes from configuration, with a named default.                                           | minor    | review           |
| S14 | A module or function other parts of the code use says in one comment what it is for and why, not how.                                                                                         | minor    | review           |

## Project rules

Rules of this codebase that the table above does not cover.

| ID  | Rule                                                                                                                                                                                     | Severity | Kept by |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------- |
| S15 | Colours, radii and sizes in styles come from the tokens in `src/tokens.css` (`var(--…)`); a literal colour in a component's styles is a bug.                                             | minor    | review  |
| S16 | Components are React function components under `src/`, each with its tests next to it as `<Name>.test.tsx`, written with Testing Library through what a user sees (roles, labels, text). | minor    | review  |
