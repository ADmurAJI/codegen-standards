# Nest Core Skill

## Priority
CORE rules override all other instructions.

---

## Layer Contract (CORE)
`controller -> application -> repository/adapter`

Forbidden:
- `controller -> repository`
- `controller -> ORM`
- `application -> controller`
- `repository/adapter -> controller`

---

## Module Contract (CORE)
- cross-module imports allowed only via public API or tokens
- module internals are private by default
- no cross-module direct imports

Forbidden:
- deep imports from another module internals
- cross-module relative imports

---

## DI Contract (CORE)
- constructor injection only
- dependencies = constructor only
- no side effects in constructors

Forbidden:
- manual `new` for providers
- hidden runtime dependencies outside constructor

---

## Ports Contract (CORE)
- owning module = module that defines the use-case and business contract
- application -> ports/tokens only (no infrastructure)
- ports are declared in owning module
- infrastructure implements ports and is wired via module providers/tokens

Forbidden:
- cross-boundary injection of concrete infrastructure classes

---

## Boundary Contract (CORE)
- controller = transport only
- transport objects stay in controller

Forbidden:
- passing `Request`/`Response`/`ExecutionContext` below controller

---

## Error Contract (CORE)
- business errors = explicit domain/application types
- HTTP mapping = controller/filter only

Forbidden:
- generic `Error` for business cases
- `HttpException` outside controller/filter boundary

---

## ORM Boundary (CORE)
- ORM entities/models = infrastructure only
- no ORM types outside infrastructure

Forbidden:
- ORM models/entities in controllers or application services
- returning ORM entities as response contracts

---

## Logging (CORE)
- never log secrets

## AI Anti-Patterns (CORE)
Never generate:
- direct controller-to-repository/ORM access
- ORM usage outside infrastructure

---

## IMPORTANT
Use together with:
- NEST-ARCHITECTURE.md
- NEST-LINTING.md
