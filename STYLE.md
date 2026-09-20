# MRI Simulator House Style

This document defines the visual and interaction style for the MRI teaching simulators.

The goal is that every simulator should feel like part of the same software suite, even when the scientific visualization and controls are different.

The simulators are **educational MRI visualizations**, not clinical or scanner-control software. The UI should therefore feel like a precise, compact **scientific teaching instrument**.

---

## 1. Design Principles

The visual language should be:

* technical
* restrained
* scientific
* compact
* information-dense
* precise
* unobtrusive
* consistent across simulators

Prefer:

* monospace typography
* thin borders and rules
* compact controls
* restrained colours
* small amounts of rounding
* clear hierarchy through typography and spacing
* visualization-first layouts

Avoid:

* gradients in the UI
* large decorative headings
* pill-shaped controls
* large colourful buttons
* excessive shadows
* excessive rounded cards
* Bootstrap/Material-style generic UI
* decorative illustrations
* unnecessary animation
* excessive whitespace
* changing the visual language for an individual simulator

The interface should feel more like a **scientific instrument console** than a consumer application or SaaS dashboard.

---

# 2. Layout

## Desktop

Use a two-column layout:

```text
┌──────────────────────┬─────────────────────────────────────────────┐
│ CONTROL RAIL         │                                             │
│ ~300 px              │                                             │
│                      │             MAIN VISUALIZATION              │
│ simulator header     │                                             │
│                      │                                             │
│ section              │                                             │
│ controls             │                                             │
│                      │                                             │
│ section              │                                             │
│ controls             │                                             │
│                      │                                             │
│ notes / credits      │                                             │
└──────────────────────┴─────────────────────────────────────────────┘
```

The control rail should be approximately **300 px wide**.

The main visualization occupies the remaining space.

The control rail has a 1 px vertical divider.

The exact arrangement of visualizations is simulator-specific, but the overall geometry should remain consistent.

## Mobile / narrow screens

Use a breakpoint at approximately:

```css
@media (max-width: 1000px)
```

At this breakpoint:

* stack the control rail above the visualization
* change the vertical divider into a horizontal divider
* allow the page to scroll vertically
* stack visualization panels where necessary
* retain the same typography and controls
* do not create a separate mobile visual language

The mobile interface should look like the same application rearranged for a narrow screen.

---

# 3. Typography

Use a monospace system font stack throughout the application:

```css
font-family:
  ui-monospace,
  SFMono-Regular,
  "SF Mono",
  Menlo,
  Consolas,
  "Liberation Mono",
  monospace;
```

Base font size:

```text
13px
```

Avoid introducing additional fonts.

## Simulator title

The simulator title should be:

* approximately 12 px
* semibold
* uppercase
* letter-spacing approximately `0.16em`
* understated

Example:

```text
RELAXATION SIM
```

Do not use a large application title.

## Section headings

Section headings should be:

* approximately 10 px
* uppercase
* semibold
* letter-spacing approximately `0.18em`
* muted/dim colour

Examples:

```text
PLAYBACK
```

```text
TISSUE
```

```text
SEQUENCE
```

Do not use large H2/H3-style headings for control sections.

## Body and controls

Normal labels:

```text
11–13px
```

Explanatory text:

```text
10–11.5px
```

Use line-height around `1.5–1.6` for explanatory text.

Use typography, colour and spacing—not large font sizes—to establish hierarchy.

---

# 4. Colour System

Use CSS variables for all UI colours.

Do not scatter hard-coded colours throughout the application.

## Dark theme

```css
--bg:     #0e1219;
--panel:  #151b24;
--panel2: #1b2230;
--line:   #26303f;

--text:   #ccd6e4;
--muted:  #7c8a9d;
--dim:    #4d5a6b;

--ui:     #2fb6b0;

--btn:    #1b2230;
--btnh:   #232c3c;
--btna:   #2a3547;
```

## Light theme

```css
--bg:     #f2f4f7;
--panel:  #ffffff;
--panel2: #f7f9fb;
--line:   #d7dde5;

--text:   #1b2430;
--muted:  #5f6c7d;
--dim:    #9aa5b3;

--ui:     #0f8f8a;

--btn:    #eef1f5;
--btnh:   #e4e9f0;
--btna:   #d9e0ea;
```

