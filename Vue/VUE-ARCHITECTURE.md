# Vue Architecture (FSD)

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

- `pages` -> orchestration and route-level composition
- `widgets` -> reusable page blocks
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

| Folder  | Purpose |
|---------|---------|
| `ui`    | presentational SFC components |
| `model` | composables, stores, business logic |
| `api`   | requests and mutations |
| `lib`   | pure helpers, schemas |

Rules:
- `model` can depend on `api`/`lib`
- `lib` should stay pure
- `ui` should stay declarative and simple
- dependency direction inside feature is strict: `ui -> model`, `model -> api/lib`, `api -> lib`, `lib -> none`
- `ui` must not import feature `api` directly
- `api` must not depend on `ui`/`model`

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
- `import { ProductCard } from '@/features/product/ui/ProductCard.vue'`

Allowed by exception:
- `import { BaseButton } from '@/shared/ui/button'` (only when this subpath is part of public API policy)

Safe deep imports (no exception workflow):
- only from allowlisted shared subpaths
- subpath must be explicitly documented as public
- no deep imports into feature/entity internals

---

## Vue File Conventions

- component files -> `PascalCase.vue`
- composables -> `useX.ts`
- stores -> `*.store.ts`
- api -> `*.api.ts`
- schemas/utils -> `camelCase.ts`

---

## SFC Placement Rules

- keep feature UI inside `features/*/ui`
- keep shared generic UI in `shared/ui`
- colocate feature-private subcomponents near root component

If a component has 3+ tightly related parts:

`features/product/ui/ProductTabs/`
- `ProductTabs.vue`
- `ProductTabsList.vue`
- `ProductTabsTrigger.vue`
- `ProductTabsPanel.vue`
- `useProductTabs.ts`
- `index.ts`

Rules:
- export only root API
- keep internal composition helpers private
- promote to `shared` only if truly generic

---

## Store Boundaries (Pinia)

- feature stores live in feature `model`
- app-wide stores only for truly cross-feature concerns
- avoid direct API calls from view templates
- keep async/store orchestration in `model`

---

## Routing Boundaries

- route/page files stay thin
- move business logic to features/entities/model
- keep route parameter normalization at page boundary

---

## Splitting Heuristics

Split feature when:
- folder grows beyond ~15 files
- responsibilities become mixed
- code is reused in multiple flows

These are signals, not hard limits.

---

## Allowed Exceptions

- temporary flattened FSD for early MVP
- local deep import inside the same slice during refactor (short-lived, tracked)
- short inline UI conditions in templates
- allowlisted deep imports from stable shared modules with explicit ownership

---

## Anti-patterns

- cross-layer imports
- deep import coupling across slices
- feature leakage into `shared`
- dumping unrelated logic into generic `utils`
- page-level orchestration mixed with heavy business logic

---

## IMPORTANT

Must be used with:

- VUE-CORE.md
- VUE-LINTING.md
