# GitHub Copilot Instructions (Repository)

These rules apply to all work in this repository. Keep outputs measurable and reproducible.

## Operating Model
- Work is coordinated by the `orchestrator` agent (single coordinator, no competition).
- The orchestrator delegates to subagents using `runSubagent()` with profiles in `.github/agents/`.
- Subagents must operate sequentially (no parallel edits in the same file category).

## Single Source of Truth
- `STATUS.md` is the canonical coordination artifact. Every phase updates it.
- Prefer checklists, explicit commands, and pass/fail criteria over narrative.

## Scope Control
- No scope creep. If acceptance criteria or scope must change, route back to Architect (PHASE 1 / Gate A).
- If run/test commands are unknown, discover them from the repo (README, package scripts, Makefile, CI) and record them.

## Write Zones (Hard Boundaries)
- `orchestrator`: coordination only; MUST NOT implement code changes.
- `architect`: plans/design in `STATUS.md`; SHOULD NOT change code.
- `issue-analyst`: repro/root-cause notes in `STATUS.md`; SHOULD NOT change code.
- `coder`: code + tests + minimal supporting config in scope; MUST log commands/results.
- `qa-test`: test plan in `STATUS.md`; may add tests only when authorized by orchestrator.
- `security-review`, `performance-review`, `auditor`: review-only; MUST NOT change code.
- `dx-ci`: CI/build/tooling config when required; must keep changes minimal and reproducible.
- `docs-writer`: documentation changes when required.

## Definition of Done (DoD)
A change is not "done" unless:
- Acceptance criteria are satisfied (measurable).
- `RUN/TEST COMMANDS` are recorded in `STATUS.md`.
- Commands were executed OR a reproducible blocker is documented.
- `AUDIT` ends with `STATUS: VERIFIED` or `STATUS: REDO` with numbered defects and repro steps.

## Quick Run/Test Fallbacks (use only if repo has no guidance)
- Node: `npm test` / `pnpm test` / `npm run lint`
- Python: `pytest -q` (plus `ruff`/`mypy` if configured)
- Go: `go test ./...`
- Rust: `cargo test`
- C/C++: build with the repo's build system (often CMake) and run tests if configured (`ctest`)