## Colour hierarchy

### Primary text

Dark:

```text
#ccd6e4
```

Light:

```text
#1b2430
```

Use for:

* simulator title
* important values
* primary labels
* important explanatory text

### Muted text

Dark:

```text
#7c8a9d
```

Light:

```text
#5f6c7d
```

Use for:

* control labels
* descriptions
* secondary information

### Dim text

Dark:

```text
#4d5a6b
```

Light:

```text
#9aa5b3
```

Use for:

* section headings
* credits
* tertiary information

### Accent

Dark:

```text
#2fb6b0
```

Light:

```text
#0f8f8a
```

Use sparingly for:

* focus indicators
* slider thumbs
* selected controls
* active states
* important interaction indicators
* primary button borders/text
* dynamic values where appropriate

The accent is an **interaction colour**, not the dominant colour of the application.

---

# 5. UI Colour vs. Physics Colour

This distinction is important.

There are two separate colour systems:

1. **UI colours**
2. **Scientific visualization colours**

The UI palette should remain consistent across the entire simulator suite.

Scientific visualizations may use different colours to represent different physical quantities.

The fundamental rule is:

> **UI colour means interaction. Visualization colour means physics.**

Do not force scientific visualizations to use the teal UI accent.

For example, a simulator may use distinct colours for:

* transverse magnetization
* longitudinal magnetization
* RF
* gradients
* ADC
* magnetic fields
* k-space
* trajectories
* tissue components

These colours should be selected for scientific meaning and readability, not merely to match the UI.

---

# 6. Header

Every simulator should have the same conceptual header:

```text
SIMULATOR NAME                         [VERSION] [LIGHT]
One-line description
```

## Title

The title should be:

* uppercase
* approximately 12 px
* semibold
* letter-spacing approximately `0.16em`

Example:

```text
FIELD SIM
```

## Header controls

Place small utility controls on the same line as the title.

Typical controls:

```text
[0.9.6] [LIGHT]
```

The version control opens the About / credits / changelog dialog.

The theme control switches between light and dark mode.

The theme button should indicate the theme it will switch **to**.

For example:

```text
LIGHT
```

means that clicking the button will switch to light mode.

## Subtitle

Immediately below the title, use a short one-line description.

Example:

```text
Gradient and concomitant Maxwell fields
```

The subtitle should:

* be approximately 11 px
* use the muted colour
* remain concise

Do not place a large descriptive paragraph in the header.

## Sticky header

The header should remain visible when the control rail scrolls.

Recommended approximate padding:

```text
13px 14px 11px
```

with a 1 px bottom border.

---

# 7. Control Sections

Group controls into logical sections.

Use section headings rather than large cards.

Conceptually:

```text
PLAYBACK
──────────────

[ Play ] [ Reset ]

Speed                         1.0×
────────────●─────────────────


ACQUISITION
──────────────

Trajectory
[ EPI                    ▼ ]

Resolution                    32
────────────●─────────────────
```

Prefer horizontal rules to boxed fieldsets.

Section headings should be:

* uppercase
* approximately 10 px
* semibold
* letter-spaced
* dim/muted

Do not visually render every section as a traditional bordered fieldset.

---

# 8. Buttons

Buttons should be compact and technical.

Recommended characteristics:

```css
font-size: 11.5px;
padding: 5px 9px;
border: 1px solid var(--line);
border-radius: 3px;
background: var(--btn);
```

Use the monospace font.

## Normal button

Dark:

```text
background: #1b2230
border:     #26303f
text:       #ccd6e4
```

Light:

```text
background: #eef1f5
border:     #d7dde5
text:       #1b2430
```

## Hover

Slightly lighten the background and/or strengthen the border.

Do not introduce dramatic hover animations.

## Selected / active

Use:

* accent-coloured border
* slightly changed background
* normal or accent text where appropriate

Do not turn the entire button into a large solid teal rectangle.

## Primary buttons

Primary actions should remain understated.

Preferred:

```text
normal button background
teal border
teal text
```

Avoid:

```text
large solid teal rectangle
```

---

# 9. Utility Buttons

Version and theme controls should be even more minimal than ordinary buttons.

