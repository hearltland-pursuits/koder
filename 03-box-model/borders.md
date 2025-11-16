---
title: CSS Borders
category: Box Model
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Borders

> **Quick Summary:** CSS borders add visible outlines around elements. Control border width, style (solid, dashed, dotted), color, and radius (rounded corners). Borders sit between padding and margin in the box model.

## Table of Contents
- [Introduction](#introduction)
- [Border Properties](#border-properties)
- [Border Width](#border-width)
- [Border Style](#border-style)
- [Border Color](#border-color)
- [Border Shorthand](#border-shorthand)
- [Individual Sides](#individual-sides)
- [Border Radius](#border-radius)
- [Examples](#examples)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)

---

## Introduction

Borders define element boundaries visually. They add visual weight, create separation, and guide user attention. Unlike outlines (which don't affect layout), borders are part of the box model—they add to element dimensions (unless using `box-sizing: border-box`).

**Key Concept:** Borders require THREE properties: width, style, and color. Without `border-style`, borders won't display.

---

## Border Properties

**Three core properties:**

| Property | Controls | Required |
|----------|----------|----------|
| `border-width` | Thickness | Optional (default: medium) |
| `border-style` | Line type | **Required** |
| `border-color` | Color | Optional (default: text color) |

**Minimum to show a border:**
```css
.element {
  border-style: solid; /* MUST have style */
}
```

---

## Border Width

**Property:** `border-width`

**Values:** `thin`, `medium` (default), `thick`, length values

### Examples

```css
/* Keywords */
.thin { border-width: thin; }
.medium { border-width: medium; }
.thick { border-width: thick; }

/* Length values */
.custom { border-width: 2px; }
.large { border-width: 10px; }

/* Different sides (top, right, bottom, left) */
.varied { border-width: 5px 10px 15px 20px; }

/* Two values (top/bottom, left/right) */
.symmetric { border-width: 5px 10px; }
```

---

## Border Style

**Property:** `border-style`

**Values:** `none`, `solid`, `dashed`, `dotted`, `double`, `groove`, `ridge`, `inset`, `outset`

### Examples

```css
/* No border (default) */
.none { border-style: none; }

/* Solid line (most common) */
.solid { border-style: solid; }

/* Dashed line */
.dashed { border-style: dashed; }

/* Dotted line */
.dotted { border-style: dotted; }

/* Double line */
.double { border-style: double; }

/* 3D effects */
.groove { border-style: groove; }
.ridge { border-style: ridge; }
.inset { border-style: inset; }
.outset { border-style: outset; }
```

**Visual Preview:**
```
solid:  ──────────────
dashed: ─ ─ ─ ─ ─ ─ ─
dotted: ∙ ∙ ∙ ∙ ∙ ∙ ∙
double: ══════════════
```

---

## Border Color

**Property:** `border-color`

**Values:** Any CSS color

### Examples

```css
/* Named color */
.red { border-color: red; }

/* HEX */
.blue { border-color: #3498db; }

/* RGB */
.green { border-color: rgb(46, 204, 113); }

/* RGBA (transparent) */
.transparent { border-color: rgba(0, 0, 0, 0.3); }

/* Different sides */
.rainbow { border-color: red green blue yellow; }

/* Inherits text color (default) */
.inherit { border-color: currentColor; }
```

---

## Border Shorthand

**Combine all properties:**

```css
.element {
  border: [width] [style] [color];
}
```

### Examples

```css
/* Standard border */
.card {
  border: 1px solid #ddd;
}

/* Thick colored border */
.box {
  border: 5px solid #3498db;
}

/* Dashed border */
.dotted-box {
  border: 2px dashed #e74c3c;
}

/* Order doesn't matter */
.flexible {
  border: solid 2px red; /* Same as above */
}
```

**Most common pattern:**
```css
.card {
  border: 1px solid #e0e0e0;
  padding: 20px;
  border-radius: 8px;
}
```

---

## Individual Sides

**Control each side separately:**

### Long Form

```css
.element {
  border-top: 3px solid red;
  border-right: 2px dashed blue;
  border-bottom: 1px solid green;
  border-left: 4px dotted yellow;
}
```

### Common Patterns

**Bottom border only (underline effect):**
```css
.underline {
  border-bottom: 2px solid #3498db;
}
```

**Left accent bar:**
```css
.card {
  border-left: 4px solid #3498db;
  padding-left: 20px;
}
```

**No top border:**
```css
.box {
  border: 1px solid #ddd;
  border-top: none;
}
```

---

## Border Radius

**Property:** `border-radius`

**Creates rounded corners**

### Examples

```css
/* All corners equal */
.round {
  border-radius: 10px;
}

/* Perfect circle (for square elements) */
.circle {
  width: 100px;
  height: 100px;
  border-radius: 50%;
}

/* Different corners (top-left, top-right, bottom-right, bottom-left) */
.varied {
  border-radius: 10px 20px 30px 40px;
}

/* Two values (top-left/bottom-right, top-right/bottom-left) */
.diagonal {
  border-radius: 10px 30px;
}

/* Pill shape */
.pill {
  border-radius: 50px;
  padding: 10px 30px;
}

/* Individual corners */
.custom {
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
```

---

## Examples

### Example 1: Card Component

```css
.card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 20px;
  background-color: white;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.card:hover {
  border-color: #3498db;
}
```

---

### Example 2: Button with Border

```css
.button-outline {
  border: 2px solid #3498db;
  color: #3498db;
  background-color: transparent;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s;
}

.button-outline:hover {
  background-color: #3498db;
  color: white;
}
```

---

### Example 3: Sidebar with Left Accent

```css
.sidebar-item {
  border-left: 4px solid transparent;
  padding: 15px;
  transition: border-color 0.3s;
}

.sidebar-item.active {
  border-left-color: #3498db;
  background-color: #f0f0f0;
}
```

---

### Example 4: Dashed Separator

```css
.separator {
  border: none;
  border-top: 2px dashed #ddd;
  margin: 40px 0;
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE |
|----------|--------|---------|--------|------|----|
| `border` | 1+ | 1+ | 1+ | 12+ | 4+ |
| `border-radius` | 4+ | 4+ | 5+ | 12+ | 9+ |
| Individual sides | 1+ | 1+ | 1+ | 12+ | 4+ |

---

## Best Practices

### ✅ Do This

1. **Use Subtle Borders for Cards**
   ```css
   .card {
     border: 1px solid #e0e0e0; /* Light, not distracting */
   }
   ```

2. **Use Shorthand**
   ```css
   /* Good - concise */
   border: 2px solid #3498db;

   /* Avoid - verbose */
   border-width: 2px;
   border-style: solid;
   border-color: #3498db;
   ```

3. **Add Border Radius for Modern Look**
   ```css
   .button {
     border: 2px solid #3498db;
     border-radius: 5px; /* Softer edges */
   }
   ```

### ❌ Avoid This

1. **Don't Forget `border-style`**
   ```css
   /* Bad - border won't show */
   .element {
     border-width: 5px;
     border-color: red;
   }

   /* Good */
   .element {
     border: 5px solid red;
   }
   ```

2. **Don't Use Excessive Border Width**
   ```css
   /* Bad - overwhelming */
   border: 20px solid black;

   /* Good - balanced */
   border: 2px solid #333;
   ```

---

**Last Updated:** November 15, 2025
**Category:** Box Model
**Difficulty:** Beginner
