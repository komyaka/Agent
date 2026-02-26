# Universal Task Prompt

Use this prompt to start any task — a new program, website, module, bug fix, refactor, or any other development work. Fill in the sections marked with `[...]` and hand it to the **Orchestrator** agent.

---

## Prompt Template

```
## Task

[One-sentence summary of what needs to be done]

## Type
<!-- Choose one or more -->
- [ ] New feature / program / site / module from scratch
- [ ] Bug fix
- [ ] Refactor / cleanup
- [ ] Performance improvement
- [ ] Security fix
- [ ] Documentation update
- [ ] CI/CD / tooling fix
- [ ] Other: [describe]

## Description

[Detailed description of what needs to be built or fixed.
Include context: what problem does this solve? Who uses it? How is it used?]

## Target Language / Stack

[e.g. Python + FastAPI, TypeScript + React, Go, Rust, C#/.NET, PHP, Java, plain HTML/CSS/JS, etc.]

## Requirements / Acceptance Criteria

[List the concrete, measurable requirements. "It works" is not enough.
Examples:
- The CLI accepts a `--output` flag and writes results to the specified file.
- The API endpoint returns HTTP 400 with a JSON error body when input is missing.
- All existing tests continue to pass.
- The page renders correctly on mobile (320px) and desktop (1280px).]

## Known Constraints

[Optional. Examples:
- Must not add new dependencies.
- Must be compatible with Python 3.9+.
- The file `src/legacy.py` must not be modified.
- Must pass existing CI pipeline.]

## Files / Directories in Scope

[Optional. If you know which files are affected, list them.
If unknown, write "unknown — let Architect determine".]

## Run / Test Commands

[Optional. If you know how to build and test, list the commands.
If unknown, write "unknown — let Architect determine".
Examples:
  Build: npm run build
  Test:  npm test
  Run:   python main.py]

## Reference / Examples

[Optional. Links, file paths, screenshots, or descriptions of similar existing code
that can guide the implementation.]

## Priority / Deadline

[Optional. e.g. "Blocking release — high priority", "Nice to have", "By Friday".]
```

---

## Minimal Example (enough to get started)

```
## Task
Add a /health endpoint to the FastAPI app that returns {"status": "ok"}.

## Type
- [x] New feature

## Description
The monitoring system needs a health check endpoint to verify the app is running.
It should return HTTP 200 with body {"status": "ok"} and no authentication required.

## Target Language / Stack
Python + FastAPI (existing project in backend/)

## Requirements / Acceptance Criteria
- GET /health returns HTTP 200 and {"status": "ok"}.
- No authentication required.
- A unit test covers the endpoint.

## Run / Test Commands
  Build: (none needed)
  Test:  pytest tests/ -v
```

---

## Full Example (complex task)

```
## Task
Build a multi-language code syntax highlighter module in TypeScript.

## Type
- [x] New feature / module from scratch

## Description
We need a reusable TypeScript module that accepts a string of code and a language
identifier, and returns an HTML string with syntax highlighting spans.
It will be used in the web editor component (frontend/editor/).

## Target Language / Stack
TypeScript (ESM), Node.js 20+, no bundler (pure TypeScript library).

## Requirements / Acceptance Criteria
- Accepts input: { code: string, language: string }
- Returns: string (HTML with <span class="token-*"> elements)
- Supports at minimum: TypeScript, Python, Go, Rust, JSON, Bash.
- Falls back gracefully to plain text for unsupported languages (no error thrown).
- All exported functions are typed; no `any` allowed.
- Unit tests cover: each supported language, unknown language fallback, empty string input.
- Bundle size of the module < 50 KB (no large dependencies).

## Known Constraints
- Do not use highlight.js or prism.js (license conflict). Use a lightweight alternative.
- Must work in both Node.js and browser environments (no Node-only APIs).

## Files / Directories in Scope
- src/highlighter/ (create new)
- src/highlighter/index.ts (main entry)
- src/highlighter/languages/ (language grammars)
- tests/highlighter/ (tests)

## Run / Test Commands
  Build: tsc --project tsconfig.json
  Test:  pnpm test

## Reference / Examples
See existing editor component at frontend/editor/CodeMirrorWrapper.tsx for how
the module will be called.
```

---

## How the Orchestrator Will Use This Prompt

1. Read your task description.
2. Evaluate routing rules to select the required agents.
3. Run the agent chain sequentially.
4. Update `STATUS.md` at each step.
5. Report back to you when the task is complete or when a decision is needed.

You will only be interrupted if:
- A blocking ambiguity cannot be resolved without your input.
- 3 REDO cycles fail on the same gate (escalation).
- A security or architecture risk requires your approval.
