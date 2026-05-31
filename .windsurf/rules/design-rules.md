---
trigger: always_on
---

# UI Layout and Visual Consistency Rules

## General Principles

- Maintain strong visual consistency across all case study cards and sections.
- Never create random widths, spacing, or alignment changes unless explicitly instructed.
- The layout should feel clean, structured, editorial, and premium.
- Avoid uneven empty spaces and avoid stretching content edge to edge unnecessarily.

---

## Grid System

### Main Content Width

Use:

- max-width: 1200px
- centered layout (margin: 0 auto)
- horizontal padding: 32px on desktop
- horizontal padding: 20px on tablet/mobile

Never allow sections to span full browser width unless it is a hero section.

---

## Card Layout Rules

### Standard Case Study Card Width

All project cards must:

- use identical widths
- align to the same grid
- maintain equal internal padding
- maintain equal vertical rhythm

Never create one oversized card beside a smaller card unless explicitly designed as a featured layout.

Preferred:

- 2-column desktop grid
- 1-column mobile grid
- consistent gap spacing

Example:
```css
grid-template-columns: repeat(2, minmax(0, 1fr));
gap: 32px;
```

---

## Image and Screenshot Rules

### Screenshot Aspect Ratios

Use only these aspect ratios:

- 16:9 for dashboards
- 4:3 for desktop UI
- 9:16 for mobile screens

Never mix random screenshot dimensions inside the same section.

### Screenshot Containers

Screenshots must:

- use overflow: hidden
- maintain fixed border-radius
- maintain consistent shadow depth
- never stretch disproportionately

Preferred:

- border-radius: 20px
- subtle shadow (e.g., `box-shadow: 0 4px 24px rgba(0,0,0,0.08)`)
- object-fit: cover

---

## Spacing System

Use only this spacing scale (in px):

- 8
- 12
- 16
- 24
- 32
- 48
- 64
- 96

Never introduce arbitrary spacing values (e.g., 15px, 37px, 50px, 70px, 100px).

Maintain consistent vertical rhythm across sections.

---

## Typography Rules

### Headings

Maintain consistent heading hierarchy. Avoid oversized headings unless in hero sections.

Preferred scale:

- H1: 56px
- H2: 40px
- H3: 28px
- Body: 18px

Use balanced line lengths (max-width on text blocks ~700px).

---

## Section Layout Rules

Every section should follow this structure:

1. Section label (small caps or tag)
2. Heading
3. Supporting text
4. Visual content (screenshots, diagrams)
5. Outcome or insight

Avoid random placement of visuals.

---

## White Space Rules

White space should feel intentional.

Avoid:

- huge empty areas beside text
- uneven card heights
- stretched containers
- isolated floating elements

Use auto-balancing where needed (e.g., `align-items: stretch` on grids).

---

## Portfolio Case Study Style

The visual direction should feel:

- minimal
- structured
- editorial
- modern SaaS
- calm
- premium

Avoid:

- clutter
- excessive gradients
- random animations
- oversized UI elements
- inconsistent alignments

---

## Windsurf Instruction

Before generating or editing any UI:

1. Read this file
2. Preserve the existing grid
3. Preserve spacing rhythm
4. Preserve image sizing consistency
5. Match surrounding card dimensions
6. Do not introduce new layout patterns unless asked
