# Agent Profiles Spec (10)

This repository uses 10 agents in `.github/agents/`. The orchestrator is the only coordinator and delegates via `runSubagent()`.

## Profiles
1) orchestrator — phases, gates, routing, REDO loops; does not implement code.
2) issue-analyst — REPRO/ROOT CAUSE for bugs; updates STATUS.md (REPRO/ROOT CAUSE).
3) architect — scope/design/interfaces; updates STATUS.md (SCOPE/DESIGN/INTERFACES/...).
4) coder — implements; updates STATUS.md (IMPLEMENTATION LOG).
5) qa-test — test plan and coverage; updates STATUS.md (TEST PLAN).
6) security-review — security review; updates STATUS.md (SECURITY REVIEW).
7) performance-review — performance review; updates STATUS.md (PERFORMANCE REVIEW).
8) dx-ci — CI/build/tooling; updates STATUS.md (BUILD/CI, RUN/TEST COMMANDS).
9) docs-writer — docs/run steps; updates STATUS.md (DOCS).
10) auditor — final VERIFIED/REDO; updates STATUS.md (AUDIT).

## Minimal STATUS.md sections
- PROBLEM, ACCEPTANCE CRITERIA, CONSTRAINTS, IN/OUT OF SCOPE, RUN/TEST COMMANDS
- (bugs) REPRO, ROOT CAUSE
- SCOPE, RISKS
- DESIGN, INTERFACES, DATAFLOW, EDGE CASES, PERFORMANCE NOTES
- TEST PLAN
- IMPLEMENTATION LOG
- SECURITY REVIEW, PERFORMANCE REVIEW, BUILD/CI, DOCS
- AUDIT (VERIFIED/REDO)
