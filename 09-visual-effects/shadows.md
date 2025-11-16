---
title: CSS Shadows
category: Visual Effects
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Shadows

> **Quick Summary:** CSS provides two shadow properties: `box-shadow` (shadows around elements) and `text-shadow` (shadows on text). Shadows add depth, hierarchy, and visual polish to designs without requiring images.

## Table of Contents
- [Introduction](#introduction)
- [Why Shadows Matter](#why-shadows-matter)
- [Text Shadow](#text-shadow)
- [Box Shadow](#box-shadow)
- [Multiple Shadows](#multiple-shadows)
- [Shadow Effects](#shadow-effects)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

Shadows simulate **light sources** in UI design, creating the illusion of depth and layering. Before CSS shadows, designers used:
- Image files (extra HTTP requests, not responsive)
- Photoshop slices (fixed dimensions)
- JavaScript libraries (performance overhead)

CSS shadows revolutionized web design by making depth effects simple, performant, and responsive. Modern design systems (Material Design, Fluent, iOS) rely heavily on shadows for visual hierarchy.

**Key Concept:** Shadows don't just "look nice"—they communicate **affordance** (what's clickable), **elevation** (what's above/below), and **focus** (what's active).

---

## Why Shadows Matter

### 1. **Material Design Elevation System**

```css
/* Cards at different elevations */
.card-1 { box-shadow: 0 1px 3px rgba(0,0,0,0.12); }
.card-2 { box-shadow: 0 3px 6px rgba(0,0,0,0.16); }
.card-3 { box-shadow: 0 10px 20px rgba(0,0,0,0.19); }
```

Higher elevation = larger, softer shadows (appears "floating above" the page).

### 2. **Button States**

```css
button {
  box-shadow: 0 2px 4px rgba(0,0,0,0.2);
}

button:hover {
  box-shadow: 0 6px 12px rgba(0,0,0,0.3); /* Elevates on hover */
}

button:active {
  box-shadow: 0 1px 2px rgba(0,0,0,0.1); /* Pressed down */
}
```

### 3. **Text Readability**

```css
/* Text on busy backgrounds */
h1 {
  color: white;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.8); /* Ensures readability */
}
```

### 4. **Career Relevance**
- **Interview question:** "How do you create depth in UI without images?"
- **Common task:** "Implement Material Design cards"
- **Framework skill:** Bootstrap, Tailwind use shadow utilities extensively

---

## Text Shadow

**Syntax:**
```css
text-shadow: offset-x offset-y blur-radius color;
```

### Basic Text Shadow

```css
h1 {
  text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
}
```

**Parameters:**
- `2px` (offset-x): Shadow moves 2px to the right
- `2px` (offset-y): Shadow moves 2px down
- `4px` (blur-radius): Shadow blur amount
- `rgba(0,0,0,0.5)`: Shadow color (50% black)

---

### Text Shadow Effects

**Embossed Text:**
```css
.embossed {
  color: #333;
  background: #f0f0f0;
  text-shadow: 1px 1px 0 rgba(255,255,255,0.8), -1px -1px 0 rgba(0,0,0,0.3);
}
```

**Neon Glow:**
```css
.neon {
  color: #fff;
  text-shadow:
    0 0 5px #fff,
    0 0 10px #fff,
    0 0 20px #ff00de,
    0 0 40px #ff00de;
}
```

**3D Text:**
```css
.text-3d {
  color: #fff;
  text-shadow:
    1px 1px 0 #ccc,
    2px 2px 0 #bbb,
    3px 3px 0 #aaa,
    4px 4px 0 #999,
    5px 5px 5px rgba(0,0,0,0.5);
}
```

**Long Shadow (Flat Design):**
```css
.long-shadow {
  color: #fff;
  text-shadow:
    1px 1px 0 rgba(0,0,0,0.1),
    2px 2px 0 rgba(0,0,0,0.1),
    3px 3px 0 rgba(0,0,0,0.1),
    4px 4px 0 rgba(0,0,0,0.1),
    5px 5px 0 rgba(0,0,0,0.1);
}
```

---

## Box Shadow

**Syntax:**
```css
box-shadow: offset-x offset-y blur-radius spread-radius color inset;
```

### Basic Box Shadow

```css
.card {
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}
```

**Parameters:**
- `0` (offset-x): No horizontal offset
- `4px` (offset-y): Shadow 4px below element
- `6px` (blur-radius): Blur amount
- `rgba(0,0,0,0.1)`: 10% black shadow

---

### Spread Radius

```css
/* Positive spread = shadow expands */
box-shadow: 0 0 10px 5px rgba(0,0,0,0.3);

/* Negative spread = shadow contracts */
box-shadow: 0 4px 6px -2px rgba(0,0,0,0.1);
```

**Use Case:** Negative spread creates tighter, more realistic shadows.

---

### Inset Shadows (Inner Shadows)

```css
/* Regular (outer) shadow */
box-shadow: 0 4px 6px rgba(0,0,0,0.1);

/* Inner shadow */
box-shadow: inset 0 4px 6px rgba(0,0,0,0.1);
```

**Use Case:** Creating "pressed" or "recessed" effects (buttons, input fields).

```css
input:focus {
  box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);
}
```

---

## Multiple Shadows

Layer shadows for complex effects (comma-separated):

```css
.card {
  box-shadow:
    0 1px 3px rgba(0,0,0,0.12),  /* Small close shadow */
    0 1px 2px rgba(0,0,0,0.24);  /* Larger far shadow */
}
```

### Layered Depth

```css
.elevated-card {
  box-shadow:
    0 2px 4px rgba(0,0,0,0.07),
    0 4px 8px rgba(0,0,0,0.07),
    0 8px 16px rgba(0,0,0,0.07),
    0 16px 32px rgba(0,0,0,0.07);
}
```

**Result:** Ultra-realistic shadow mimicking real-world light diffusion.

---

## Shadow Effects

### Neumorphism (Soft UI)

```css
.neomorphic {
  background: #e0e5ec;
  box-shadow:
    9px 9px 16px rgba(163,177,198,0.6),   /* Dark shadow */
    -9px -9px 16px rgba(255,255,255,0.5); /* Light shadow */
  border-radius: 20px;
}
```

### Glassmorphism

```css
.glass {
  background: rgba(255,255,255,0.1);
  box-shadow: 0 8px 32px rgba(31,38,135,0.37);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255,255,255,0.18);
}
```

### Card Hover Lift

```css
.card {
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

.card:hover {
  box-shadow: 0 12px 24px rgba(0,0,0,0.2);
  transform: translateY(-4px);
}
```

### Glow Effect

```css
.glow-button {
  box-shadow: 0 0 10px rgba(0,123,255,0.5);
}

.glow-button:hover {
  box-shadow: 0 0 20px rgba(0,123,255,0.8);
}
```

---

## Examples

### Example 1: Material Design Card

**HTML:**
```html
<div class="material-card">
  <h3>Card Title</h3>
  <p>Card content goes here.</p>
</div>
```

**CSS:**
```css
.material-card {
  background: white;
  border-radius: 8px;
  padding: 20px;
  box-shadow:
    0 2px 4px rgba(0,0,0,0.07),
    0 4px 8px rgba(0,0,0,0.07);
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

.material-card:hover {
  box-shadow:
    0 4px 8px rgba(0,0,0,0.1),
    0 8px 16px rgba(0,0,0,0.1);
  transform: translateY(-2px);
}
```

---

### Example 2: Input Field with Inner Shadow

**CSS:**
```css
input {
  border: 1px solid #ddd;
  padding: 10px;
  border-radius: 4px;
  box-shadow: inset 0 2px 4px rgba(0,0,0,0.05);
  transition: box-shadow 0.3s;
}

input:focus {
  outline: none;
  border-color: #007bff;
  box-shadow:
    inset 0 2px 4px rgba(0,0,0,0.05),
    0 0 0 3px rgba(0,123,255,0.1);
}
```

---

### Example 3: Neumorphic Button

**CSS:**
```css
.neuro-button {
  background: #e0e5ec;
  border: none;
  padding: 15px 30px;
  border-radius: 50px;
  box-shadow:
    6px 6px 12px rgba(163,177,198,0.6),
    -6px -6px 12px rgba(255,255,255,0.5);
  cursor: pointer;
  transition: all 0.3s;
}

.neuro-button:active {
  box-shadow:
    inset 3px 3px 6px rgba(163,177,198,0.6),
    inset -3px -3px 6px rgba(255,255,255,0.5);
}
```

---

## Common Use Cases

### Use Case 1: Elevation Hierarchy
```css
.low-elevation { box-shadow: 0 1px 3px rgba(0,0,0,0.12); }
.mid-elevation { box-shadow: 0 4px 8px rgba(0,0,0,0.16); }
.high-elevation { box-shadow: 0 10px 20px rgba(0,0,0,0.19); }
```

### Use Case 2: Focus Indicators
```css
button:focus {
  box-shadow: 0 0 0 3px rgba(0,123,255,0.25);
}
```

### Use Case 3: Text Legibility
```css
.hero-text {
  text-shadow: 2px 2px 4px rgba(0,0,0,0.7);
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE 11 |
|----------|--------|---------|--------|------|-------|
| `box-shadow` | ✅ 10+ | ✅ 4+ | ✅ 5.1+ | ✅ 12+ | ✅ 9+ |
| `text-shadow` | ✅ 4+ | ✅ 3.5+ | ✅ 4+ | ✅ 12+ | ✅ 10+ |

**Can I Use:** [https://caniuse.com/css-boxshadow](https://caniuse.com/css-boxshadow)

---

## Best Practices

### ✅ Do This

1. **Use Multiple Shadows for Realism**
   ```css
   box-shadow:
     0 1px 3px rgba(0,0,0,0.12),
     0 1px 2px rgba(0,0,0,0.24);
   ```

2. **Pair Shadows with Transitions**
   ```css
   transition: box-shadow 0.3s ease;
   ```

3. **Use Subtle Shadows (Less is More)**
   ```css
   box-shadow: 0 2px 4px rgba(0,0,0,0.1); /* Subtle */
   ```

---

### ❌ Avoid This

1. **Heavy Shadows Everywhere**
   ```css
   /* Too aggressive */
   box-shadow: 0 20px 50px rgba(0,0,0,0.8);
   ```

2. **Forgetting Performance**
   ```css
   /* Animating box-shadow directly is slow */
   transition: box-shadow 0.3s; /* OK */
   ```

---

## Video Tutorial

**Watch:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=3200s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=3200s)

**Additional Resources:**
- [Box Shadow Generator](https://cssgenerator.org/box-shadow-css-generator.html)
- [Material Design Shadows](https://material.io/design/environment/elevation.html)

---

## Related Topics

**Prerequisites:**
- [Colors Overview](../02-colors/colors-overview.md)

**Next Steps:**
- [2D Transforms](transforms-2d.md)
- [Transitions](transitions.md)

---

## Practice Exercise

### 🎯 Challenge: Create a Material Design Card with Interactive Shadows

**Requirements:**
- [ ] Default state: Subtle shadow
- [ ] Hover state: Elevated shadow + lift animation
- [ ] Active state: Pressed shadow (lower elevation)
- [ ] Bonus: Add text shadow to heading

---

### Starter Code

**HTML:**
```html
<div class="material-card">
  <h3>Card Title</h3>
  <p>This is a Material Design card with interactive shadows.</p>
  <button>Learn More</button>
</div>
```

**CSS (Complete this):**
```css
/* Your CSS here */
```

---

## Navigation

**Previous:** [← Gradients](gradients.md)
**Next:** [2D Transforms →](transforms-2d.md)
**Up:** [↑ Back to Visual Effects](../README.md#9️⃣-visual-effects-8-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Visual Effects
**Difficulty:** Beginner
