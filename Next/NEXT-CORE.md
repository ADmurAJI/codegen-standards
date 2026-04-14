# Next.js Core Skill

## Context
Next.js App Router, TypeScript strict.

---

## CORE Rules

- server-first by default
- use `"use client"` only for interactivity/state/effects/browser APIs
- keep server/client boundary explicit and minimal
- pass only serializable server-to-client props
- do not violate architecture boundaries (see `NEXT-ARCHITECTURE.md`)

---

## Server And Client Boundaries

- default to Server Components
- keep client components as leaf nodes when possible
- do not pass functions/classes/DB clients across boundary
- avoid duplicated server+client fetching without explicit reason

---

## Data And Async

- fetch on server by default; normalize data at boundary
- in client components, use hooks/query libs; no direct fetch in render/body
- prefer Server Actions for mutations when suitable
- prevent race conditions; only latest async result may update interactive state

---

## Router

- keep route files thin (orchestration only)
- normalize `params`/`searchParams` at route boundary
- do not pass raw route values deep into UI without normalization
- keep URL and UI state in sync explicitly

---

## Caching And Streaming

- use explicit caching strategy (`cache`, `revalidate`, tags)
- use `Suspense` intentionally for async boundaries

---

## Error Handling

- expected errors → structured typed state
- unexpected errors → segment `error.tsx` / boundary / logs
- do not swallow errors

---

## Performance

- minimize client bundle
- push logic/data work to server when possible
- measure before optimization

---

## IMPORTANT

Use together with:

- NEXT-ARCHITECTURE.md
- NEXT-LINTING.md
