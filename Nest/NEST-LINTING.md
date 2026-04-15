## Goal

Guarantee:
- deterministic formatting
- strict TypeScript safety
- enforceable Nest architecture boundaries
- clean and homogeneous code style

Linting is mandatory for CORE rules.

---

## Priority

CORE rules override all other instructions.

---

## Rule Levels

### CORE (must fail CI)
- TypeScript safety
- layer/module boundary enforcement
- import discipline and no cycles
- DTO/transport boundary safety
- formatting consistency

### RECOMMENDED (warn locally, promotable to error)
- complexity caps in controllers/services
- stricter naming style rules

### OPTIONAL (team choice)
- LOC caps
- extra stylistic rules not tied to correctness

---

## Stack (MANDATORY)

### Core
- eslint (flat config only: `eslint.config.js`)
- typescript-eslint

### Imports/Architecture
- eslint-plugin-import
- eslint-plugin-boundaries (mandatory boundary mechanism)
- eslint-plugin-unused-imports

### Node/Nest
- eslint-plugin-n
- eslint-plugin-promise

### Formatting
- prettier

### Git hooks
- husky
- lint-staged

Legacy `.eslintrc*` config is forbidden.

---

## Enforceability Matrix (Single Source Of Truth)

- TypeScript strictness -> ESLint (`@typescript-eslint/*`) + `tsc --noEmit`
- Layer boundaries -> `eslint-plugin-boundaries` (element types + allowed directions)
- Cross-module deep imports -> `no-restricted-imports`
- Circular imports -> `import/no-cycle`
- Import order -> `import/order`
- Unused code -> `unused-imports/no-unused-imports`, `unused-imports/no-unused-vars`
- `process.env` outside config layer -> `no-restricted-properties` or `no-restricted-syntax`
- `console` policy -> `no-console` (allow only `warn`, `error`)
- Transport objects in service/repository signatures -> custom ESLint rule required
- ORM models/entities outside infrastructure boundary -> custom ESLint rule required
- `HttpException` outside controller/filter boundary -> custom ESLint rule required
- ORM/entity types used as transport response contracts -> custom ESLint rule required

---

## Boundary Enforcement (CORE)

Element types:
- `controller`
- `application`
- `domain`
- `infrastructure`

Allowed dependencies:
- `controller -> application`
- `application -> domain`
- `application -> infrastructure` (ports/tokens only)
- `infrastructure -> domain`
- `domain -> none`

Forbidden:
- `controller -> infrastructure/domain`
- `application -> controller`
- `domain -> application/controller/infrastructure`

`eslint-plugin-boundaries` must explicitly encode these rules.

---

## Imports And Aliases (CORE)

Policy:
- cross-module imports use aliases (`@/...`) only
- relative imports are allowed only inside one module subtree
- deep imports into another module internals are forbidden (including alias paths)

Required `no-restricted-imports` patterns:
- `@/modules/*/*/*`
- `@/modules/*/(application|domain|infrastructure|controller|dto|tokens)/**`
- `../../../modules/**`

Allowed:
- module public entry points only (for example `@/modules/users`)

Import order must be enforced with `import/order`:
1. node built-ins (`node:*`)
2. framework (`@nestjs/*`)
3. third-party
4. internal aliases (`@/app`, `@/modules`, `@/shared`, `@/infrastructure`)
5. relative

---

## TypeScript Rules (CORE)

- `@typescript-eslint/no-explicit-any`: error
- `@typescript-eslint/no-floating-promises`: error
- `@typescript-eslint/no-misused-promises`: error
- `@typescript-eslint/consistent-type-imports`: error
- ban `ts-ignore` without explanation
- explicit return type for exported/public functions

---

## Nest Rules (CORE)

- forbid direct repository/ORM access in controllers
- forbid transport objects (`Request`, `Response`, `ExecutionContext`) below controller boundary
- forbid `HttpException` outside controller/filter boundary
- forbid ORM/entity types in controller/application response contracts
- forbid direct `process.env` reads outside config layer
- forbid deep cross-module internal imports

Rules marked below require custom ESLint implementation:
- transport objects below controller boundary -> custom ESLint rule required
- `HttpException` outside boundary -> custom ESLint rule required
- ORM/entity types outside infrastructure/transport mapping boundary -> custom ESLint rule required

---

## Naming And Unused Code (CORE)

- `@typescript-eslint/naming-convention` enforces identifier naming
- file role naming (`*.controller.ts`, `*.service.ts`, `*.repository.ts`, `*.dto.ts`) -> custom ESLint rule required
- async methods must not use `Async` suffix -> custom ESLint rule required
- unused imports must fail via `unused-imports/no-unused-imports`
- unused variables must fail via `unused-imports/no-unused-vars` with `_` ignore

---

## Formatting Source Of Truth

Prettier is the only formatting tool.

Rules:
- 2 spaces
- no tabs
- semicolons: always
- quotes: single
- trailing commas: all
- print width: 100
- bracket spacing: true
- arrow parens: always
- end of line: lf

ESLint must not conflict with Prettier.

---

## EditorConfig (baseline)

- charset: utf-8
- indent_style: space
- indent_size: 2
- end_of_line: lf
- insert_final_newline: true
- trim_trailing_whitespace: true

---

## Enforcement (MANDATORY)

### Pre-commit (husky + lint-staged)

On commit:
1. `eslint --fix`
2. `prettier --write`

Commit is blocked on CORE errors.

### Pre-push

On push:
1. `eslint .`
2. `tsc --noEmit`
3. `npm test`

Push is blocked on any CORE failure.

### CI

CI must run:
1. `eslint .`
2. `tsc --noEmit`
3. `npm test`
4. `npm run build`

CI fails on any CORE violation.

---

## AI Anti-Patterns (CORE)

Never generate:
- mixed boundary enforcement mechanisms
- boundary rules without explicit element types and allowed directions
- alias deep imports into module internals
- placeholder lint configs without executable rules

