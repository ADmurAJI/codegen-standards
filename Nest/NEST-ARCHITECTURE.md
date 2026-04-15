# Nest Architecture (Layered + Vertical Modules)

---

## Core Idea

- Nest is framework/runtime and DI container
- architecture defines dependency direction, module ownership, and boundaries
- canonical behavioral contracts are defined in `NEST-CORE.md`

---

## Source Layout

`src/`
- `app/` (bootstrap, global pipes/filters/interceptors, app module wiring)
- `modules/` (business capabilities as vertical modules)
- `shared/` (cross-module technical primitives only: config, logger, errors, utils)
- `infrastructure/` (platform-level clients/integrations reused by multiple modules)

Rule:
- business code belongs to `modules`, not `app`
- `app/` contains no feature business logic
- feature use-cases are not created in `app/`

---

## Infrastructure Split

- `modules/*/infrastructure`: repositories/adapters owned by one specific module
- `src/infrastructure`: shared platform clients and integrations used by many modules

Forbidden:
- placing module-owned repositories in `src/infrastructure`
- placing cross-module platform clients inside a single feature module

---

## Module Layout

`modules/users/`
- `users.module.ts`
- `controller/`
- `application/`
- `domain/`
- `infrastructure/`
- `dto/`
- `tokens/`
- `index.ts` (public exports for non-Nest consumers/tests if needed)

Optionality:
- module uses only needed directories
- missing `domain/` or `tokens/` is allowed when truly unnecessary
- structure must be consistent, not ritualistic with empty folders

---

## Module Public API

- everything inside a module is private by default
- cross-module access is allowed only through module exports/tokens or explicit public entry points

Forbidden:
- direct imports from internal folders of another module
- deep cross-module relative imports

---

## Dependency Direction

`controller -> application -> domain/ports -> infrastructure`

Rules:
- controller depends on application services only
- application depends on module ports/contracts
- infrastructure implements ports and is wired in module providers
- domain is independent from transport and framework

---

## Shared Contract

- `shared` contains only cross-module technical code
- `shared` must not contain feature business logic
- if code belongs to one business capability, it stays in that module

---

## Application Contract

- `application` contains use-cases and orchestration
- application is transport-agnostic
- application depends on ports, not concrete ORM/HTTP client implementations
- one public application service method should represent one use-case unless explicitly justified

---

## Domain Contract

- `domain` contains business rules independent of Nest, DB, and transport
- if domain complexity is low, `domain` may stay minimal
- domain layer must not exist as ceremony only

---

## Controller Contract

- `controller` is input/output transport boundary only
- controller delegates to application layer

Forbidden:
- direct DB/external service calls from controller
- non-trivial orchestration in controller

---

## DTO Contract

- DTOs belong to transport boundary
- DTOs are not internal domain/application models
- mapping between DTOs and internal models is explicit

---

## Nest Boundary

Use framework-specific types/decorators only at boundary layers:
- allowed in `app/` and `controller/`
- limited use in guards/pipes/interceptors/filters
- avoid Nest-specific abstractions inside domain logic

- do not pass framework transport objects into application/domain/infrastructure services
- `@nestjs/*` dependencies must not be required to execute domain logic

---

## Ports And Tokens Placement

- ports are declared by the owning module (typically in `tokens/` or adjacent application contracts)
- implementations live in module `infrastructure/`
- wiring is done via module providers/tokens
- application depends on ports, not concrete implementations

---

## Mapping Placement

- request mapping happens at controller boundary
- response mapping happens in controller or dedicated mapper
- repositories do not create transport contracts
- infrastructure does not know response DTOs

---

## Transaction Placement

- transaction boundaries are defined in application layer
- repositories execute operations within provided transaction context when present
- repositories do not define business transaction boundaries on their own

---

## Validation And Serialization Placement

- `ValidationPipe` is configured at app/bootstrap or route boundary
- DTO validation runs before application logic
- serialization policy is handled at transport boundary

---

## Error And Logging Placement

- shared app/domain error base in `shared/errors`
- global exception filter registration in `app/`
- shared structured logger in `shared/logger`
- request correlation id setup in middleware/interceptor at app layer

Use contracts from:
- `Error Contract (CORE)`
- `Logging (CORE)`

---

## Config Contract

- config reads are centralized
- parse and validate env once at startup
- modules consume typed config/services instead of direct env access
- feature code must not parse env on its own

---

## Testing Targets

- `application`: use-case behavior tests with mocked ports/repositories
- `infrastructure`: adapter correctness tests with real integrations/test doubles
- `controller`: transport contract tests (status/body/error contract)
- `module` composition: DI wiring correctness tests

---

## Allowed Exceptions

- exceptions are temporary, human-reviewed, and explicitly documented
- each exception must include owner, reason, scope, and removal date
- exceptions are migration aids, not an allowed architecture mode

---

## AI Anti-Patterns

See `AI Anti-Patterns (CORE)` in `NEST-CORE.md`.

---

## IMPORTANT

Must be used with:

- NEST-CORE.md
- NEST-LINTING.md
