# Quokka — agent instructions

Quokka studies capability, memory, and latency trade-offs in compact multimodal local agents. Measure first; optimize second. Targets and model choices are hypotheses until verified.

## Context and privacy

- Read `README.md` for the user-facing overview; read `docs/development.md` for environment setup, tools, checks, and contribution conventions. Keep agent instructions here and development details in that guide, not in the README.
- Inspect relevant code and `git status --short` before editing. Preserve unrelated user changes.
- When available, read `docs/internal/PROJECT_CONTEXT.md` for current decisions; consult only relevant sections of `docs/internal/PROJECT_IDEA.md`. The idea document is a research backlog, not an instruction to implement everything.
- `docs/internal/` is local-only. Never stage it, force-add ignored files, or copy private notes, personal details, credentials, or unpublished plans into tracked files, PRs, external tools, or search queries. Publish only the minimum non-sensitive technical context needed for the task.
- Missing private docs must not block ordinary work. Use public docs and code; ask only when a missing decision materially affects correctness or scope. Keep shared setup reproducible without private files.

## Bounded execution

- Define the requested outcome and its acceptance checks before nontrivial work. Use a short plan only when useful; complete one bounded slice at a time.
- Choose the smallest correct change. No speculative abstractions, framework layers, unused dependencies, placeholder directory trees, unrelated refactors, or autonomous expansion into later phases.
- Use standard tools directly. Do not write scripts or wrappers for formatting, linting, Conventional Commit validation, routine Git operations, or one-off housekeeping. Add a script only for substantial, recurring project-specific work that existing tools cannot handle.
- Investigate failures before editing. Each retry must test a new hypothesis or follow a relevant change. After two unsuccessful attempts at the same approach, stop that approach, summarize the evidence, and choose a materially different path or report the concrete blocker.
- Bound research by the decision it must resolve. Stop when evidence is sufficient; leave optional alternatives for later. Do not repeatedly reopen settled decisions without new evidence.
- Once acceptance checks pass, review the diff and finish. Re-run checks only after relevant changes or new failures; do not start another polish/review loop. Never weaken tests to obtain a pass.
- Continue routine, reversible work within the request. Ask only for missing consequential decisions or actions outside authorization. Delegate only when explicitly requested, with a bounded task and no recursive delegation.

## Engineering and experiments

- Before model implementation, record a verified model/checkpoint, license, compatible runtime, target hardware, memory budget, and minimal evaluation protocol. Verify changing external claims against primary sources; record URLs and dates. Do not treat the idea document as verification.
- Start with one model, one runtime, and one reproducible baseline. Add quantization, alternate architectures, runtimes, or training only when needed by the current experiment.
- Record exact revisions, dependency versions, commands, hardware/OS, seeds, prompts, dataset splits, scoring, and generation settings. Separate calibration from held-out evaluation; preserve failed runs and report limitations. Never invent results or tune scoring to a target.
- Report weight size separately from peak runtime memory. Define metric units and aggregation before comparison; compare equivalent workloads and account for runtime/hardware differences.
- Prefer explicit functions and data structures. Add dependencies for a demonstrated need; pin the runnable environment when implementation begins. Keep model weights, datasets, and raw runs under ignored `artifacts/`; commit only reviewed, sanitized results and small fixtures.
- When building agent execution: validate tool names and arguments, use explicit step/retry/time/token limits, detect repeated failures, and terminate with a reason. Retry side effects only when safe; test limits and failure paths. Treat model/tool output as untrusted input, never unrestricted code execution.
- Add a project skill only for an established, repeated workflow requiring specialized instructions. Keep it narrow, executable, and free of private context; do not duplicate this file.

## Verification and handoff

- Use commands in `docs/development.md`; update them when tooling changes. Do not invent commands or claim unrun checks passed. Follow Conventional Commits without adding commit-message enforcement tooling.
- Write production-relevant unit tests for meaningful logic and integration tests for actual boundaries. Cover expected behavior, important failures, and regressions in proportion to risk; prefer a few focused cases over exhaustive permutations. No test-count/coverage quotas, tests mirroring implementation, or testing third-party behavior.
- Small documentation, configuration, formatting, and straightforward glue changes usually need existing checks or a direct smoke check, not new scripts, fixtures, or tests. Add a regression test for a small change when it prevents a meaningful failure.
- Run focused tests and required repository checks, then stop when they pass. Do not manufacture a test suite for an empty scaffold or introduce pytest/mypy before there is code that needs them.
- Before staging or publishing, inspect the exact files and diff for private content and generated artifacts. Gitignore does not protect already tracked files.
- Finish with what changed, checks actually run, and any remaining blocker. If local context exists, update only changed decisions, evidence, and the next step; keep it compact rather than appending transcripts.