Recommended:

```css
font-size: 10px;
letter-spacing: .1em;
text-transform: uppercase;
padding: 3px 7px;
border-radius: 2px;
background: transparent;
```

Example:

```text
[0.9.6] [LIGHT]
```

These should read as small utility controls, not major actions.

---

# 10. Sliders

Use a minimal custom slider.

Recommended appearance:

```text
──────────────●──────────────
```

Track:

```text
height: 2px;
background: var(--line);
```

Thumb:

```text
12px × 12px;
border-radius: 50%;
background: var(--ui);
```

The actual interaction area may be approximately 18 px high even though the visual track is only 2 px.

Do not use a bulky browser-default slider appearance.

## Disabled sliders

Disabled sliders should:

* remain visible
* use approximately 50% opacity
* use a non-interactive cursor

---

# 11. Labels and Values

Adjustable controls should generally use a two-level layout:

```text
Parameter name                         VALUE
───────────────●────────────────────────────
```

Labels:

* muted
* approximately 12 px

Current values:

* primary text colour
* slightly stronger visual hierarchy
* tabular numerals where useful

Do not make every numerical value teal.

Teal is primarily for interaction and state.

---

# 12. Selects and Number Inputs

Select boxes and number inputs should match the button style.

Use:

* panel/secondary-panel background
* 1 px border
* approximately 3 px radius
* monospace font
* approximately 12 px text
* compact padding

Number inputs should generally be right-aligned.

Select menus should generally be left-aligned.

Avoid browser-default styling where practical.

---

# 13. Checkboxes and Radio Buttons

Use native controls where practical.

Set:

```css
accent-color: var(--ui);
```

Labels should remain muted.

Selected state should be clear but visually restrained.

---

# 14. Separators

Prefer 1 px rules over decorative cards.

Dark:

```text
#26303f
```

Light:

```text
#d7dde5
```

Use separators to establish hierarchy between control groups.

The UI should feel like a carefully organized instrument panel rather than a collection of floating cards.

---

# 15. Visualization Panels

Scientific visualization should be the dominant element of the interface.

Panels may be used when they help separate distinct scientific views.

If using panels:

* use the panel background
* use a 1 px border
* use approximately 3–4 px radius
* avoid heavy shadows
* avoid decorative framing

Do not let UI chrome visually compete with the scientific visualization.

---

# 16. Visualization Overlays and HUDs

For information displayed over a visualization:

* use small monospace text
* use a panel or semi-transparent background
* use a thin border
* use small corner radius
* use muted text
* use accent colour only for dynamic/current information

Example:

```text
┌─────────────────────────┐
│ Effective k-space       │
│ Shot       12 / 32      │
│ Time       43.2 ms      │
│ k = (...)               │
└─────────────────────────┘
```

The overlay should remain compact and should never obscure the important scientific content.

---

# 17. Scientific Colour Conventions

Where an established physical convention exists, preserve it.

Possible conventions include:

* Mxy: red
* Mz: blue
* RF: distinct warm/cool colour depending on visualization
* gradients: muted neutral colour
* ADC: amber/yellow
* current cursor/interaction: teal
* warning: amber
* error: red
* tissue components: distinct but restrained colours

These are examples rather than mandatory colours.

When introducing a new scientific quantity:

1. Prefer an existing colour convention if one exists.
2. Avoid introducing unnecessary colours.
3. Make colours semantically meaningful.
4. Ensure sufficient contrast in both themes.
5. Do not confuse visualization colours with UI accent colours.

---

# 18. About / Version Dialog

Every simulator should have an About dialog accessible through the version control.

Include:

1. simulator name
2. author/design attribution
3. short description
4. educational simplifications/caveats
5. changelog
6. related information where appropriate
7. Close button

The dialog should be:

* centered
* compact
* panel-coloured
* thinly bordered
* approximately 4 px radius
* backed by a dark translucent overlay
* monospace
* consistent with the rest of the application

Use horizontal rules to separate sections.

---

# 19. Credits

Credits should appear near the bottom of the control rail.

Use:

* approximately 10 px
* dim colour
* line-height around 1.6
* subtle letter spacing

Credits should not dominate the UI.

---

# 20. Theme Handling

