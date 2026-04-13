# React Architecture (FSD)

---

## Layers (CORE)

`app -> pages -> widgets -> features -> entities -> shared`

Rules:
- import only down the layers
- never import up
- prevent cross-layer leaks

---

## Strictness By Project Size

### Large team / long-life product
- full FSD hierarchy is required
- enforce layer boundaries in lint and CI

### MVP / small team
- allow reduced depth (`pages -> features -> shared`) temporarily
- keep public API and boundary rules from day one
- document migration path before scaling

---

## Responsibility

- `pages` -> orchestration
- `widgets` -> layout blocks
- `features` -> user interactions and use-cases
- `entities` -> domain model
- `shared` -> reusable UI and utilities

---

## Structure (Co-location)

`features/product/`
- `ui/`
- `model/`
- `api/`
- `lib/`
- `index.ts`

---

## Feature Folder Semantics

| Folder  | Purpose                   |
|---------|---------------------------|
| `ui`    | presentational components |
| `model` | state and business logic  |
| `api`   | requests and mutations    |
| `lib`   | pure helpers, schemas     |

Rules:
- `model` can depend on `api`/`lib`
- `lib` should stay pure
- `ui` should stay declarative and simple

Optional strict mode:
- keep domain model independent of transport
- move API orchestration to adapters/services instead of `model -> api`

---

## Public API

- export feature/entity API via `index.ts`
- avoid deep imports outside the slice
- allow deep imports only from explicitly exposed, documented subpaths

Good:
- `import { ProductCard } from '@/features/product'`

Bad:
- `import { ProductCard } from '@/features/product/ui/ProductCard'`

Allowed by exception:
- `import { Button } from '@/shared/ui/button'` (only when this subpath is part of public API policy)

Safe deep imports (no exception workflow):
- only from allowlisted shared subpaths
- subpath must be explicitly documented as public
- no deep imports into feature/entity internals

---

## Naming

- Component -> `PascalCase`
- Hook -> `useX`
- API -> `*.api.ts`
- Store -> `*.store.ts`
- UI styles near component -> `Component.styles.ts`

---

## Compound Components Location

If a component has 3+ tightly related parts:

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
- promote to `shared` only if truly generic

---

## Server / Client Boundaries

Rules:
- server components are default
- use `"use client"` only when needed
- keep client boundary as low as possible
- fetch data on server and pass via props when practical
- do not pass functions from server components to client components
- do not move client hooks across server boundaries

Guidelines:
- `pages/app` -> mostly server
- `widgets` -> mixed
- `features` -> often client
- `entities/shared` -> depends on usage

---

## Splitting Heuristics

Split feature when:
- the folder grows beyond ~15 files
- responsibilities become mixed
- code is reused in multiple flows

These are signals, not absolute limits.

---

## Allowed Exceptions

- temporary flattened FSD for early MVP
- local deep import inside the same slice during refactor (short-lived, tracked)
- short inline UI conditions in component render
- allowlisted deep imports from stable shared modules with explicit ownership

---

## Anti-patterns

- cross-layer imports
- deep import coupling across slices
- feature leakage into `shared`
- dumping unrelated logic into `utils`

---

## IMPORTANT

Must be used with:

- REACT-CORE.md
