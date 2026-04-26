# Data-First Terminal Style

## Context
Dense, tool-like interface style for analytics, trading, monitoring, logs, observability, and operator-facing systems.

Use for:

- analytics terminals
- trading interfaces
- monitoring and observability
- logs and ops UI
- infra and operator consoles

Avoid:

- expressive marketing
- portfolio websites
- cinematic storytelling

---

## Core Directive

- design must feel like an instrument, not a lifestyle product
- prioritize: scanability -> density -> structure -> latency -> tone
- every visual decision must improve data reading speed

---

## Style Identity

- dense, disciplined, terminal-adjacent
- tables and lists are first-class citizens
- visual hierarchy comes from alignment, grouping, and signal color
- interface should feel operational, technical, and fast

---

## Hard Prohibitions

Do not:

- use spacious marketing-style layouts
- use decorative gradients, glows, or soft atmospheric effects
- use oversized radius, floating cards, or luxury surface treatment
- use expressive hero sections or oversized brand moments
- use decorative motion or theatrical transitions
- use low-information filler blocks

---

## Typography

- prefer mono or semi-mono families such as `IBM Plex Mono`, `JetBrains Mono`, or mixed mono + neutral sans pairings
- typography must remain highly readable at dense sizes
- use a strict hierarchy: title -> section -> table header -> row -> meta
- avoid dramatic scale jumps and oversized headings
- keep line-height tight but readable

---

## Layout

- use strict column alignment and baseline rhythm
- prefer structured panes, tables, sidebars, and segmented work areas
- keep layout predictable and tool-oriented
- avoid decorative asymmetry and visual theatrics

---

## Spacing

- spacing should be tight, repeatable, and system-driven
- preserve clear grouping even at high density
- avoid wasted whitespace that reduces information throughput
- avoid cramped collisions between controls and data

---

## Data Presentation

- tables, lists, tickers, metrics, and logs must dominate when relevant
- use dense but readable row rhythm
- support scanning through alignment, separators, and consistent value placement
- prioritize comparability over decorative layout variation

---

## Surfaces

- use flat or lightly separated surfaces
- prefer thin borders, dividers, and panel segmentation
- avoid layered decorative containers
- avoid soft premium card aesthetics

---

## Color

- color must act as signal, not decoration
- use a restrained dark or light terminal-like base
- use green, red, amber, cyan, or similar accents only when they communicate state
- avoid multiple decorative accent colors competing for attention
- maintain strong text contrast at all times

---

## Components

- buttons should feel utilitarian and compact
- inputs should be clear, dense, and keyboard-friendly
- tables should be highly structured and sortable-looking
- filters, tabs, and segmented controls should feel operational, not playful

---

## Interaction

- interactions must be immediate and low-latency
- hover and focus states should clarify target and state without theatrics
- keyboard navigation should feel natural and supported by layout

---

## Motion

- motion must be minimal and functional only
- use motion for state updates, focus changes, and panel transitions only
- avoid scroll storytelling, pinning, stagger chains, and cinematic effects

---

## Responsive

- prioritize utility over composition
- preserve access to key data on smaller screens
- collapse secondary panes before degrading primary data visibility
- do not hide critical controls behind decorative breakpoints

---

## Framework Constraints

### React / Next / Vue

- no side effects in render
- first render must be deterministic
- components must remain predictable and testable

### Data-Heavy UI

- use virtualization for large tables and lists
- avoid rendering dense data surfaces without optimization

---

## Performance

- prioritize low latency and high update clarity
- avoid heavy effects, large animated areas, and repaint-heavy surfaces
- dense data must remain readable during updates

---

## Failure Conditions

Invalid if:

- the UI feels like a marketing page instead of a tool
- data density harms readability instead of improving throughput
- decorative color competes with signal color
- layout weakens scanning or comparison
- motion delays operational clarity

---

## Pre-Flight

Verify:

- tables and dense data areas are easy to scan
- alignment feels strict and repeatable
- color behaves as signal
- typography remains readable at dense sizes
- layout feels operational, not decorative
- interaction remains fast and predictable
