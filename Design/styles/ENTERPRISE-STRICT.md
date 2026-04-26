# Enterprise Strict Style

## Context
Strict, structured design for enterprise apps, fintech platforms, B2B SaaS, and data-heavy interfaces.

Use for:

- dashboards
- analytics
- admin panels
- enterprise landing pages

Avoid:

- storytelling
- expressive marketing
- portfolios

---

## Core Directive

- design must be precise, controlled, and deterministic
- prioritize: clarity -> readability -> structure -> performance -> tone
- every decision must improve comprehension

---

## Style Identity

- grid-driven, disciplined, minimal
- no decoration; clarity first
- visual weight comes from alignment and spacing
- UI should feel engineered and predictable

---

## Hard Prohibitions

Do not:

- use gradients, glow, or blur-heavy surfaces
- use large border radius or pill UI
- use unjustified asymmetry
- use floating detached components
- use decorative motion
- use inconsistent layout variation

---

## Typography

- use neutral fonts such as `Inter`, `IBM Plex Sans`, `Source Sans 3`, or `Roboto`
- do not use display fonts
- use a strict hierarchy: title -> section -> label -> body -> meta
- heading line-height should remain in the `1.2` to `1.3` range
- body line-height should remain in the `1.4` to `1.6` range
- body width should usually remain within `max-w-2xl` to `max-w-3xl`
- avoid large scale jumps

---

## Layout

- use a consistent 4px or 8px grid
- align everything to columns
- prefer symmetrical or balanced composition
- avoid overlap and z-axis layering
- containers must be repeatable and predictable

---

## Spacing

- use token-based spacing only
- avoid large empty gaps
- spacing separates logic, not decor
- keep related elements tightly grouped

---

## Grids

- use standard grids only; avoid bento layouts
- avoid irregular spans unless they are data-driven
- avoid empty or visually unbalanced areas

---

## Section Density

- allow higher density than marketing layouts
- group related data tightly
- avoid unnecessary section splits

---

## Surfaces

- use flat or lightly elevated surfaces
- prefer `border` or `ring` over shadow
- avoid decorative layering or glass

---

## Color

- use a restrained palette
- use a neutral base and one accent
- do not use competing accents
- color communicates state, not style
- strong text contrast is required

---

## Components

- buttons should be rectangular or slightly rounded
- inputs should have clear borders and no glow
- tables should be structured and readable
- cards should be minimal and functional
- tables and dense data areas must prioritize scanability over visual styling

---

## Interaction

- interactions must be immediate and predictable
- hover states should be subtle
- focus states must be strong and visible

---

## Motion

- motion must be minimal and functional only
- duration should usually remain in the `100ms` to `300ms` range
- use `linear` or `ease-out` easing
- do not use scroll animation, pinning, stagger chains, or complex timelines

---

## Responsive

- prioritize usability over composition
- layouts must degrade predictably
- do not hide critical interaction or information behind layout tricks

---

## Framework Constraints

### React / Next / Vue

- no side effects in render
- first render must be deterministic
- components must remain predictable and testable

### Data-Heavy UI

- use virtualization for large lists
- avoid large unoptimized tables

---

## Performance

- avoid heavy visual effects
- avoid large animated areas
- prioritize low latency

---

## Failure Conditions

Invalid if:

- UI feels decorative
- layout is misaligned or inconsistent
- multiple accents are used
- spacing feels arbitrary
- hierarchy is unclear
- motion distracts from content

---

## Pre-Flight

Verify:

- grid alignment is consistent
- typography hierarchy is clear
- spacing is consistent
- color usage is minimal
- interaction feedback is immediate
- UI feels stable and predictable
