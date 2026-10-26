# MRI Simulator House Style

Visual and interaction rules for the MRI teaching simulator suite.

The UI should feel like a **compact scientific instrument**: technical, restrained, precise, and visualization-first.

---

## 1. Core Principles

Use:

* monospace typography
* compact controls
* thin borders/rules
* minimal rounding and shadows
* restrained UI colors
* dark/light themes
* high information density
* clear hierarchy through spacing and typography

Avoid:

* gradients in UI
* large headings
* pill-shaped controls
* large colorful buttons
* heavy shadows
* excessive rounded cards
* Bootstrap/Material-style UI
* decorative elements
* unnecessary animation

**Do not redesign the house style for an individual simulator.**

---

## 2. Layout

### Desktop

```text
┌──────────────────┬──────────────────────────────────────┐
│ CONTROL RAIL     │                                      │
│ ~300 px          │          MAIN VISUALIZATION          │
│                  │                                      │
│ Header           │                                      │
│ Controls         │                                      │
│ Controls         │                                      │
│ Credits          │                                      │
└──────────────────┴──────────────────────────────────────┘
```

* Control rail: ~300 px.
* Visualization fills remaining space.
* 1 px divider between rail and visualization.
* Header remains visible when the rail scrolls.

### Mobile

Breakpoint:

```css
@media (max-width: 1000px)
```

* Stack control rail above visualization.
* Change vertical divider to horizontal.
* Stack visualization panels as needed.
* Keep the same visual styling.

---

## 3. Typography

Use:

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

Base size: **13 px**.

### Simulator title

* ~12 px
* semibold
* uppercase
* `letter-spacing: .16em`

### Section headings

* ~10 px
* semibold
* uppercase
* `letter-spacing: .18em`
* dim color

### Body/controls

* 11–13 px
* muted labels
* primary color for important values

Avoid large typography.

---

## 4. Colors

Use CSS variables. Do not scatter hard-coded UI colors.

### Dark

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

### Light

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

### Color roles

* `--text`: primary text and important values
* `--muted`: labels/descriptions
* `--dim`: section headings/tertiary information
* `--ui`: interaction accent

**UI color means interaction. Visualization color means physics.**

Scientific visualizations may use their own semantic colors.

---

## 5. Header

Structure:

```text
SIMULATOR NAME                 [VERSION] [LIGHT]
One-line description
```

* Title: uppercase, ~12 px, semibold.
* Subtitle: ~11 px, muted.
* Header padding: approximately `13px 14px 11px`.
* Bottom border: 1 px.
* Header is sticky within the control rail.

Version button opens About/changelog.

Theme button indicates the theme it will switch **to**.

Example:

```text
[0.9.6] [LIGHT]
```

---

## 6. Sections

Prefer flat sections separated by rules:

```text
PLAYBACK
──────────────

[ Play ] [ Reset ]

Speed                         1.0×
────────────●─────────────────


SEQUENCE
──────────────
...
```

Do not turn every section into a bordered card.

Section heading:

* ~10 px
* uppercase
* semibold
* `.18em` letter spacing
* dim color

---

## 7. Buttons

Normal button:

```css
font-size: 11.5px;
padding: 5px 9px;
border: 1px solid var(--line);
border-radius: 3px;
background: var(--btn);
```

Use monospace text.

Hover: slightly lighter background.

Active/selected: accent border and subtle background change.

Primary buttons should remain understated:

```text
normal background + teal border + teal text
```

Avoid large solid-color buttons.

---

## 8. Utility Buttons

For version/theme controls:

```css
font-size: 10px;
letter-spacing: .1em;
text-transform: uppercase;
padding: 3px 7px;
border-radius: 2px;
background: transparent;
```

Keep them visually subtle.

---

## 9. Sliders

Use a minimal custom appearance:

```text
──────────────●──────────────
```

* Track: 2 px, `--line`
* Thumb: 12 × 12 px circle, `--ui`
* Interaction area: ~18 px high
* Disabled: ~50% opacity

Do not use bulky browser-default sliders.

