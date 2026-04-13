## Goal

Guarantee:
- deterministic formatting
- strict TypeScript discipline
- clean React patterns
- safe hooks usage
- consistent import structure
- enforced FSD architecture boundaries

Linting is mandatory for CORE rules.

---

## AI Relaxation Mode (OPTIONAL)

During AI-assisted generation:
- temporary RECOMMENDED/OPTIONAL violations are allowed
- run `eslint --fix` + `prettier --write` before review
- final patch must pass all CORE rules before merge

This mode is for faster iteration, not for bypassing quality gates.

Guardrails:
- use only in non-main branches
- do not merge with active relaxation TODO markers
- CI must always run in strict CORE mode

---

## Rule Levels

### CORE (must fail CI)
- TypeScript safety (`no any`, no floating promises, strict null checks)
- Hooks safety (`rules-of-hooks`, `exhaustive-deps`)
- FSD boundary enforcement
- public API import rules (no cross-slice deep imports)
- formatting consistency

### RECOMMENDED (warn locally, can be promoted to error)
- JSX complexity limits
- naming conventions
- prop formatting preferences
- no inline complex expressions in JSX

### OPTIONAL (team choice)
- LOC thresholds
- memoization style constraints
- extra stylistic rules not tied to correctness

---

## Stack (MANDATORY)

AI agent must install and configure:

### Core
- eslint (flat config)
- typescript-eslint

### React
- eslint-plugin-react
- eslint-plugin-react-hooks
- eslint-plugin-jsx-a11y

### Imports
- eslint-plugin-import

### Formatting
- prettier

### Git hooks
- husky
- lint-staged

---

## Formatting Source Of Truth

### Prettier (only formatting tool)

Controls:
- indentation
- line width
- quotes
- semicolons
- trailing commas
- JSX formatting

Rules:
- 2 spaces
- no tabs
- semicolons: always
- quotes: single (JS/TS), double (JSX)
- trailing commas: all
- print width: 100
- bracket spacing: true
- arrow parens: always
- end of line: lf

ESLint must not fight Prettier.

---

## EditorConfig (baseline)

- charset: utf-8
- indent_style: space
- indent_size: 2
- end_of_line: lf
- insert_final_newline: true
- trim_trailing_whitespace: true

---

## ESLint Core Rules

### General

- no unused variables
- no unused imports
- no duplicate imports
- no shadowing
- no use-before-define
- no empty functions
- allow `console.log` in local development only
- block `console.log` in CI/production builds
- no debugger

---

## TypeScript Rules (CORE)

- no `any`
- no implicit any
- no `ts-ignore` without reason
- no floating promises
- no misused promises
- strict null checks required
- consistent type imports (`import type`)
- explicit return type for public/exported API functions

Conventions:
- prefer `type` for simple structures, unions, and utility composition
- use `interface` for extendable contracts and declaration merging

---

## React Rules

- functional components only
- no class components
- component name -> PascalCase
- hooks -> useX

### JSX intent rules

- keep JSX declarative and shallow
- extract complex or repeated logic before return
- avoid nested ternaries
- avoid unstable nested components
- no array index as key in mutable lists
- no useless fragments
- accessibility rules are mandatory

Enforce with lint where possible:
- `no-nested-ternary`
- complexity limits (`complexity`, `max-depth`)
- optional JSX perf rules (for example `eslint-plugin-react-perf`)

---

## Hooks Rules (CORE)

- `rules-of-hooks` -> error
- `exhaustive-deps` -> error

Forbidden:
- hooks in conditions
- hooks in loops
- hooks in callbacks

Effects:
- useEffect only for side-effects
- no derived state in useEffect
- no heavy business logic in useEffect

---

## Imports (CORE)

### Structure

Imports must be grouped and ordered:

1. `react`
2. framework libs
3. third-party
4. internal aliases (`@/app`, `@/pages`, `@/widgets`, `@/features`, `@/entities`, `@/shared`)
5. relative (same dir)
6. relative (parent)
7. styles (last)

Rules:
- no empty lines inside one group
- one empty line between groups
- alphabetical inside group
- no duplicate imports
- no unused imports

---

## FSD Architecture Enforcement (CORE)

Layers:

`app -> pages -> widgets -> features -> entities -> shared`

Allowed:
- import only down the layers
- import from slice public API (`index.ts`)
- import from explicitly allowlisted subpaths (rare, documented)

Forbidden:
- import up the layers
- deep imports across slices
- cross-layer leaks

---

## Relative Imports

- allowed inside the same feature/entity/widget
- forbid `../../../` chains across layers

---

## File Naming

- components -> `PascalCase.tsx`
- hooks -> `useX.ts`
- api -> `*.api.ts`
- store -> `*.store.ts`
- utils -> `camelCase.ts`
- tests -> `*.test.ts(x)`

---

## Allowed Exceptions

- small inline UI conditions in JSX
- local state duplication with a documented reason
- memoization in performance-critical areas after profiling
- temporary local deviations during refactor with TODO + owner
- allowlisted deep imports such as `@/shared/ui/button` when explicitly exported and documented

---

## Enforceability Notes

FSD boundaries are not enforced by ESLint by default. Use one of:
- `eslint-plugin-boundaries`
- `eslint-plugin-import` with restricted paths/zones
- custom ESLint rules for project-specific layer constraints

---

## Forbidden Patterns

- untyped unsafe flows
- deep imports across slices
- dead code
- commented-out code in production commits
- mutable exports
- barrel dumping without ownership
- circular imports

---

## Enforcement (MANDATORY)

Linting must run automatically.

### Pre-commit (husky + lint-staged)

On commit:
1. `eslint --fix` (staged files)
2. `prettier --write` (staged files)
3. re-stage files

Requirements:
- only staged files are processed
- commit is blocked on CORE errors

### Pre-push

On push:
1. full eslint
2. typecheck (`tsc --noEmit`)
3. optional: tests

Push must be blocked on any CORE failure.

### CI Enforcement

CI must run:
- lint
- typecheck
- tests

CI must fail on:
- any CORE lint error
- any TS error
- any test failure

---

## Strictness Policy

- CORE violations always fail CI
- RECOMMENDED rules can start as warnings and be promoted later
- OPTIONAL rules are team-tunable
- formatting is always auto-applied

---

## Performance Rules

- use `lint-staged` (no full lint on commit)
- run full lint on push / CI

---

## Result

Codebase must stay:
- predictable
- uniform
- readable
- architecture-safe
- resilient to regression
