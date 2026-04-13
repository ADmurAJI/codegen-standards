# React Core Skill

## Context
React 18/19+, TypeScript strict, optional React Compiler.

---

## Principles
- functional components only
- strict typing (no any)
- composition over inheritance
- UI / logic / data separation
- one responsibility per unit

---

## Components

- ≤ 200 LOC
- no business logic in JSX
- pure render

type Props = { title: string }

export const Card = ({ title }: Props) => {
return <div>{title}</div>
}

---

## Composition

- use children for simple composition
- use compound components for complex UI
- avoid prop drilling

---

## Hooks

- one hook = one responsibility
- no UI inside hooks
- no conditional calls
- effects only in useEffect

---

## State

- local first
- no duplicated state
- derived via useMemo

---

## Data Fetching

### Client Components
- no fetch in component body
- use hooks or query libs
- handle loading / error / empty

### Server Components
- direct async data access allowed
- fetch / DB in component body

---

## Events & Memoization

### With React Compiler
- inline handlers allowed
- avoid manual memoization

### Without Compiler
- stabilize refs only when needed

Rules:
- handlers must stay small
- no premature optimization

---

## Forms

- controlled inputs
- validation outside UI
- schema validation (zod/yup)

---

## Performance

- measure first
- avoid unnecessary re-renders
- split components
- colocate state

---

## Error Handling

if (error) return <ErrorState />
if (loading) return <Loader />

---

## Anti-patterns

- business logic in JSX
- duplicated state
- large components
- uncontrolled side-effects

---

## IMPORTANT

Follow architecture rules from:

→ REACT-ARCHITECTURE.md