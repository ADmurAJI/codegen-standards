# React Core Skill

## Context
React 18/19+, TypeScript strict, optional React Compiler.

---

## Rule Levels

### CORE (mandatory)
- functional components only
- strict typing (no any)
- one responsibility per unit
- side-effects must not happen during render
- no direct cross-layer violations (see architecture doc)

### RECOMMENDED
- keep JSX declarative and simple
- separate UI / model / api / lib concerns
- prefer composition over inheritance
- avoid prop drilling

### OPTIONAL
- component LOC targets
- memoization style preferences

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

- target small-to-medium components; split when readability drops
- as a heuristic, 200 LOC is a signal to review, not a hard blocker
- readability degradation is the primary split signal, not LOC
- splitting must not increase cognitive load
- component responsibility should be explainable in one sentence
- if a unit has 2+ independent reasons to change, split it
- keep render pure and predictable
- move complex or repeated business logic out of JSX
- small inline conditions in JSX are acceptable

```tsx
type Props = { title: string };

export const Card = ({ title }: Props) => {
  return <div>{title}</div>;
};
```

---

## Composition

- use children for simple composition
- use compound components for complex UI
- avoid excessive prop drilling (3+ levels)
- prefer composition first, then context

---

## Hooks

- one hook = one responsibility
- hook responsibility should be explainable in one sentence
- hooks should not own UI
- hooks may return render fragments only for headless patterns (rare, documented)
- no conditional calls
- keep side-effects in event handlers or effects depending on lifecycle
- avoid heavy business logic in effects
- do not derive state in effects when it can be computed in render

---

## State

- local first
- avoid duplicated state unless there is a clear reason
- prefer derived values from source state

---

## State Management Decision Rules

- keep transient UI state local to component by default
- place feature-shared client state in `features/*/model`
- promote to app-level store only for truly cross-feature state
- keep server cache in query/data libraries, not in global client stores

---

## Data Fetching

### Client Components
- do not call `fetch` directly in component body
- use api layer + query hooks (React Query/SWR/custom hooks)
- handle loading / error / empty states

### Server Components
- direct async data access is allowed
- fetch / DB access in component body is allowed

---

## Events And Memoization

### With React Compiler
- inline handlers are acceptable
- manual memoization is allowed only when profiling shows value

### Without Compiler
- use memoization when it prevents measured re-render cost
- avoid blanket `useMemo`/`useCallback` usage

Rules:
- handlers must stay small
- no premature optimization

---

## Forms

- controlled inputs by default
- uncontrolled inputs are allowed with form libraries (for example react-hook-form)
- validation outside presentational UI
- schema validation (zod/yup) for non-trivial forms

---

## Performance

- measure first
- avoid unnecessary re-renders
- split components when complexity rises
- colocate state near usage

---

## Async State Consistency

- prevent race conditions in async flows
- cancel stale requests (for example via `AbortController`)
- ensure only latest request updates interactive state

---

## Error Handling

- use error boundaries around unstable UI regions
- keep fallback UI simple and recoverable
- keep expected errors in state, unexpected errors in boundaries

---

## Testability

- business logic should be testable outside React runtime
- `model` and `lib` are primary unit-testing targets
- components should mostly be integration/render targets

---

## Allowed Exceptions

- small inline conditions in JSX
- local state duplication when explicitly justified
- memoization in performance-critical paths with evidence

---

## Anti-patterns

- heavy business workflows embedded in JSX
- duplicated state without reason
- large components with mixed responsibilities
- uncontrolled side-effects

---

## IMPORTANT

Follow architecture rules from:

- REACT-ARCHITECTURE.md
- REACT-LINTING.md
