# Vue Core Skill

## Context
Vue 3/4+, TypeScript strict, Composition API first.

---

## CORE Rules

- use SFC + `<script setup lang="ts">`
- no `any`
- keep template/render pure; no side-effects during render
- all side-effects must be lifecycle/scope-bound
- avoid putting business logic directly in SFC unless trivial
- prefer `model`/composables for reusable logic
- do not violate architecture boundaries (see `VUE-ARCHITECTURE.md`)

---

## Component Boundaries

- component must not contain unrelated UI + business logic
- split when one file mixes orchestration, domain logic, and rendering details
- prefer thin UI components and explicit data/event contracts

---

## Composables

- one composable = one responsibility
- composables must not act as hidden global state unless explicitly designed
- composables that allocate effects/resources must cleanup with `onScopeDispose`

---

## Reactivity And Effects

- use `computed` for derived state; `computed` must be pure and synchronous
- use `watch` for non-trivial side-effects; `watchEffect` only for simple reactive bindings
- prefer `flush: 'post'` for DOM-dependent side-effects
- use `nextTick` when reading DOM after reactive updates
- avoid destructuring/spreading `reactive` state without `toRefs`/`toRef`
- avoid hanging timers/listeners/subscriptions/requests

---

## Context And State

- local state first
- use `provide`/`inject` for deep local context (not global)
- avoid overusing global stores for local context sharing
- use `Teleport` for modals/overlays

---

## Pinia (CORE)

- no UI state in store
- no DOM access in store
- no side-effects in getters
- async actions must expose loading/error
- do not mix server cache with store state

---

## Data And Async

- fetch via `api` + composables, not directly in template/render
- normalize data at boundaries before passing to UI
- avoid `async setup` for fetching unless `Suspense` is intentionally used in project
- event handlers must be explicit about async behavior and state updates

---

## Error Handling

- do not swallow errors
- expected errors → typed state
- unexpected errors -> boundary/logs
- composables must expose error state
- use `onErrorCaptured` for component-level isolation when needed

---

## IMPORTANT

Use together with:

- VUE-ARCHITECTURE.md
- VUE-LINTING.md
