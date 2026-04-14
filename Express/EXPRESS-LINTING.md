## Goal

Guarantee:
- deterministic formatting
- strict TypeScript safety
- enforceable Express layer boundaries
- consistent async/error patterns
- predictable imports and naming

Linting is mandatory for CORE rules.

---

## Priority

CORE rules override all other instructions.

---

## Rule Levels

### CORE (must fail CI)
- TypeScript safety (`no any`, `no-floating-promises`, strict null checks)
- layer boundaries and import discipline
- no circular dependencies
- async error safety in handlers
- formatting consistency

### RECOMMENDED (warn locally, promotable to error)
- controller/handler complexity caps
- stricter naming/style constraints

### OPTIONAL (team choice)
- LOC caps
- extra stylistic rules not tied to correctness

---

## Stack (MANDATORY)

### Core
- eslint (flat config)
- typescript-eslint

### Node/Express
- eslint-plugin-n
- eslint-plugin-security
- eslint-plugin-promise

### Architecture/Imports
- eslint-plugin-import
- eslint-plugin-boundaries (or `import/no-restricted-paths` zones)

### Formatting
- prettier

### Git hooks
- husky
- lint-staged

---

## Enforceability Matrix (CORE)

`Layer Contract (routes -> controller -> service -> repo)`:
- enforce with `eslint-plugin-boundaries` element rules
- or enforce with `import/no-restricted-paths` zones

`No cross-module deep imports`:
- enforce with `no-restricted-imports` patterns

`No circular dependencies`:
- enforce with `import/no-cycle`

`No raw async handlers without forwarding errors`:
- enforce with wrapper usage convention + code review checklist
- enforce `@typescript-eslint/no-misused-promises` and `no-floating-promises`
- wrapper contract: `asyncHandler` must call `next(err)` for thrown/rejected errors

`DTO Boundary`:
- enforce via code review checklist
- forbid direct domain usage in controller responses
- forbid DTO types in service/repo signatures

`No console.log in production code`:
- enforce with `no-console` (allow list for local/dev scripts only)

---

## Formatting Source Of Truth

### Prettier (only formatting tool)

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

## TypeScript Rules (CORE)

- `@typescript-eslint/no-explicit-any`: error
- `@typescript-eslint/no-floating-promises`: error
- `@typescript-eslint/no-misused-promises`: error
- `@typescript-eslint/consistent-type-imports`: error
- ban `ts-ignore` without explanation
- explicit return type for exported/public functions

---

## Express Rules (CORE)

- handlers must use `asyncHandler(fn)` or explicit `next(err)` forwarding
- forbid unvalidated boundary data in controller/service
- forbid direct `process.env` usage in `modules/*`
- forbid DB/repo usage from routes/controllers (enforce with boundary rules)
- `requestId` must be created in app-layer middleware, not in controllers
- repos must not throw HTTP-aware errors (`AppError`)
- forbid passing Express `req`/`res` objects into service/repo
- forbid creating logger instances outside `shared/logger`

---

## Imports And Naming (CORE)

Import order:
1. node built-ins (`node:*`)
2. framework (`express`)
3. third-party
4. internal aliases (`@/app`, `@/modules`, `@/shared`)
5. relative

File naming:
- routes: `*.route.ts`
- controllers: `*.controller.ts`
- services: `*.service.ts`
- repos: `*.repo.ts`
- validation schemas: `*.schema.ts`
- tests: `*.test.ts`

Async naming:
- plain verb naming only (no `Async` suffix)

Alias policy:
- internal imports must use project aliases (`@/...`)
- forbid deep relative paths across modules (for example `../../../modules/...`)

---

## Forbidden Patterns

- deep imports into other module internals
- circular imports
- business logic in routes/controllers
- DTO declarations inside handlers
- commented-out production code

---

## Enforcement (MANDATORY)

### Pre-commit (husky + lint-staged)

On commit:
1. `eslint --fix` (staged files)
2. `prettier --write` (staged files)
3. re-stage files

Commit is blocked on CORE errors.

### Pre-push

On push:
1. full eslint
2. typecheck (`tsc --noEmit`)
3. tests

Push is blocked on any CORE failure.

### CI

CI must run:
- lint
- typecheck
- tests
- build

CI fails on any CORE violation.

---

## AI Anti-Patterns (CORE)

Never generate:
- violations of Layer Contract or DTO Boundary
- ad-hoc `throw new Error()` for business cases
- deep cross-module imports
- new architecture patterns not defined in Express standards
