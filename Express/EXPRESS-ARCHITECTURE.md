# Express Architecture (Layered + Vertical Slices)

---

## Core Idea

- Express is transport/runtime only
- architecture defines dependency direction and ownership
- canonical behavioral contracts are defined in `EXPRESS-CORE.md`

---

## Source Layout

`src/`
- `app/` (bootstrap, middleware wiring, server lifecycle)
- `modules/` (business capabilities, vertical slices)
- `shared/` (cross-module libs: logger, config, errors, utils)

Rule:
- business code belongs to `modules`, not `app`

---

## Module Layout

`modules/users/`
- `routes/`
- `controller/`
- `service/`
- `repo/`
- `model/`
- `dto/`
- `validation/`
- `index.ts`

---

## Dependency Direction

See `Layer Contract (CORE)` in `EXPRESS-CORE.md`.

Additional rule:
- cross-module usage is allowed only through module public API (`index.ts`)
- internal cross-module imports must use alias paths (`@/...`), not deep relatives

---

## Layer Semantics

- `routes`: HTTP mapping (`method + path + middleware + handler`)
- `controller`: request/response orchestration and DTO mapping
- `service`: use-cases and domain decisions
- `repo`: DB/external integrations and persistence mapping
- `model`: domain types/value objects
- `dto`: transport contracts
- `validation`: boundary schemas and normalization

---

## Express Boundary

See `DTO Boundary (CORE)` and `Validation Contract (CORE)`.

Additional rule:
- Express types (`Request`, `Response`, `NextFunction`) must stay in `routes/controller`

---

## Error And Logging Placement

- base `AppError` hierarchy: `shared/errors`
- global error middleware registration: `app/`
- shared structured logger: `shared/logger`

Use contracts from:
- `Error Types (CORE)`
- `Logging (CORE)`

---

## Config Contract

- parse env once at startup
- expose typed config via `shared/config`
- no direct `process.env` reads in `modules/*`

---

## Testing Targets

- `service`: unit tests with mocked repos
- `repo`: integration tests with real adapter/test DB
- `routes/controller`: HTTP contract tests (status/body/error format)

---

## Allowed Exceptions

- temporary local deep import during refactor (TODO + owner + due date)
- temporary flattened module layout in MVP with explicit migration plan

---

## AI Anti-Patterns

See `AI Anti-Patterns (CORE)` in `EXPRESS-CORE.md`.

---

## IMPORTANT

Must be used with:

- EXPRESS-CORE.md
- EXPRESS-LINTING.md
