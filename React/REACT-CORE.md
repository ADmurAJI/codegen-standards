# React Core Skill

## Context
React 18/19+, TypeScript strict, optional React Compiler.

---

## CORE Rules

- functional components only
- no `any`
- keep render pure; no side-effects during render
- avoid putting business logic directly in components unless trivial
- prefer `model`/hooks for reusable logic
- no architecture boundary violations (see `REACT-ARCHITECTURE.md`)

---

## Component Boundaries

- component must not contain unrelated UI + business logic
- split when one unit mixes orchestration, domain logic, and rendering details
- prefer thin UI components and explicit props/events contracts

---

## Hooks And Effects

- one hook = one responsibility
- no conditional hooks
- effects only for side-effects; no derived state in effects
- side-effects must be explicit and lifecycle-controlled
- cleanup subscriptions/timers/requests

---

## State

- local state first
- avoid duplicated state
- keep server cache in query/data libs, not in global client stores
- promote to app store only for truly cross-feature state

---

## Data And Async

- use `api` + query hooks; avoid direct `fetch` in component render/body
- normalize data at boundaries before UI
- prevent race conditions; only latest async result may update state
- event handlers must be explicit about async behavior and state updates

---

## Data Fetching Strategy (CORE)

- use one data layer consistently (`TanStack Query` or `SWR`)
- no manual caching in components
- no duplication of server state in client stores
- colocate queries with `feature/api`
- mutations must invalidate or update cache explicitly
- map server errors to typed UI state

---

## Data Mapping

- do not use raw API response directly in UI
- map DTO -> domain model in `api` layer/adapters
- UI must depend on stable domain shape

---

## Forms

- use one form approach consistently (`React Hook Form` or `Formik`)
- colocate validation schemas (`zod`/`yup`)
- no uncontrolled side-effects in form handlers
- form state must not leak into global stores

---

## Side Effects

- side-effects only in event handlers, effects, or async actions in model layer
- never in render
- never in pure helpers

---

## Server Components Constraints (if used)

- no client-only libraries in Server Components
- no stateful client hooks in Server Components
- data must be serialized safely across boundaries
- avoid passing large objects through props
- prefer streaming/partial rendering when useful
- server-side errors must be handled by boundaries/route-level error handling

---

## Memoization

- with React Compiler: avoid manual memoization unless profiling proves value
- without Compiler: use `useMemo`/`useCallback` only for measured bottlenecks
- no blanket memoization

---

## Error Handling

- do not swallow errors
- expected errors → typed state
- unexpected errors -> error boundaries/logs

---

## Performance

- avoid unnecessary re-renders (stable props, stable keys)
- use virtualization for large lists
- avoid heavy computations in render
- measure before optimizing

---

## Naming

- boolean props: `is*` / `has*` / `can*`
- event handlers: `on*`
- async function naming must be consistent project-wide (`verb` or `verbAsync`)

---

## IMPORTANT

Use together with:

- REACT-ARCHITECTURE.md
- REACT-LINTING.md
