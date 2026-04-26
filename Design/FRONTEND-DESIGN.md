# Frontend Design Skill

## Context
Short production prompt for design-heavy frontend work in React, Next.js, and Vue.

Use for:

- landing pages
- promo pages
- showcase sections
- premium product surfaces

---

## Core Directive

- produce non-generic UI with explicit visual decisions
- prioritize: readability -> accessibility -> responsiveness -> performance -> visuals
- do not break usability or existing design systems

---

## Hard Prohibitions

Do not:

- use left/right alternating layouts across the page
- use `center hero + 3 cards + testimonials` as the default composition
- repeat identical cards without variation
- use `max-w-xl` for desktop hero text
- place text directly on images without contrast control
- use more than 3 CTAs per viewport
- use labels like `SECTION 01`, `ABOUT US`

---

## Layout And Spacing

- sections must feel like distinct chapters
- use large vertical spacing, typically `py-24` to `py-48`
- prefer fewer, intentional sections
- prevent horizontal overflow with an explicit root guard such as `overflow-x-hidden`

---

## Composition Requirement

- avoid safe layout structures when a stronger visual composition is possible
- at least one section must break standard flow through composition, scale, or interaction
- prefer asymmetry, overlap, or spatial contrast when it improves hierarchy

---

## Implementation

- use `clamp()` for typography scaling
- avoid magic pixel values when scale can be expressed proportionally
- follow a 4px or 8px spacing rhythm
- prefer utility-first styles if the project already uses them
- avoid deep selector nesting and cascade-heavy styling

---

## Hero

- headline must stay within 2 to 3 lines on desktop
- headline container must be at least `max-w-5xl`
- reduce font size instead of allowing extra wrapping
- use no more than 2 CTAs
- use no more than 1 supporting paragraph
- include a dominant visual anchor such as image, gradient, or motion
- do not use badges, pills, or raw stats by default
- avoid awkward wrapping and orphan words

---

## Typography

- do not default to `Inter`, `system-ui`, or generic `sans-serif`
- use explicit font pairing or a clear single-family hierarchy
- keep at least `1.25x` contrast between adjacent text hierarchy levels
- large headings should use line-height in the `1.0` to `1.2` range
- body text should use line-height in the `1.4` to `1.7` range

---

## Grids

- no empty cells or visually dead space
- bento layouts should use 3 to 5 cards
- spans must resolve cleanly at the target breakpoint
- use `grid-auto-flow: dense` when irregular spans would otherwise create holes

---

## Section Density

- use no more than 3 to 5 primary items per section
- avoid large flat lists in visual sections
- use tabs, carousel, or accordion when content exceeds the section density limit

---

## Cards

- each card should have one primary focus
- avoid multiple competing focal points inside the same card

---

## Content

- headings must be concise and scannable
- paragraphs should stay within 2 to 3 sentences
- do not generate filler marketing text

---

## Color And Contrast

- define one accent role and a neutral base
- use no more than 3 color roles per screen
- text must meet WCAG AA contrast
- control image contrast with overlays, gradients, surfaces, or blur layers

---

## Motion

- motion must support hierarchy, not decoration
- prefer `transform` and `opacity` for animation
- use no more than 2 scroll-driven motion systems
- use no more than 1 pinned section at a time
- define safe initial states to avoid layout jump

Preferred patterns:

- staged entrances
- scale and fade on scroll
- pinned title with scrolling content
- hover lift or scale

---

## Responsive

- design mobile intentionally, not as an afterthought
- collapse complex asymmetrical layouts into a clear vertical flow
- do not allow horizontal scroll unless it is intentional

---

## Accessibility

- maintain contrast, focus states, and keyboard access
- respect reduced-motion preferences
- keep touch targets large enough for mobile interaction

---

## Framework Constraints

### React / Vue / Next

- no side effects in render
- DOM-dependent logic only after mount or in effects
- first render must be deterministic

### Next.js

- no `window` or `document` access during SSR
- avoid hydration mismatch from random or time-based render values
- use `"use client"` only where needed
- use dynamic import for heavy client-only animation code such as `gsap`

### Vue

- avoid direct DOM manipulation when Vue primitives are sufficient
- initialize animation in `onMounted`
- avoid unnecessary deep watchers

### Animation Integration

- initialize animations only after mount
- use refs instead of broad query selectors
- cleanup animations on unmount

---

## Performance

- avoid unnecessary re-renders or reactive cascades
- do not animate large DOM trees
- use virtualization for large lists

---

## Layout Stability

- do not introduce layout shift during animation
- reserve space for media to avoid CLS

---

## Failure Conditions

Invalid if:

- hero exceeds 3 lines on desktop
- primary CTA is not clearly visible
- grid has unintended empty space
- text has low contrast
- repeated layout rhythm dominates the page
- animation causes jank, delay, or layout instability

---

## Pre-Flight

Verify:

- layout is not generic
- hero line count is valid
- spacing is sufficient
- CTA contrast is correct
- no meta-labels were added
- grid has no unintended gaps
- mobile layout is correct
