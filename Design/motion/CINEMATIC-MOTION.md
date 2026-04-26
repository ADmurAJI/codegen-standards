# Cinematic Motion Style

## Context
High-end motion-driven design for landing pages, product storytelling, and immersive editorial UI.

Use for:

- marketing pages with narrative flow
- product storytelling sections
- interactive showcases

Do not use for:

- CRUD interfaces
- dashboards
- form-heavy flows

This prompt is additive. It is meant to complement an existing visual style prompt, not replace it.

---

## Core Directive

- design must be motion-first, not layout-first
- motion defines hierarchy, pacing, and focus
- prioritize: readability -> performance -> motion clarity -> visuals
- at least one section must rely on scroll-driven storytelling

---

## Style Identity

- cinematic, layered, immersive
- strong sense of depth, timing, and reveal
- UI should feel like a sequence of scenes, not static blocks
- avoid decorative motion; every animation must communicate structure

---

## Hard Prohibitions

Do not:

- use static layouts without motion in key sections
- animate layout properties such as `top`, `left`, `width`, or `height`
- use default easing such as `ease` or `ease-in-out`
- trigger all elements at once on scroll
- stack multiple unrelated animations in one viewport
- use GSAP timelines without clear sequencing purpose

---

## Motion Requirement

- at least one section must use scroll-driven animation with `GSAP ScrollTrigger` or equivalent controlled orchestration
- motion must create progression, not just appearance
- animations must be staged, not simultaneous
- animated elements must have stable initial layout before animation starts

Motion budget:

- limit to 2 to 3 distinct animated sections per page
- do not animate every section; leave static contrast where appropriate

---

## Motion Architecture

Use one primary motion system per page:

- `Scroll Narrative`: pinned section with progressive reveal
- `Layered Reveal`: elements enter with depth and timing offsets
- `Stacking Cards`: elements overlap and reorder on scroll
- `Horizontal Scene`: horizontal movement driven by vertical scroll

Do not mix multiple systems equally. One must clearly dominate.

---

## GSAP Usage

- use `gsap` with `ScrollTrigger` for scroll-driven sections
- initialize only after mount with `useEffect`, `onMounted`, or equivalent client-side lifecycle
- use refs, not global selectors
- prefer timeline-based orchestration
- timelines should remain concise and clearly sequenced
- avoid deeply nested or overly long timelines

Allowed patterns:

- pin + scrub
- staggered reveal
- scale + opacity progression
- parallax depth layering

---

## Motion Grammar

- motion must feel weighted and interpolated
- use custom cubic-bezier curves
- animate with slight delay offsets or stagger
- maintain contrast between animated and static sections to preserve visual rhythm

Preferred effects:

- scale from `0.9` to `1`
- opacity from `0` to `1`
- blur reduction from `blur(12px)` to `blur(0)`
- vertical shift from `y: 40` to `0`
- use blur sparingly and avoid applying it to large or frequently updated elements

---

## Scroll Behavior

- pinned sections must have clear entry and exit
- avoid long dead scroll zones
- scrolling must always reveal new information
- use scrub only for sections that benefit from direct scroll coupling
- avoid scrub on multiple sections in the same viewport

---

## Layout And Composition

- layout must support motion, not fight it
- prefer large sections with fewer elements
- avoid dense grids in motion-heavy areas
- at least one section must break normal flow through overlap, pinning, or layering

---

## Depth And Layering

- use 2 to 3 depth layers per section
- background, content, and foreground must be visually distinguishable
- overlapping elements must not block primary content

---

## Performance Constraints

- animate only `transform` and `opacity`
- limit to 1 pinned section visible at a time
- avoid animating large DOM trees
- use `IntersectionObserver` or `ScrollTrigger` instead of raw scroll listeners
- use `will-change` only on active elements

---

## Responsive Behavior

- disable or simplify pinned sections on mobile when needed
- collapse motion-heavy layouts into vertical flow
- remove overlap if it breaks usability
- ensure touch interactions remain reliable

---

## Framework Constraints

### React / Next / Vue

- no side effects in render
- initialize animations after mount
- cleanup GSAP instances on unmount

### Next.js

- no `window` access during SSR
- use dynamic import for GSAP-heavy sections when appropriate
- prevent hydration mismatch

### Vue

- initialize motion in `onMounted`
- avoid direct DOM manipulation where possible

---

## Failure Conditions

Invalid if:

- page feels static despite the motion requirement
- animations are decorative and not structural
- multiple motion systems compete in one viewport
- motion causes jank or frame drops
- pinned sections trap the user or break scroll flow
- mobile experience degrades due to animation

---

## Pre-Flight

Verify:

- one dominant motion system is clearly defined
- at least one scroll-driven section exists
- motion reveals content progressively
- animations are GPU-safe
- layout supports motion instead of contradicting it
- mobile fallback is clean and usable