---

## 10. Inputs

Selects and number inputs:

* `--panel2` background
* 1 px `--line` border
* ~3 px radius
* monospace
* ~12 px text
* compact padding

Number inputs: generally right-aligned.

Selects: generally left-aligned.

Checkboxes/radios:

```css
accent-color: var(--ui);
```

---

## 11. Labels and Values

Use:

```text
Parameter name                         VALUE
───────────────●────────────────────────────
```

Labels use `--muted`.

Values use `--text`.

Do not make every value teal.

---

## 12. Separators

Use 1 px rules:

```text
dark:  #26303f
light: #d7dde5
```

Prefer rules over decorative cards.

---

## 13. Scientific Visualization

The visualization should dominate the screen.

Panels may be used to separate distinct scientific views:

* 1 px border
* `--panel` background
* ~3–4 px radius
* no heavy shadow

### Visualization colors

Use semantic colors for physical quantities.

Existing conventions should be preserved where applicable, e.g.:

* Mxy: red
* Mz: blue
* ADC: amber/yellow
* gradients: neutral
* interaction/current state: teal

Do not force physics colors to match the UI palette.

---

## 14. Visualization Overlays

For HUDs, legends, and plot labels:

* small monospace text
* thin border
* panel/semitransparent background
* small radius
* muted text
* teal only for dynamic/selected information

Keep overlays compact and unobtrusive.

---

## 15. About Dialog

Every simulator should have an About dialog via the version button.

Include:

* simulator name
* attribution
* short description
* educational caveats
* changelog

Style:

* centered
* panel background
* 1 px border
* ~4 px radius
* translucent backdrop
* compact monospace typography
* horizontal rules

---

## 16. Theme

Use:

```text
localStorage key: mrisim.theme
```

Values:

```text
light
dark
```

On startup:

1. use saved preference if present
2. otherwise use `prefers-color-scheme`

Theme changes should be saved so all simulators share the preference.

---

## 17. Accessibility

All interactive controls need visible keyboard focus.

Recommended:

```css
outline: 2px solid var(--ui);
outline-offset: 2px;
```

Do not remove focus indicators.

Respect:

```css
@media (prefers-reduced-motion: reduce)
```

---

## 18. Educational Tone

Use concise, technically accurate, physical language.

Prefer:

> Signal decays as the transverse components lose phase coherence.

Avoid implementation-oriented wording such as:

> Execute relaxation calculation.

Explain important physical simplifications briefly.

---

## 19. Naming

Use short section names:

```text
PLAYBACK
TISSUE
SEQUENCE
GRADIENT
DISPLAY
VIEW
RECORDING
```

Prefer short button labels:

```text
Play
Pause
Reset
Reset view
Next
Record
```

---

## 20. Deployment

Prefer self-contained HTML:

* no build system
* no external CSS framework
* no external fonts
* no CDN dependencies
* works from `file://`
* inline CSS/JavaScript
* bundle required libraries when necessary

---

## 21. Adding New Components

First reuse existing patterns:

* sections
* rules
* buttons
* sliders
* selects
* inputs
* checkboxes
* panels
* HUDs

Do not introduce new colors or visual treatments unless necessary.

When adding a new component, match the existing:

1. layout
2. typography
3. colors
4. dimensions
5. spacing
6. interaction states

---

## 22. LLM Instructions

When creating or modifying a simulator:

1. Follow this file as the canonical visual specification.
2. Do not invent a new UI style.
3. Keep the ~300 px desktop control rail.
4. Use the ~1000 px responsive breakpoint.
5. Use the monospace font.
6. Use the defined color variables.
7. Use teal primarily for interaction.
8. Keep controls compact.
9. Prefer rules over cards.
10. Keep scientific visualization visually dominant.
11. Preserve dark/light themes and `mrisim.theme`.
12. Add visible keyboard focus.
13. Respect reduced motion.
14. Keep the application self-contained where possible.
15. Preserve established scientific color conventions.
16. If a new visual convention is needed, make it compatible with this guide.
