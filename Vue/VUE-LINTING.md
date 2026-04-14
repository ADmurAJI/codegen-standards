## Goal

Guarantee:
- deterministic formatting
- strict TypeScript discipline
- clean Vue Composition API patterns
- safe reactivity usage
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
- Vue SFC and reactivity safety
- lifecycle/effect-scope safety (no hanging side-effects)
- DOM timing safety (`watch` flush / `nextTick` usage)
- FSD boundary enforcement
- public API import rules (no cross-slice deep imports)
- formatting consistency

### RECOMMENDED (warn locally, can be promoted to error)
- template complexity limits
- naming conventions
- explicit emits/model contracts
- no inline complex expressions in templates

### OPTIONAL (team choice)
- LOC thresholds
- extra stylistic rules not tied to correctness

---

## Stack (MANDATORY)

AI agent must install and configure:

### Core
- eslint (flat config)
- typescript-eslint

### Vue
- eslint-plugin-vue
- vue-eslint-parser
- @vue/eslint-config-typescript (or equivalent flat TS setup)

### Imports
- eslint-plugin-import
- eslint-import-resolver-typescript

### Formatting
- prettier
- prettier-plugin-organize-imports (optional)

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
- template/script/style formatting

Rules:
- 2 spaces
- no tabs
- semicolons: always
- quotes: single (JS/TS), double (Vue templates)
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

## Vue Rules (CORE)

- Composition API first
- `<script setup lang="ts">` by default
- component name -> PascalCase
- composables -> `useX`
- no deprecated Vue 2 patterns in new code

### Template intent rules

- keep template declarative and shallow
- extract complex/repeated logic before template
- avoid nested ternaries
- avoid `v-if` + `v-for` on the same node
- no mutating props
- prefer keyed `v-for` with stable keys (no array index for mutable lists)
- accessibility rules are mandatory
- emits are explicit typed public contract (no implicit event API)
- side-effects in `setup` must be explicit and lifecycle-bound
- use `provide`/`inject` for deep non-global context sharing when needed
- avoid pushing local context state into global store by default
- use `Teleport` for modals/overlays instead of DOM hacks

Enforce with lint where possible:
- `vue/no-mutating-props`
- `vue/no-use-v-if-with-v-for`
- `vue/require-v-for-key`
- `vue/require-explicit-emits`
- template complexity limits (`complexity`, `max-depth` in script logic)

---

## Reactivity Rules (CORE)

- use `computed` for derived state
- `computed` must stay pure and synchronous
- use `watch`/`watchEffect` only for side-effects
- prefer `watch` over `watchEffect` for non-trivial logic
- allow `watchEffect` only for simple reactive bindings
- avoid deep watch by default
- avoid side-effects in computed getters
- use explicit `watch` flush timing for DOM/layout-sensitive logic
- prefer `flush: 'post'` for DOM-dependent side-effects
- use `nextTick` before reading DOM after reactive state updates
- avoid destructuring `reactive` objects without `toRefs`/`toRef`
- avoid spreading `reactive` objects into plain objects
- side-effects must be tied to component/effect scope
- cleanup with `onUnmounted`/`onScopeDispose` when needed

Forbidden:
- derived state via watchers when computed is enough
- heavy business logic inside watch callbacks
- hanging listeners/timers/subscriptions/requests
- implicit async event flows without loading/error/race handling

---

## SSR / Hydration Safety (CORE when SSR-capable)

- avoid direct `window`/`document` usage outside `onMounted`
- guard browser-only APIs when SSR is possible
- avoid non-deterministic render output that causes hydration mismatch

---

## Error Isolation

- use `onErrorCaptured` for local component tree isolation where partial failure is expected

---

## Imports (CORE)

### Structure

Imports must be grouped and ordered:

1. `vue`
2. framework/router libs
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

- components -> `PascalCase.vue`
- composables -> `useX.ts`
- api -> `*.api.ts`
- store -> `*.store.ts`
- utils -> `camelCase.ts`
- tests -> `*.test.ts(x)`

---

## Allowed Exceptions

- small inline UI conditions in templates
- local state duplication with a documented reason
- memo-like optimizations in performance-critical areas after profiling
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
- business logic in templates

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
- tests/build (project choice)

CI must fail on:
- any CORE lint error
- any TS error
- any failed required job

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
- Vue-safe
- resilient to regression
