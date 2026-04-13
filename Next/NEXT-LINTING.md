## Goal

Guarantee:
- deterministic formatting
- strict TypeScript discipline
- clean React patterns
- safe hooks usage
- correct Next.js App Router usage
- safe server/client boundaries
- consistent import structure
- enforced FSD architecture boundaries

Linting is not optional.

---

## Stack (MANDATORY)

AI agent must install and configure:

### Core
- eslint (flat config)
- typescript-eslint

### React / Next
- eslint-config-next
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

## Formatting Source of Truth

### Prettier (ONLY formatting tool)

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

ESLint must NOT fight Prettier.

---

## EditorConfig (baseline)

- charset: utf-8
- indent_style: space
- indent_size: 2
- end_of_line: lf
- insert_final_newline: true
- trim_trailing_whitespace: true

---

## ESLint – Core Rules

### General

- no unused variables
- no unused imports
- no duplicate imports
- no shadowing
- no use-before-define
- no empty functions
- no console (except warn/error)
- no debugger

---

## TypeScript Rules

- no `any`
- no implicit any
- no ts-ignore without reason
- no floating promises
- no misused promises
- strict null checks required
- consistent type imports (`import type`)
- explicit return type for exported functions

Conventions:
- prefer `type` over `interface`
- allow interface only for extension/merging

---

## React Rules

- functional components only
- no class components
- component name → PascalCase
- hooks → useX

### Strict rules

- no business logic inside JSX
- no nested ternaries in JSX
- no inline complex expressions
- no unstable nested components
- no array index as key (mutable lists)
- no useless fragments
- self-closing where possible
- boolean props shorthand

---

## Hooks Rules (STRICT)

- rules of hooks → error
- exhaustive deps → error

Forbidden:
- hooks in conditions
- hooks in loops
- hooks in callbacks

Effects:

- useEffect ONLY for side-effects
- no derived state in useEffect
- no business logic in useEffect

---

## JSX Rules

- keep JSX shallow
- extract logic before return
- one prop per line when long
- no string concatenation in JSX
- no nested ternaries
- accessibility rules mandatory

---

## Next.js Rules (CRITICAL)

### Server Components

- Server Components are default
- no useState
- no useEffect
- no browser APIs
- no event handlers

---

### Client Components

- use "use client" only when needed
- keep client boundary as deep as possible
- do not wrap entire route in client component

---

### Data Fetching

- fetch on server by default
- no duplicated fetch (server + client)
- no fetch in Client Component body unless required

---

### Props

- only serializable props allowed between server/client

Forbidden:
- functions
- class instances
- non-serializable objects

---

### App Router Files

- page.tsx must stay thin
- layout.tsx must stay thin
- no business logic in route files
- no heavy transformations in route files

---

## Imports (STRICT)

### Structure

Imports must be grouped and ordered:

1. react
2. next
3. third-party
4. internal aliases:
	- @/app
	- @/pages
	- @/widgets
	- @/features
	- @/entities
	- @/shared
5. relative (same dir)
6. relative (parent)
7. styles (last)

Rules:

- one group → no empty lines inside
- one empty line between groups
- alphabetical inside group
- no duplicate imports
- no unused imports

---

## FSD Architecture Enforcement (CRITICAL)

Layers:

app → pages → widgets → features → entities → shared

### Allowed imports

- only DOWN the layers
- never UP
- no cross-layer leaks

### Examples

✔ features → entities  
✔ widgets → features

✘ entities → features  
✘ shared → entities

---

## Public API Rule

- import only from `index.ts`
- no deep imports

✔ `@/features/product`  
✘ `@/features/product/ui/ProductCard`

---

## Relative Imports

- allowed ONLY inside the same feature/entity/widget
- forbid `../../../` chains across layers

---

## File Naming

- components → PascalCase.tsx
- hooks → useX.ts
- api → *.api.ts
- store → *.store.ts
- utils → camelCase.ts
- tests → *.test.ts(x)

---

## Forbidden Patterns

- any
- ts-ignore (without reason)
- deep imports
- duplicated state
- business logic in JSX
- effect used for derivation
- dead code
- commented-out code
- mutable exports
- barrel dumping
- circular imports
- unnecessary "use client"
- client fetching by default

---

## Enforcement (MANDATORY)

Linting MUST run automatically.

---

## Pre-commit (husky + lint-staged)

On commit:

1. eslint --fix (staged files)
2. prettier --write (staged files)
3. re-stage files

Requirements:

- only staged files processed
- commit blocked on error

---

## Pre-push

On push:

1. full eslint (no warnings allowed)
2. typecheck (tsc --noEmit)

Push must be blocked on any failure.

---

## CI Enforcement

CI must run:

- lint
- typecheck
- build

CI must fail on:
- any lint error
- any TS error
- any build failure

---

## Strictness Policy

- warnings → treated as errors in CI
- no commit with lint errors
- no push with type errors
- formatting always auto-applied

---

## Performance Rules

- lint-staged must be used (no full lint on commit)
- full lint only on push / CI

---

## Result

Codebase must be:

- predictable
- uniform
- readable
- architecture-safe
- Next.js-safe
- resistant to regression