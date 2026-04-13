# Next.js Architecture (FSD + App Router)

---

## Core Idea

Next.js → rendering model  
FSD → project structure

Both must be respected.

---

## Layers (STRICT)

app → pages → widgets → features → entities → shared

Rules:
- import only DOWN
- no cross-layer imports
- no internal leaks

---

## App Router Structure

app/

layout.tsx
page.tsx
error.tsx
loading.tsx

Rules:
- app layer = orchestration only
- no business logic

---

## Component Placement

### Server (default)
- app/
- pages/
- data loading
- layout composition

### Client
- features (interactions)
- interactive widgets

Rule:
- push "use client" as deep as possible

---

## Data Flow

Server → props → client

- fetch on server
- normalize at boundary
- pass typed data down

---

## Feature Structure

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
| lib | pure helpers |

Rules:
- model depends on api/lib
- lib must stay pure
- ui must not contain business logic

---

## Public API

✔ import from feature root  
✘ no deep imports

---

## Compound Components Location

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

- server is default
- use "use client" only when needed
- keep boundary minimal

Guidelines:
- app/pages → server
- widgets → mixed
- features → often client
- entities/shared → depends

---

## Routing Rules

- keep routes thin
- move logic to features/entities

---

## Error Boundaries

- use error.tsx per route segment
- place close to failure point
- use global-error.tsx only for root

---

## Splitting

Split feature if:
- >15 files
- multiple responsibilities
- reused elsewhere

---

## Naming

routes → kebab-case  
components → PascalCase

---

## Anti-patterns

- logic in app/page
- client fetching by default
- deep imports
- layer violations

---

## Dependency

Must be used with:

- NEXT-CORE.md