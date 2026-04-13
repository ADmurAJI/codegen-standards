# Next.js Core Skill

## Context
Next.js App Router, TypeScript strict.

---

## Principles

- server-first architecture
- minimal client code
- explicit boundaries
- no duplicated data fetching

---

## Components

### Default
- all components are Server Components

### Use "use client" ONLY if:
- interactivity (events, inputs)
- state (useState)
- effects (useEffect)
- browser APIs

---

## Server Components

- async components allowed
- direct data fetching allowed
- no client hooks

export default async function Page() {
const data = await fetch('/api').then(r => r.json())
return <div>{data.length}</div>
}

---

## Client Components

"use client"

- for interactivity only
- keep as leaf nodes

---

## Data Fetching

### Server (default)
- fetch on server
- pass data via props

### Client
- only if required
- use hooks / query libs

---

## Search Params

- page receives searchParams as Promise
- await in Server Components
- use for filtering, sorting, pagination
- normalize at route boundary
- pass typed values down

---

## Server → Client Props

- pass only serializable data
- no functions / classes / DB clients
- map to plain objects

---

## Mutations

- prefer Server Actions
- use form action / formAction by default
- avoid client → API → server loops

Client-side:
- use useTransition when needed
- keep UI responsive

---

## Error Handling

### Expected errors
- do not throw for validation/business logic
- return structured state

### Unexpected errors
- let them bubble to error.tsx
- use segment-level error boundaries

---

## Caching

fetch(url, { cache: 'force-cache' })
fetch(url, { next: { revalidate: 60 } })

---

## Streaming

- use Suspense
- split async UI

---

## Routing

- file-based routing
- keep routes thin

---

## Performance

- minimize client bundle
- push logic to server
- lazy load heavy UI

---

## Anti-patterns

- "use client" everywhere
- client fetching by default
- duplicated fetch (server + client)
- non-serializable props

---

## Architecture Dependency

This skill must be used together with:

- NEXT-ARCHITECTURE.md