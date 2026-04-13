# React Architecture (FSD)

---

## Layers (STRICT)

app → pages → widgets → features → entities → shared

Rules:
- import only DOWN
- never import UP
- no cross-layer leaks

---

## Component Nesting

- 1–3 levels → ideal
- 4–5 → acceptable
- 6+ → refactor

---

## Responsibility

pages → orchestration  
widgets → layout blocks  
features → user interactions  
entities → domain  
shared → UI / utils

---

## Structure (Co-location)

features/product/

ui/
model/
api/
lib/
index.ts

---

## Feature Folder Semantics

| Folder | Purpose |
|--------|--------|
| ui | components (view only) |
| model | state, business logic |
| api | requests, mutations |
| lib | pure helpers, schemas |

Rules:
- model can depend on api/lib
- lib must stay pure
- ui must not contain business logic

---

## Public API

- export only via index.ts
- no deep imports

✔ import { ProductCard } from '@/features/product'  
✘ import from '@/features/product/ui/...'

---

## Naming

Component → PascalCase  
Hook → useX  
API → *.api.ts  
Store → *.store.ts

---

## Compound Components Location

If a component has 3+ related parts:

features/product/ui/ProductTabs/

ProductTabs.tsx
List.tsx
Trigger.tsx
Panel.tsx
context.ts
index.ts

Rules:
- export only root API
- keep context internal
- promote to shared only if generic

---

## Server / Client Boundaries

Rules:
- server components are default
- use "use client" only when needed
- keep client boundary as low as possible
- fetch data on server and pass via props

Guidelines:
- pages/app → mostly server
- widgets → mixed
- features → often client (interactions)
- entities/shared → depends on usage

---

## Splitting

Split feature if:
- >15 files
- multiple responsibilities
- reused elsewhere

---

## Anti-patterns

- cross-layer imports
- deep nesting
- feature leakage
- dumping into utils
## IMPORTANT

Must be used with:

- REACT-CORE.md