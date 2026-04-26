# Scientific Lab Style

## Context
Structured research-oriented interface style for ML platforms, biomedical tools, quantitative analysis, scientific dashboards, and experimental systems.

Use for:

- ML and model inspection tools
- research dashboards
- biomedical and lab systems
- quantitative analytics
- experiment and evaluation interfaces

Avoid:

- expressive brand marketing
- playful consumer UI
- cinematic storytelling

---

## Core Directive

- design must feel like a research instrument
- prioritize: clarity -> measurement -> structure -> readability -> restraint
- every visual decision must support analysis, comparison, or interpretation

---

## Style Identity

- sterile, precise, analytical
- minimal decoration with high structural clarity
- visual emphasis comes from charts, metrics, axes, grids, and measured spacing
- interface should feel methodical, trustworthy, and research-grade

---

## Hard Prohibitions

Do not:

- use marketing-style hero composition
- use decorative gradients, glows, or luxury surfaces
- use playful icons, expressive illustration, or brand-heavy ornament
- use aggressive asymmetry or overlap without analytical reason
- use cinematic motion or theatrical transitions
- use filler sections that do not contribute to understanding

---

## Typography

- prefer neutral, highly readable fonts such as `IBM Plex Sans`, `Inter`, `Source Sans 3`, or restrained mono pairings
- typography must feel measured and calm, not promotional
- use a strict hierarchy: title -> section -> metric -> label -> body -> meta
- avoid oversized display moments
- keep line-height clean and controlled

---

## Layout

- use clean grids, axes, panels, and repeatable modules
- align charts, metrics, and controls with explicit structural rhythm
- prefer balanced scientific composition over expressive layout gestures
- avoid unnecessary layering and decorative framing

---

## Spacing

- spacing should be clean, rational, and repeatable
- maintain enough whitespace for interpretation, but avoid marketing-style emptiness
- group related evidence closely
- separate analytical blocks clearly

---

## Data And Visualization

- charts, metrics, plots, tables, and measured comparisons should lead the interface
- labels, legends, scales, and values must remain readable
- visualization styling must support interpretation before aesthetics
- avoid chart ornament that weakens analytical trust

---

## Surfaces

- use flat, clean, lightly separated surfaces
- prefer thin borders, subtle dividers, and clear panel logic
- avoid decorative nesting, glass, or soft premium layering

---

## Color

- use restrained, research-friendly color logic
- base palette should remain neutral or sterile
- use accent colors to distinguish signals, categories, or states
- avoid decorative color drama
- contrast must remain strong for labels, values, and chart elements

---

## Components

- controls should look precise and reliable
- tables and metric cards should feel systematic, not branded
- filters, toggles, and selectors should support analytical workflows
- component styling must stay secondary to information clarity

---

## Interaction

- interactions must feel precise and predictable
- hover, focus, and selected states should reveal analytical utility
- avoid theatrical feedback
- support workflows that involve repeated comparison and inspection

---

## Motion

- motion must be minimal and explanatory
- use motion only for state change, focus guidance, and chart-safe transitions
- avoid scroll storytelling, pinning, long staggers, and cinematic sequences

---

## Responsive

- preserve readability of charts, tables, and controls on smaller screens
- simplify layout without hiding key analytical meaning
- degrade panels predictably and keep workflows intact

---

## Framework Constraints

### React / Next / Vue

- no side effects in render
- first render must be deterministic
- components must remain predictable and testable

### Data-Heavy UI

- use virtualization where data volume requires it
- avoid large analytical surfaces without optimization

---

## Performance

- prioritize stable rendering and clear analytical feedback
- avoid heavy decorative effects and large animated areas
- charts and data panels must stay responsive under load

---

## Failure Conditions

Invalid if:

- the UI feels promotional instead of analytical
- charts or metrics are visually secondary to decoration
- layout weakens interpretation or comparison
- color styling reduces measurement clarity
- motion distracts from research work

---

## Pre-Flight

Verify:

- charts, metrics, and controls lead the interface
- the layout feels measured and research-oriented
- labels and values remain readable
- color usage supports interpretation
- the UI feels precise, calm, and trustworthy
- interaction supports analysis rather than spectacle
