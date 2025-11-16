---
title: CSS Outline
category: Box Model
order: 7
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Outline

> **Quick Summary:** Outlines draw a line OUTSIDE the border, without affecting layout. Used primarily for focus states on interactive elements. Unlike borders, outlines don't add to element dimensions and don't respect border-radius.

## Table of Contents
- [Introduction](#introduction)
- [Outline vs Border](#outline-vs-border)
- [Outline Properties](#outline-properties)
- [Outline Offset](#outline-offset)
- [Focus States](#focus-states)
- [Accessibility](#accessibility)
- [Examples](#examples)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)

---

## Introduction

**Outline:** A line drawn around elements OUTSIDE the border that doesn't affect page layout.

**Key differences from borders:**
- Doesn't take up space (no layout impact)
- Can't set different sides individually
- Doesn't respect `border-radius` (always rectangular)
- Perfect for focus indicators
- Doesn't cause layout shifts

---

## Outline vs Border

### Visual Comparison

```
┌─────────────────────────────────┐
│ Outline (no layout impact)      │
│  ┌──────────────────────────┐   │
│  │ Border                   │   │
│  │  ┌──────────────────┐    │   │
│  │  │ Padding          │    │   │
│  │  │  ┌──────────┐    │    │   │
│  │  │  │ Content  │    │    │   │
│  │  │  └──────────┘    │    │   │
│  │  └──────────────────┘    │   │
│  └──────────────────────────┘   │
└─────────────────────────────────┘
```

### Property Comparison

| Feature | Border | Outline |
|---------|--------|---------|
| **Affects layout** | Yes | No |
| **Individual sides** | Yes | No |
| **Border radius** | Yes | No |
| **Inside/Outside** | Inside margin | Outside border |
| **Use case** | Visual structure | Focus indicators |

**Example:**
```css
.with-border {
  border: 2px solid blue;
  /* Adds 4px to total width/height */
}

.with-outline {
  outline: 2px solid blue;
  /* No layout change */
}
```

---

## Outline Properties

### Outline Width

```css
.element {
  outline-width: thin | medium | thick | <length>;
}
```

**Examples:**
```css
.thin { outline-width: thin; }
.medium { outline-width: medium; } /* Default */
.thick { outline-width: thick; }
.custom { outline-width: 3px; }
```

### Outline Style

```css
.element {
  outline-style: none | solid | dashed | dotted | double | groove | ridge | inset | outset;
}
```

**Examples:**
```css
.solid { outline-style: solid; }
.dashed { outline-style: dashed; }
.dotted { outline-style: dotted; }
.double { outline-style: double; }
```

**Required:** Must set `outline-style` for outline to show

### Outline Color

```css
.element {
  outline-color: <color>;
}
```

**Examples:**
```css
.blue { outline-color: blue; }
.custom { outline-color: #3498db; }
.transparent { outline-color: rgba(0, 0, 0, 0.3); }
```

### Outline Shorthand

```css
.element {
  outline: [width] [style] [color];
}
```

**Examples:**
```css
.button {
  outline: 2px solid blue;
}

.focus {
  outline: 3px dashed red;
}

/* Order doesn't matter */
.flexible {
  outline: solid 2px blue; /* Same as above */
}
```

---

## Outline Offset

**Property:** `outline-offset`

**Purpose:** Create space between outline and border

```css
.element {
  outline: 2px solid blue;
  outline-offset: 4px; /* 4px gap between border and outline */
}
```

**Values:**
- Positive: Moves outline outward
- Negative: Moves outline inward (overlaps element)
- Zero: No offset (default)

**Examples:**
```css
.outward {
  outline: 2px solid blue;
  outline-offset: 5px; /* Outline pushed away from element */
}

.inward {
  outline: 2px solid red;
  outline-offset: -5px; /* Outline overlaps element */
}
```

---

## Focus States

**Primary use case:** Indicating keyboard focus on interactive elements

### Default Browser Focus

```css
/* Browsers add default focus outline */
button:focus {
  outline: 1px dotted black; /* Browser default (varies) */
}
```

### Custom Focus Outline

```css
.button:focus {
  outline: 3px solid #3498db;
  outline-offset: 2px;
}

.input:focus {
  outline: 2px solid #2ecc71;
  outline-offset: 1px;
}
```

### Focus-Visible (Modern)

**Better approach:** Only show outline for keyboard users

```css
.button:focus-visible {
  outline: 3px solid #3498db;
  outline-offset: 2px;
}

/* Remove outline for mouse clicks */
.button:focus:not(:focus-visible) {
  outline: none;
}
```

---

## Accessibility

**CRITICAL:** Never remove outlines without providing alternatives

### BAD: Removing Outlines

```css
/* VERY BAD - breaks keyboard navigation */
*:focus {
  outline: none; /* DON'T DO THIS */
}
```

### GOOD: Custom Accessible Outlines

```css
/* Good - custom outline */
.button:focus {
  outline: 3px solid #3498db;
  outline-offset: 2px;
}

/* Better - use focus-visible */
.button:focus-visible {
  outline: 3px solid #3498db;
  outline-offset: 2px;
}
```

### Accessibility Guidelines

1. **Always provide focus indicators** (outline or alternative)
2. **Meet WCAG contrast** (3:1 ratio minimum)
3. **Make outlines visible** (thick enough to see)
4. **Don't rely on color alone** (use thickness/offset too)

---

## Examples

### Example 1: Button Focus States

```css
.button {
  padding: 10px 20px;
  border: 2px solid #3498db;
  background: white;
  color: #3498db;
  cursor: pointer;
}

.button:focus-visible {
  outline: 3px solid #2ecc71;
  outline-offset: 2px;
}
```

---

### Example 2: Input Field Focus

```css
.input {
  padding: 10px;
  border: 1px solid #ddd;
}

.input:focus {
  border-color: #3498db;
  outline: 2px solid #3498db;
  outline-offset: 0;
}
```

---

### Example 3: Card Selection

```css
.card {
  padding: 20px;
  border: 1px solid #e0e0e0;
  cursor: pointer;
}

.card:focus {
  outline: 3px solid #3498db;
  outline-offset: 4px;
}

.card.selected {
  border-color: #3498db;
  outline: 3px solid #3498db;
  outline-offset: 4px;
}
```

---

### Example 4: Removing Outline Safely

```css
/* Only remove for mouse users */
.button {
  outline: none; /* Remove default */
}

.button:focus-visible {
  /* Add back for keyboard */
  outline: 3px solid #3498db;
  outline-offset: 2px;
}

/* Or use custom focus style */
.button:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.5);
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE |
|----------|--------|---------|--------|------|-----|
| `outline` | 1+ | 1.5+ | 1.2+ | 12+ | 8+ |
| `outline-offset` | 1+ | 1.5+ | 1.2+ | 12+ | |
| `:focus-visible` | 86+ | 85+ | 15.4+ | 86+ | |

**Note:** `outline-offset` not supported in IE.

---

## Best Practices

### Do This

**1. Always provide focus indicators**
```css
.button:focus-visible {
  outline: 3px solid #3498db;
  outline-offset: 2px;
}
```

**2. Use outline-offset for better UX**
```css
.link:focus {
  outline: 2px solid currentColor;
  outline-offset: 3px; /* Breathing room */
}
```

**3. Match outline color to brand**
```css
:root {
  --focus-color: #3498db;
}

*:focus-visible {
  outline: 3px solid var(--focus-color);
  outline-offset: 2px;
}
```

**4. Use focus-visible for better UX**
```css
/* Only show for keyboard users */
.button:focus-visible {
  outline: 3px solid #3498db;
}
```

### Avoid This

**1. Never remove outlines globally**
```css
/* NEVER DO THIS - accessibility nightmare */
* {
  outline: none !important;
}
```

**2. Don't use outlines for visual design**
```css
/* Bad - use borders instead */
.card {
  outline: 1px solid #ddd; /* Should be border */
}

/* Good */
.card {
  border: 1px solid #ddd;
}
```

**3. Don't rely on outline for layout**
```css
/* Bad - outline doesn't affect layout */
.spacer {
  outline: 20px solid transparent; /* Won't create space */
}

/* Good - use margin/padding */
.spacer {
  margin: 20px;
}
```

---

**Last Updated:** November 15, 2025
**Category:** Box Model
**Difficulty:** Beginner

**Related Topics:**
- [Borders](borders.md) - Border properties
- [Box Model](box-model-concept.md) - Box model fundamentals
- [Focus States](../04-typography/links.md) - Styling interactive elements
- [Accessibility](../13-modern-css/accessibility.md) - Accessible CSS
