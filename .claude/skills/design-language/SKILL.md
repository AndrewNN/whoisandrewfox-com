---
name: design-language
description: This site's design system — colors, type, spacing, breakpoints, motion, voice. Use when designing, building, or critiquing any page.
---

# whoisandrewfox.com — design language

Not yet written. The designer subagent fills this in from the approved
`docs/brief.md`, and nothing is built against it until it has real values.

Every value must be checkable. A critic has to be able to hold a screenshot
against this file and say yes or no. "Generous spacing" is not a value;
"96px above each section heading" is.

Do not import another site's system into this file. Each site in
`~/Developer/sites/` has its own and they are not interchangeable.

## Sections to fill

- **Palette.** Every colour as a hex value, its role, and its measured
  contrast against each ground it sits on.
- **Type.** Stack, fallbacks, the full scale in px or rem, weights, line
  heights, letter spacing, and which element uses which step.
- **Spacing.** Base unit and the scale built on it. Section rhythm. The page
  gutter at each breakpoint, never below 16px.
- **Breakpoints.** Exact pixel values and what changes at each.
- **Surfaces.** Panel background, border treatment, and when a block earns a
  panel instead of sitting on the ground.
- **Motion.** What moves, how far, how fast, what triggers it, and the
  `prefers-reduced-motion` behaviour, which is required.
- **Voice.** Register, sentence length, and what is never said.

## Constraints carried over from the current build

Fill this in from `CONTEXT.md` and the live code before designing. Anything
here is a floor, not a preference.