All simulators should share the same theme preference.

Use:

```text
localStorage key: mrisim.theme
```

Possible values:

```text
light
dark
```

On first use:

1. use the saved `mrisim.theme` preference if present
2. otherwise follow `prefers-color-scheme`

When the user changes the theme:

1. immediately update the current simulator
2. save the new preference
3. allow other simulators in the suite to inherit it

This means that choosing dark mode in one simulator should cause another simulator in the suite to start in dark mode.

---

# 21. Focus and Accessibility

All interactive controls must have a visible keyboard focus state.

Recommended:

```css
outline: 2px solid var(--ui);
outline-offset: 2px;
```

Never remove focus indicators.

Controls should have sufficiently large actual hit areas even when their visual appearance is compact.

Respect:

```css
@media (prefers-reduced-motion: reduce)
```

and remove or reduce nonessential animation.

---

# 22. Responsive Behaviour

At approximately 1000 px:

```text
desktop:

┌──────────┬──────────────────────┐
│ controls │ visualization        │
└──────────┴──────────────────────┘
```

becomes:

```text
mobile:

┌─────────────────────────────────┐
│ controls                        │
├─────────────────────────────────┤
│ visualization                   │
└─────────────────────────────────┘
```

The visual identity should remain unchanged.

Only the geometry changes.

---

# 23. Deployment

The simulators should preferably remain self-contained HTML applications.

Avoid dependencies on:

* build systems
* external CSS frameworks
* external fonts
* CDNs
* network connectivity

Prefer:

* one self-contained HTML file
* inline CSS
* inline JavaScript
* bundled/inlined libraries when necessary
* operation from `file://`

A simulator should be usable locally without a development environment.

---

# 24. Educational Tone

The simulators are teaching instruments.

UI text should be:

* concise
* technically accurate
* physically meaningful
* explanatory
* non-marketing

Prefer:

> Signal decays as the transverse components lose phase coherence.

Avoid:

> Execute relaxation calculation.

Prefer terminology from MRI physics rather than implementation terminology.

When an important physical simplification has been made, explain it briefly in the UI or About dialog.

The simulator should make the underlying physics understandable rather than merely exposing software parameters.

---

# 25. Naming

Use short, functional section names.

Prefer:

```text
PLAYBACK
TISSUE
SEQUENCE
GRADIENT
DISPLAY
VIEW
RECORDING
```

Avoid unnecessarily verbose headings such as:

```text
Playback Controls
Simulation Configuration
Advanced Visualization Settings
```

Buttons should also use short functional labels:

```text
Play
Pause
Reset
Reset view
Next
Record
```

Avoid verbose button text.

---

# 26. Adding New UI Components

When a new control or component is required, first attempt to construct it using existing primitives:

* section
* rule
* label/value pair
* button
* slider
* select
* numeric input
* checkbox/radio
* compact panel
* HUD/overlay

Do not introduce a new visual component unless existing primitives genuinely cannot express the required interaction.

When a new component is necessary, derive its:

* typography
* colours
* border
* radius
* spacing
* hover state
* focus state

from the existing house style.

Do not introduce a new colour or visual treatment merely to make the component "stand out."

---

# 27. Consistency Rule

When adding something new, ask:

> **Would this look like it belongs in the existing MRI simulator suite?**

If uncertain, prioritize consistency in this order:

1. layout
2. typography
3. UI colour palette
4. control dimensions
5. spacing
6. interaction conventions
7. simulator-specific styling

Do not redesign the house style for an individual simulator.

---

# 28. LLM Implementation Instructions

When an LLM is asked to create or modify an MRI simulator:

1. Read this `STYLE.md` first.
2. Treat the values and conventions in this document as the canonical design system.
3. Do not invent a new UI style.
4. Do not introduce a CSS framework.
5. Reuse the existing layout and control patterns.
6. Keep the UI compact.
7. Keep scientific visualization colours separate from UI colours.
8. Preserve the dark/light theme system.
9. Preserve the shared `mrisim.theme` preference.
10. Preserve the approximately 1000 px responsive breakpoint.
11. Preserve the approximately 300 px desktop control rail.
12. Use monospace typography.
13. Use teal primarily as an interaction accent.
14. Prefer horizontal r
