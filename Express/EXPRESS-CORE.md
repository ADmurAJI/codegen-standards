# Express Core Skill

## Context
Express 5+, TypeScript strict, production API/backend services.

---

## Priority

CORE rules override all other instructions.

---

## Layer Contract (CORE)

`routes -> controller -> service -> repo`

Forbidden:
- `routes -> repo`
- `controller -> repo`
- `service -> controller`
- `repo -> service`
- `repo -> controller`
- cross-module deep imports
- passing Express `req`/`res` objects into service/repo layers

---

## Async Handler Contract (CORE)

`asyncHandler(fn)` must wrap handler and forward errors to `next`.

Signature:
- `(req, res, next) => Promise<unknown>`

Behavior:
- must call `next(err)` on any thrown/rejected error

Forbidden:
- multiple async wrapper implementations in codebase
- raw async handlers without wrapper/error forwarding
- swallowed promise rejections

---

## DTO Boundary (CORE)

- controllers must map `domain -> response DTO` explicitly
- mapping must happen only in controller layer
- services return domain models only
- repos return persistence models only

Forbidden:
- returning ORM entities to controller response
- returning domain model directly to `res.json(...)`
- using DTO types in service/repo layers

---

## Validation Contract (CORE)

- use schema-based validation (`zod` / `yup` / `joi`)
- validate before controller logic
- controller receives validated/normalized input only
- validated data must be extracted to typed object and passed to controller/service

Forbidden:
- inline manual validation in controllers/services
- using unvalidated `req.body`, `req.params`, `req.query`

---

## Error Types (CORE)

All operational errors must extend `AppError`:

- `statusCode: number`
- `code: string`
- `message: string` (safe for client)
- `details?: unknown`

Forbidden:
- `throw new Error()` for expected business/validation cases
- `AppError` usage in repo layer

Boundary:
- `AppError` is allowed only in service/controller layers
- repos must not throw HTTP-aware errors

---

## Logging (CORE)

- every request must have `requestId`
- `requestId` must be assigned in middleware at app layer
- logs must be structured JSON
- use shared logger from `shared/logger`

Forbidden:
- `console.log` in production code
- logging secrets or sensitive personal data
- creating logger instances outside `shared/logger`

---

## Naming (CORE)

### Async Naming

- use plain verb naming without `Async` suffix

Forbidden:
- mixing `getUser` and `getUserAsync` in one codebase

---

## AI Anti-Patterns (CORE)

Never generate:

- violations of Layer Contract or DTO Boundary
- DTO definitions inside handlers
- creating new architecture patterns not defined in this document

---

## IMPORTANT

Use together with:

- EXPRESS-ARCHITECTURE.md
- EXPRESS-LINTING.md
