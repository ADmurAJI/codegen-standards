# Apple / Linear Premium Style

## Context
Specific style prompt for premium landing pages, SaaS marketing surfaces, portfolio showcases, and editorial product presentations in React, Next.js, and Vue.

Do not use this style for dense CRUD screens, admin panels, or utility-first internal tools.

---

## Core Directive

- produce a calm, premium, high-precision interface with strong spatial rhythm
- prioritize: readability -> accessibility -> responsiveness -> performance -> visual refinement
- vary at least 2 of: layout archetype, media framing, typography scale, motion emphasis
- preserve the existing design system if the product already has one

---

## Style Identity

- design language should feel Apple-esque or Linear-tier: restrained, precise, quiet, premium
- use crisp typography, large whitespace, soft contrast transitions, and minimal but deliberate color
- surfaces should feel machined, layered, and tactile rather than flat
- avoid visual noise, gimmicks, and overloaded decoration

---

## Hard Prohibitions

Do not:

- use `Inter`, `Roboto`, `Arial`, `Open Sans`, or `Helvetica`
- use heavy Lucide, FontAwesome, or Material-style icon sets
- use generic `1px` gray borders or harsh dark drop shadows
- use edge-to-edge sticky navbars glued to the top by default
- use symmetrical 3-column marketing grids with no whitespace tension
- use linear or default `ease-in-out` transitions
- use instant state changes with no interpolation
- use repeated left/right alternation across the page

---

## Preferred Assets

- fonts: `Geist`, `Clash Display`, `PP Editorial New`, `Plus Jakarta Sans`
- icons: ultra-light precise line icons such as `Phosphor Light` or `Remix Line`
- colors: near-black, warm off-white, silver-grey, muted sage, deep espresso, restrained accent tones

---

## Vibe Archetypes

Choose one dominant vibe per page:

- `Ethereal Glass`: near-black background, radial glow fields, geometric grotesk typography, glass surfaces, white hairlines
- `Editorial Luxury`: warm neutrals, serif-led display typography, muted earthy tones, subtle paper or grain feel
- `Soft Structuralism`: white or silver-grey base, bold grotesk type, airy floating surfaces, soft ambient depth

Do not mix multiple vibe systems equally. One must clearly lead.

---

## Layout Archetypes

Choose one dominant layout direction per page:

- `Asymmetrical Bento`: varied card spans, deliberate imbalance, strong whitespace
- `Z-Axis Cascade`: lightly overlapping surfaces with controlled depth and rare restrained rotation
- `Editorial Split`: oversized typography on one side, interactive media or staggered content on the other

Mobile rule:

- all asymmetric layouts must collapse below `768px` into a clear single-column flow with `w-full`, `px-4`, and `py-8`
- do not use `h-screen`; use `min-h-[100dvh]` when full-height treatment is needed
- remove overlap and rotation on mobile when they hurt touch interaction or readability

---

## Composition Rules

- avoid safe layout structures when a stronger composition is possible
- at least one section must break standard flow through scale, composition, or interaction
- prefer asymmetry, overlap, or spatial contrast when it improves hierarchy
- do not let the entire page resolve into repeated equally weighted blocks

---

## Surface Grammar

Default to nested surfaces for major cards, feature panels, media frames, and highlighted content blocks.

`Double-Bezel` pattern:

- outer shell: subtle surface tint, hairline border or ring, small padding, large radius
- inner core: separate background, smaller concentric radius, light inner highlight where appropriate

Use this as the default for primary surfaces, not for every minor UI fragment.

---

## CTA Grammar

- primary CTAs should use rounded pill geometry with generous padding
- when using a trailing icon, place it inside its own nested circular wrapper
- CTA hover should create internal motion tension, not only color change
- active states should feel pressed, not binary

---

## Spacing And Rhythm

- section padding should usually start at `py-24` and may extend to `py-40`
- whitespace must create tension and hierarchy, not emptiness
- typography and media need enough room to feel deliberate and expensive

---

## Motion Grammar

- motion must feel fluid, weighted, and interpolated
- use custom cubic-bezier easing instead of default motion curves
- use staged reveal, fade-up, soft blur resolution, magnetic hover, and controlled menu expansion
- use scroll reveal for key sections, not every single element

Navigation motion:

- floating detached nav pill is preferred over a full-width attached bar
- hamburger transitions should morph into a precise `X`, not disappear abruptly
- expanded navigation should feel like a layered modal surface with staggered content reveal

Button motion:

- hover should affect both outer button and nested icon surface
- icon motion should create diagonal or depth-oriented tension
- pressed state should slightly compress scale

---

## Performance Constraints

- animate only `transform` and `opacity`
- use `will-change` sparingly and only on actively animated elements
- use `IntersectionObserver`, `whileInView`, or equivalent mount-safe viewport triggers
- do not use raw `window.scroll` listeners for continuous animation
- use backdrop blur only on fixed or overlay surfaces, not large scrolling content regions
- keep z-index layering disciplined and systemic

---

## Framework Constraints

### React / Next / Vue

- no side effects in render
- initialize animation only after mount
- use refs instead of broad query selectors
- cleanup animation instances on unmount

### Next.js

- no `window` or `document` usage during SSR
- avoid hydration mismatch from random or time-based values
- use client boundaries only where required
- dynamically import heavy client-only motion code such as `gsap`

### Vue

- initialize motion in `onMounted`
- avoid unnecessary deep watchers
- avoid direct DOM manipulation when framework primitives are sufficient

---

## Failure Conditions

Invalid if:

- banned fonts, icons, borders, or motion patterns appear
- the page looks like a generic template with premium fonts pasted on top
- there is no dominant vibe archetype or layout archetype
- all major sections use the same safe composition
- motion feels default, abrupt, or mechanically flat
- blur is applied to large scrolling areas and causes performance degradation
- the layout does not collapse cleanly on mobile

---

## Pre-Flight

Verify:

- one vibe archetype clearly leads
- one layout archetype clearly leads
- at least one section breaks standard flow
- primary surfaces use nested layering where it matters
- navigation and CTA motion feel interpolated, not default
- spacing is generous enough to create premium rhythm
- mobile collapses to a clean single-column layout
- animation remains GPU-safe
