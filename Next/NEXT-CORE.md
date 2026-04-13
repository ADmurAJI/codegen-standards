# Next.js Core Skill

## Context
Next.js App Router, TypeScript strict.

---

## Rule Levels

### CORE (mandatory)
- server-first architecture
- explicit server/client boundaries
- no duplicated data fetching across server and client without reason
- serializable server-to-client props only

### RECOMMENDED
- keep client code minimal
- keep route files thin
- normalize and type data at boundaries
- keep units explainable in one sentence
- if a unit has 2+ independent reasons to change, split it

### OPTIONAL
- additional style constraints not tied to correctness

---

## Client Escalation Criteria (STRICT)

Default: Server Component.

Use `"use client"` only if at least one is true:
- uses local state
- uses effects
- uses browser APIs

If none apply, keep component on server.

---

## AI Generation Workflow

AI generation steps:
1. Define feature boundary
2. Split into `ui` / `model` / `api` / `lib`
3. Write types first
4. Implement model logic
5. Implement UI
6. Connect via hooks
7. Run lint/typecheck and fix CORE violations

---

## Components

### Default
- all components are Server Components by default
- side-effects must not happen during render

### Use `"use client"` only when needed
- interactivity (events, inputs)
- client state (`useState`)
- effects (`useEffect`)
- browser APIs

---

## Server Components

- async components are allowed
- direct data fetching is allowed
- do not use client hooks

```tsx
export default async function Page() {
  const data = await fetch('/api').then((r) => r.json());
  return <div>{data.length}</div>;
}
```

---

## Client Components

- use for interactivity only
- keep them as leaf nodes where possible
- keep side-effects in event handlers or effects depending on lifecycle
- hook responsibility should be explainable in one sentence

---

## Data Fetching

### Server (default)
- fetch on server
- pass typed data via props

### Client
- use only when required by UX/runtime constraints
- do not call `fetch` directly in client component render/body
- prefer hooks/query libs over direct fetch in component body

---

## State Management Decision Rules

- keep transient UI state local by default
- keep feature-shared client state in `features/*/model`
- promote to app-level store only for truly cross-feature state
- keep remote server cache in query/data libraries, not global client stores

---

## Search Params

- read and normalize `searchParams` at route boundary
- use for filtering, sorting, pagination
- pass typed normalized values downward

---

## Server To Client Props

- pass only serializable data
- no functions/classes/DB clients
- map domain objects to plain transport objects

---

## Mutations

- prefer Server Actions
- prefer `action` / `formAction` for form-driven flows
- avoid unnecessary client -> API -> server loops

Client-side:
- use `useTransition` when needed to keep UI responsive

---

## Forms

- controlled inputs by default
- uncontrolled inputs are allowed with form libraries (for example react-hook-form)
- keep validation in schemas/services instead of view-only components

---

## Error Handling

### Expected errors
- do not throw for validation/business errors
- return structured state

### Unexpected errors
- let them bubble to `error.tsx`
- use segment-level error boundaries

---

## Caching

- use explicit fetch caching strategy (`cache`, `revalidate`, tags)
- choose strategy per data volatility

---

## Streaming

- use Suspense for async UI boundaries
- split long async sections into smaller loading islands

---

## Async State Consistency

- prevent race conditions in interactive fetch flows
- cancel stale requests (for example via `AbortController`)
- ensure latest request wins for UI state updates

---

## Routing

- keep file-based routes thin
- move business logic to features/entities/model

---

## Performance

- minimize client bundle
- push logic to server when possible
- lazy-load heavy interactive UI
- measure before optimizing
- splitting must not increase cognitive load

---

## Testability

- business logic should be testable outside React runtime
- `model` and `lib` are primary unit-testing targets
- route files/components should stay thin and test mostly behavior/integration

---

## Allowed Exceptions

- client-side fetch in truly client-only scenarios (with justification)
- temporary mixed boundary during migration/refactor (tracked)
- selective memoization for proven hot paths

---

## Anti-patterns

- `"use client"` everywhere
- client fetching by default
- duplicated fetch (server + client) without intent
- non-serializable props crossing boundary

---

## IMPORTANT

This skill must be used together with:

- NEXT-ARCHITECTURE.md
- NEXT-LINTING.md
