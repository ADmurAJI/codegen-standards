# Next.js Architecture (FSD + App Router)

---

## Core Idea

- Next.js defines rendering/runtime boundaries
- FSD defines project structure and dependency direction
- both are mandatory in production-scale projects

---

## Layers (CORE)

`app -> pages -> widgets -> features -> entities -> shared`

Rules:
- import only down the layers
- no cross-layer imports
- no internal slice leaks

---

## Strictness By Project Size

### Large team / long-life product
- full FSD hierarchy is required
- enforce boundaries in lint and CI

### MVP / small team
- allow reduced depth temporarily (`pages -> features -> shared`)
- keep public API import rules from day one
- define a migration path before scaling

---

## App Router Structure

`app/`
- `layout.tsx`
- `page.tsx`
- `error.tsx`
- `loading.tsx`

Rules:
- app layer is orchestration-first
- avoid embedding business workflows in route files

---

## Component Placement

### Server (default)
- `app/`
- `pages/`
- data loading
- layout composition

### Client
- interactive features
- interactive widgets

Rule:
- push `"use client"` as deep as possible

---

## Data Flow

`server -> props -> client`

- fetch on server by default
- normalize at the boundary
- pass typed data down

---

## Feature Structure

`features/product/`
- `ui/`
- `model/`
- `api/`
- `lib/`
- `index.ts`

---

## Feature Folder Semantics

| Folder | Purpose |
| --- | --- |
| `ui` | presentational components |
| `model` | state and business logic |
| `api` | requests and mutations |
| `lib` | pure helpers |

Rules:
- `model` can depend on `api`/`lib`
- `lib` should stay pure
- `ui` should stay declarative and simple

Optional strict mode:
- keep domain model independent from transport
- move API orchestration to adapters/services instead of `model -> api`

---

## Public API

Good:
- import from feature/entity root (`index.ts`)

Bad:
- deep import from internals across slices

Allowed by exception:
- deep import from explicitly exposed shared subpaths (for example `@/shared/ui/button`)

Safe deep imports (no exception workflow):
- only from allowlisted shared subpaths
- subpath must be explicitly documented as public
- no deep imports into feature/entity internals

---

## Compound Components Location

`features/product/ui/ProductTabs/`
- `ProductTabs.tsx`
- `List.tsx`
- `Trigger.tsx`
- `Panel.tsx`
- `context.ts`
- `index.ts`

Rules:
- export only root API
- keep context internal
- promote to shared only when truly generic

---

## Server / Client Boundaries

- server is default
- use `"use client"` only when needed
- keep boundary minimal
- do not pass functions from server components to client components
- do not move client hooks across server boundaries

Guidelines:
- `app/pages` -> mostly server
- `widgets` -> mixed
- `features` -> often client
- `entities/shared` -> depends on usage

---

## Routing Rules

- keep route files thin
- move business logic to features/entities
- keep segment ownership clear

---

## Error Boundaries

- use `error.tsx` per route segment
- place close to failure points
- use `global-error.tsx` only at root scope

---

## Splitting Heuristics

Split a feature when:
- folder grows beyond ~15 files
- responsibilities diverge
- reuse appears in multiple flows

These are heuristics, not hard limits.

---

## Naming

- routes -> kebab-case
- components -> PascalCase
- UI styles near component -> `Component.styles.ts`

---

## Allowed Exceptions

- temporary local deep import inside same slice during refactor (tracked)
- temporary flattened FSD in early MVP
- local boundary compromise during migration with explicit TODO + owner
- allowlisted deep imports from stable shared modules with explicit ownership

---

## Anti-patterns

- heavy logic in route files
- client fetching by default
- deep imports across slices
- layer violations

---

## IMPORTANT

Must be used with:

- NEXT-CORE.md
- NEXT-LINTING.md
