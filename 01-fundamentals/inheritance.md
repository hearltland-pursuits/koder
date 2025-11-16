---
title: CSS Inheritance & Cascade
category: Fundamentals
order: 7
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Inheritance & Cascade

> **Quick Summary:** CSS properties flow down from parent to child elements (inheritance) and combine through specificity rules (cascade). Understanding these concepts prevents style conflicts and creates maintainable stylesheets.

## Table of Contents
- [Introduction](#introduction)
- [What is Inheritance](#what-is-inheritance)
- [Inherited vs Non-Inherited Properties](#inherited-vs-non-inherited-properties)
- [The Cascade](#the-cascade)
- [Specificity](#specificity)
- [Controlling Inheritance](#controlling-inheritance)
- [Examples](#examples)
- [Best Practices](#best-practices)

---

## Introduction

CSS has two fundamental concepts that determine which styles apply:

1. **Inheritance:** Properties children automatically get from parents
2. **Cascade:** How CSS resolves conflicting rules

**Together they answer:** "Why does my element look like this?"

---

## What is Inheritance

**Inheritance:** Child elements automatically receive certain style properties from their parent elements.

**Example:**
```html
<div style="color: blue; font-family: Arial;">
  <p>This text is blue and Arial</p>
  <span>This too!</span>
</div>
```

**Why inheritance exists:**
- Reduces code repetition
- Creates visual consistency
- Simplifies styling large documents

---

## Inherited vs Non-Inherited Properties

### Properties That Inherit

**Typography properties:**
```css
.parent {
  /* These inherit to children */
  color: blue;
  font-family: Arial;
  font-size: 16px;
  font-weight: bold;
  line-height: 1.5;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 1px;
}
```

**List properties:**
```css
ul {
  list-style: none; /* Inherits to <li> */
}
```

**Visibility:**
```css
.parent {
  visibility: hidden; /* Inherits */
  cursor: pointer; /* Inherits */
}
```

### Properties That DON'T Inherit

**Box model properties:**
```css
.parent {
  /* These DON'T inherit to children */
  width: 500px;
  height: 300px;
  margin: 20px;
  padding: 10px;
  border: 1px solid black;
}
```

**Positioning:**
```css
.parent {
  /* These DON'T inherit */
  position: absolute;
  top: 0;
  left: 0;
  z-index: 100;
}
```

**Background:**
```css
.parent {
  /* These DON'T inherit */
  background-color: blue;
  background-image: url('image.jpg');
}
```

**Flexbox/Grid:**
```css
.parent {
  /* These DON'T inherit */
  display: flex;
  flex-direction: column;
  grid-template-columns: 1fr 1fr;
}
```

---

## The Cascade

**Cascade:** The algorithm CSS uses to determine which rule wins when multiple rules target the same element.

### Cascade Order (Highest to Lowest Priority)

**1. Importance**
```css
.box {
  color: blue !important; /* Highest priority */
}
```

**2. Inline Styles**
```html
<div style="color: red;"> <!-- Higher than stylesheet -->
```

**3. Specificity**
```css
#id { } /* Specificity: 1-0-0 */
.class { } /* Specificity: 0-1-0 */
element { } /* Specificity: 0-0-1 */
```

**4. Source Order**
```css
.box { color: blue; }
.box { color: red; } /* This wins (comes last) */
```

---

## Specificity

**Specificity:** How CSS determines which selector is "more specific."

### Specificity Calculation

| Selector Type | Specificity | Example |
|--------------|-------------|---------|
| Inline style | 1-0-0-0 | `style="color: red"` |
| ID | 0-1-0-0 | `#header` |
| Class, attribute, pseudo-class | 0-0-1-0 | `.nav`, `[type="text"]`, `:hover` |
| Element, pseudo-element | 0-0-0-1 | `div`, `p`, `::before` |
| Universal | 0-0-0-0 | `*` |

### Specificity Examples

```css
/* Specificity: 0-0-0-1 */
p {
  color: black;
}

/* Specificity: 0-0-1-0 - wins */
.text {
  color: blue;
}

/* Specificity: 0-1-0-0 - wins */
#main {
  color: green;
}

/* Specificity: 0-1-1-1 - highest, wins */
#main .text p {
  color: red;
}
```

**Specificity rule:** More specific selectors override less specific ones.

---

## Controlling Inheritance

### The `inherit` Keyword

**Force inheritance:**
```css
.child {
  padding: inherit; /* Use parent's padding value */
  background-color: inherit; /* Use parent's background */
}
```

**Use case:** Make non-inheriting properties inherit
```css
.button {
  border: inherit; /* Normally doesn't inherit */
}
```

### The `initial` Keyword

**Reset to default browser value:**
```css
.reset {
  color: initial; /* Browser default (usually black) */
  padding: initial; /* 0 */
}
```

### The `unset` Keyword

**Smart reset:** Acts like `inherit` if property normally inherits, otherwise acts like `initial`.

```css
.smart-reset {
  color: unset; /* Inherits (color normally inherits) */
  padding: unset; /* Resets to 0 (padding doesn't inherit) */
}
```

### The `revert` Keyword

**Reset to user agent stylesheet:**
```css
.revert {
  all: revert; /* Reset everything to browser default */
}
```

---

## Examples

### Example 1: Inheritance Chain

```html
<body style="font-family: Arial; color: #333;">
  <div style="color: blue;">
    <p>
      This text is:
      - Font: Arial (inherited from body)
      - Color: blue (inherited from div)
    </p>
  </div>
</body>
```

```css
/* Equivalent CSS */
body {
  font-family: Arial;
  color: #333;
}

div {
  color: blue; /* Overrides inherited #333 */
}

p {
  /* Inherits font-family from body */
  /* Inherits color from div */
}
```

---

### Example 2: Specificity Battle

```css
/* Specificity: 0-0-0-1 */
p {
  color: black;
}

/* Specificity: 0-0-1-0 - wins */
.intro {
  color: blue;
}

/* Specificity: 0-0-1-1 - wins */
p.intro {
  color: green;
}

/* Specificity: 0-1-1-1 - wins */
#header p.intro {
  color: red;
}
```

```html
<div id="header">
  <p class="intro">I'm red!</p>
</div>
```

---

### Example 3: Cascade Order

```css
/* These all target .box */
.box {
  color: red; /* Declared first */
}

.box {
  color: blue; /* Same specificity, later = wins */
}
```

Result: Box is blue (source order wins).

---

### Example 4: Forcing Inheritance

```css
/* Buttons normally don't inherit font-family */
body {
  font-family: 'Roboto', sans-serif;
}

button {
  font-family: inherit; /* Now uses Roboto */
}
```

---

## Best Practices

### Do This

**1. Use inheritance to reduce code**
```css
/* Good - set once on body */
body {
  font-family: Arial, sans-serif;
  color: #333;
  line-height: 1.6;
}

/* All children automatically get these */
```

**2. Keep specificity low**
```css
/* Good - easy to override */
.button {
  color: blue;
}

/* Bad - hard to override */
#header nav ul li a.button {
  color: blue;
}
```

**3. Understand cascade order**
```css
/* Good - organized by specificity */
/* 1. Elements */
p { }

/* 2. Classes */
.text { }

/* 3. IDs (sparingly) */
#main { }
```

### Avoid This

**1. Don't abuse !important**
```css
/* Bad - makes everything harder */
.button {
  color: blue !important;
  padding: 10px !important;
}

/* Good - fix specificity instead */
.header .nav .button {
  color: blue;
}
```

**2. Don't use overly specific selectors**
```css
/* Bad - too specific */
body div.container div.row div.col p.text {
  color: blue;
}

/* Good */
.text {
  color: blue;
}
```

**3. Don't fight inheritance**
```css
/* Bad - repeating inherited values */
body { font-family: Arial; }
p { font-family: Arial; }
span { font-family: Arial; }

/* Good - let inheritance work */
body { font-family: Arial; }
/* Everything else inherits automatically */
```

---

## Inheritance Cheat Sheet

| Property Type | Inherits? |
|--------------|-----------|
| Typography (font, color, text) | Yes |
| Box Model (padding, margin, border) | No |
| Positioning (position, top, left) | No |
| Background (color, image) | No |
| Display (flex, grid, block) | No |
| List styles | Yes |
| Table styles | Yes |
| Visibility | Yes |

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|-----|
| Inheritance | 1+ | 1+ | 1+ | 12+ | 3+ |
| Cascade | 1+ | 1+ | 1+ | 12+ | 3+ |
| `inherit` | 1+ | 1+ | 1+ | 12+ | 8+ |
| `initial` | 1+ | 1+ | 1.2+ | 12+ | |
| `unset` | 41+ | 27+ | 9.1+ | 13+ | |
| `revert` | 84+ | 67+ | 9.1+ | 84+ | |

---

**Last Updated:** November 15, 2025
**Category:** Fundamentals
**Difficulty:** Intermediate

**Related Topics:**
- [CSS Selectors](selectors.md) - Targeting elements
- [CSS Specificity](../08-selectors-advanced/specificity.md) - Advanced specificity rules
- [CSS Syntax](syntax.md) - CSS rule structure
