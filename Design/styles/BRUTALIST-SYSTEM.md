# Brutalist System Style

## Context
Controlled digital brutalist style for dev tools, AI products, internal tools with character, and systems that should feel raw but intentional.

Use for:

- dev tools
- AI products with attitude
- internal tools with strong identity
- system interfaces that need deliberate harshness

Avoid:

- conservative enterprise dashboards
- luxury marketing pages
- soft consumer brand UI

---

## Core Directive

- design must feel raw, direct, and unapologetically structured
- prioritize: hierarchy -> contrast -> legibility -> structure -> attitude
- the interface may feel harsh, but never careless

---

## Style Identity

- controlled digital brutalism
- hard edges, sharp contrast, and visible structure
- typography acts as architecture
- ugliness must be intentional, systematic, and readable

---

## Hard Prohibitions

Do not:

- use soft premium gradients, glow, or luxury blur
- use oversized radius, floating glass cards, or gentle lifestyle surfaces
- use decorative complexity without structural purpose
- use chaotic asymmetry that harms reading order
- use playful illustration or cute brand cues
- use motion that softens the interface into generic SaaS polish

---

## Typography

- typography should be bold, structural, and high-contrast
- prefer neutral grotesk or mono-accented pairings such as `IBM Plex Sans`, `Space Grotesk`, `JetBrains Mono`, or similar hard-edged families
- hierarchy must be obvious and assertive
- use typography to create separation before relying on containers
- avoid polished luxury type treatment

---

## Layout

- use visible grid logic and hard-edged composition
- allow asymmetry only when it increases tension without harming clarity
- sections should feel deliberate and forceful, not soft or atmospheric
- avoid floating detached composition with no structural anchors

---

## Spacing

- spacing should be controlled, not airy
- preserve enough room for readability, but avoid luxury emptiness
- use spacing to intensify hierarchy and contrast
- keep grouping strict and intentional

---

## Surfaces

- prefer flat surfaces, hard borders, and sharp divisions
- use little or no radius by default
- surfaces should feel direct and uncompromising
- avoid decorative layering, glass, and over-framed card systems

---

## Color

- use black, white, and one accent color by default
- contrast should be bold and unmistakable
- accent color should create structure or signal, not atmosphere
- avoid soft palettes and over-blended tonal systems

---

## Components

- buttons should feel blunt, obvious, and immediate
- inputs should be clear, hard-edged, and functional
- cards should exist only when they improve structure
- labels, dividers, and blocks should feel system-level, not decorative

---

## Interaction

- interactions must feel immediate and assertive
- hover states can be abrupt, but must remain readable
- focus states must be highly visible
- do not hide function behind overly subtle cues

---

## Motion

- motion should be sparse, sharp, and functional
- use simple transitions for reveal, state, and emphasis only
- avoid cinematic storytelling, soft easing, and decorative choreography

---

## Responsive

- preserve harsh structural clarity on smaller screens
- simplify layout without softening the character into generic mobile SaaS
- keep controls obvious and touch-safe

---

## Framework Constraints

### React / Next / Vue

- no side effects in render
- first render must be deterministic
- components must remain predictable and testable

---

## Performance

- avoid heavy effects and repaint-heavy decoration
- keep the interface fast and direct
- strong contrast must not come at the cost of responsiveness

---

## Failure Conditions

Invalid if:

- the UI feels random instead of intentional
- brutalism reduces readability or hierarchy
- harshness turns into visual chaos
- the result looks like generic SaaS with sharper borders
- attitude overwhelms usability

---

## Pre-Flight

Verify:

- contrast is strong and structural
- typography carries visible hierarchy
- harshness feels intentional rather than sloppy
- components remain usable and obvious
- the interface feels raw, direct, and controlled
