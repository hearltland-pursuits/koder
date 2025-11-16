---
title: CSS Gradients
category: Visual Effects
order: 1
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Gradients

> **Quick Summary:** CSS gradients let you create smooth transitions between two or more colors without using images. There are three types: **linear** (straight line), **radial** (circular/elliptical), and **conic** (360° rotation around a center point).

## Table of Contents
- [Introduction](#introduction)
- [Why Gradients Matter](#why-gradients-matter)
- [Linear Gradients](#linear-gradients)
- [Radial Gradients](#radial-gradients)
- [Conic Gradients](#conic-gradients)
- [Repeating Gradients](#repeating-gradients)
- [Advanced Techniques](#advanced-techniques)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

Before CSS gradients, creating smooth color transitions required **image files** (PNGs, JPEGs). This meant:
- Extra HTTP requests (slower page loads)
- Fixed dimensions (not responsive)
- Difficult to edit (required image editor)
- Accessibility issues (no text alternative)

**CSS gradients** changed everything. Now you can create infinitely scalable, responsive color transitions using pure CSS. Gradients are treated as **background images**, so they work with `background-image`, `background`, and even `mask` properties.

**Key Concept:** Gradients are **generated images** created by the browser at render time. They're not actual image files, so they're infinitely scalable and have zero HTTP overhead.

---

## Why Gradients Matter

### 1. **Performance (No Image Files)**

**Before (image-based):**
```css
.header {
  background-image: url('gradient.png'); /* 50KB file, extra HTTP request */
}
```

**After (CSS gradient):**
```css
.header {
  background-image: linear-gradient(to right, #007bff, #0056b3); /* 0KB, no request */
}
```

### 2. **Responsive & Scalable**

Gradients automatically adapt to container size—no pixelation, no stretching.

### 3. **Modern Design Patterns**

```css
/* Glass morphism effect */
.card {
  background: linear-gradient(135deg, rgba(255,255,255,0.1), rgba(255,255,255,0));
  backdrop-filter: blur(10px);
}

/* Animated gradient backgrounds */
.hero {
  background: linear-gradient(270deg, #ff6b6b, #4ecdc4, #45b7d1);
  background-size: 600% 600%;
  animation: gradientShift 10s ease infinite;
}
```

### 4. **Career Relevance**
- **Interview question:** "How do you create a gradient without images?"
- **Common task:** "Build a modern hero section with gradient background"
- **Framework pattern:** Material Design, iOS gradients (UI kits use CSS gradients)
- **Salary impact:** Modern CSS skills (gradients, animations) = $10-15K more than basic CSS

---

## Linear Gradients

**Definition:** Transitions colors along a **straight line** (top to bottom, left to right, diagonal, or custom angle).

### Basic Syntax

```css
background-image: linear-gradient(direction, color-stop1, color-stop2, ...);
```

### Example 1: Top to Bottom (Default)

```css
.box {
  background-image: linear-gradient(#007bff, #0056b3);
  /* Defaults to "to bottom" direction */
}
```

**Result:** Blue fading to darker blue from top to bottom.

---

### Direction Keywords

```css
/* Top to bottom (default) */
background-image: linear-gradient(to bottom, red, yellow);

/* Left to right */
background-image: linear-gradient(to right, red, yellow);

/* Diagonal (top-left to bottom-right) */
background-image: linear-gradient(to bottom right, red, yellow);

/* Reverse (bottom to top) */
background-image: linear-gradient(to top, red, yellow);
```

---

### Angle-Based Direction

```css
/* 0deg = to top */
background-image: linear-gradient(0deg, red, yellow);

/* 90deg = to right */
background-image: linear-gradient(90deg, red, yellow);

/* 180deg = to bottom */
background-image: linear-gradient(180deg, red, yellow);

/* 45deg = diagonal */
background-image: linear-gradient(45deg, red, yellow);
```

**Angle Guide:**
```
    0deg (↑ to top)
    |
270deg (←) --- 90deg (→ to right)
    |
  180deg (↓ to bottom)
```

---

### Multiple Color Stops

```css
/* Three colors */
background-image: linear-gradient(to right, red, yellow, green);

/* Five colors (rainbow) */
background-image: linear-gradient(
  to right,
  red,
  orange,
  yellow,
  green,
  blue
);
```

---

### Positioning Color Stops

```css
/* Default (even distribution) */
background-image: linear-gradient(to right, red, yellow, green);

/* Custom positions (percentages) */
background-image: linear-gradient(
  to right,
  red 0%,     /* Starts at 0% */
  yellow 50%, /* Middle at 50% */
  green 100%  /* Ends at 100% */
);

/* Sharp transition (no blending) */
background-image: linear-gradient(
  to right,
  red 0% 50%,    /* Red from 0-50% */
  blue 50% 100%  /* Blue from 50-100% */
);
```

**Result (sharp transition):**
```
[====RED====][====BLUE====]
   (0-50%)      (50-100%)
```

---

### Transparent Gradients

```css
/* Fade to transparent */
background-image: linear-gradient(
  to bottom,
  rgba(0, 123, 255, 1),   /* Solid blue */
  rgba(0, 123, 255, 0)    /* Transparent blue */
);
```

**Use Case:** Overlays on images for better text readability.

```css
.hero {
  background-image:
    linear-gradient(to bottom, rgba(0,0,0,0.5), rgba(0,0,0,0.8)),
    url('hero-image.jpg');
}
```

---

## Radial Gradients

**Definition:** Transitions colors in a **circular or elliptical** pattern from a center point.

### Basic Syntax

```css
background-image: radial-gradient(shape size at position, color-stop1, color-stop2, ...);
```

### Example 1: Simple Radial

```css
.box {
  background-image: radial-gradient(circle, #007bff, #0056b3);
}
```

**Result:** Blue circle fading to darker blue from center.

---

### Shape: Circle vs Ellipse

```css
/* Circle (equal width/height) */
background-image: radial-gradient(circle, red, yellow);

/* Ellipse (stretches to container) */
background-image: radial-gradient(ellipse, red, yellow);
```

---

### Size Keywords

```css
/* Closest side */
background-image: radial-gradient(closest-side, red, yellow);

/* Farthest side (default) */
background-image: radial-gradient(farthest-side, red, yellow);

/* Closest corner */
background-image: radial-gradient(closest-corner, red, yellow);

/* Farthest corner */
background-image: radial-gradient(farthest-corner, red, yellow);
```

---

### Positioning the Center

```css
/* Center (default) */
background-image: radial-gradient(circle at center, red, yellow);

/* Top-left corner */
background-image: radial-gradient(circle at top left, red, yellow);

/* Custom position (percentages) */
background-image: radial-gradient(circle at 75% 25%, red, yellow);

/* Pixel positioning */
background-image: radial-gradient(circle at 100px 50px, red, yellow);
```

---

### Spotlight Effect

```css
.spotlight {
  background-image: radial-gradient(
    circle at 50% 50%,
    rgba(255, 255, 255, 0.8) 0%,
    rgba(0, 0, 0, 0.9) 100%
  );
}
```

**Use Case:** Focus attention on specific content areas.

---

## Conic Gradients

**Definition:** Transitions colors in a **360° rotation** around a center point (like a pie chart).

### Basic Syntax

```css
background-image: conic-gradient(from angle at position, color-stop1, color-stop2, ...);
```

### Example 1: Simple Conic

```css
.box {
  background-image: conic-gradient(red, yellow, green, blue, red);
}
```

**Result:** Rainbow spiral from center.

---

### Starting Angle

```css
/* Start at 0deg (top) */
background-image: conic-gradient(from 0deg, red, yellow, green, blue);

/* Start at 90deg (right) */
background-image: conic-gradient(from 90deg, red, yellow, green, blue);
```

---

### Positioning the Center

```css
/* Center (default) */
background-image: conic-gradient(from 0deg at center, red, yellow);

/* Top-left corner */
background-image: conic-gradient(from 0deg at top left, red, yellow);

/* Custom position */
background-image: conic-gradient(from 0deg at 75% 50%, red, yellow);
```

---

### Pie Chart Effect

```css
.pie-chart {
  width: 200px;
  height: 200px;
  border-radius: 50%; /* Make it circular */
  background-image: conic-gradient(
    red 0deg 90deg,       /* 25% red (0-90°) */
    blue 90deg 180deg,    /* 25% blue (90-180°) */
    green 180deg 270deg,  /* 25% green (180-270°) */
    yellow 270deg 360deg  /* 25% yellow (270-360°) */
  );
}
```

**Result:** Four equal pie slices in different colors.

---

## Repeating Gradients

Create **patterns** by repeating gradient sequences.

### Repeating Linear Gradient

```css
/* Striped pattern */
background-image: repeating-linear-gradient(
  45deg,
  #007bff,
  #007bff 10px,
  #0056b3 10px,
  #0056b3 20px
);
```

**Result:** Diagonal stripes alternating between two blues.

### Repeating Radial Gradient

```css
/* Concentric circles */
background-image: repeating-radial-gradient(
  circle,
  red,
  red 10px,
  yellow 10px,
  yellow 20px
);
```

**Result:** Bullseye pattern.

### Repeating Conic Gradient

```css
/* Star burst pattern */
background-image: repeating-conic-gradient(
  from 0deg,
  red 0deg 15deg,
  yellow 15deg 30deg
);
```

---

## Advanced Techniques

### Layering Multiple Gradients

```css
background-image:
  linear-gradient(45deg, rgba(255,255,255,0.1) 25%, transparent 25%),
  linear-gradient(-45deg, rgba(255,255,255,0.1) 25%, transparent 25%),
  linear-gradient(45deg, transparent 75%, rgba(255,255,255,0.1) 75%),
  linear-gradient(-45deg, transparent 75%, rgba(255,255,255,0.1) 75%),
  linear-gradient(to bottom, #007bff, #0056b3);
background-size: 20px 20px, 20px 20px, 20px 20px, 20px 20px, 100% 100%;
```

**Result:** Checkered pattern overlay on gradient.

---

### Animated Gradients

```css
.animated-gradient {
  background: linear-gradient(270deg, #ff6b6b, #4ecdc4, #45b7d1);
  background-size: 600% 600%;
  animation: gradientShift 10s ease infinite;
}

@keyframes gradientShift {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

---

### Text Gradients

```css
.gradient-text {
  background-image: linear-gradient(45deg, #ff6b6b, #4ecdc4);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  color: transparent; /* Fallback */
}
```

**Result:** Rainbow text effect.

---

## Examples

### Example 1: Modern Hero Section

**HTML:**
```html
<div class="hero">
  <h1>Welcome to Our Site</h1>
  <p>Experience the future of web design</p>
</div>
```

**CSS:**
```css
.hero {
  height: 500px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-image: linear-gradient(
    135deg,
    #667eea 0%,
    #764ba2 100%
  );
  color: white;
  text-align: center;
}

.hero h1 {
  font-size: 3rem;
  margin: 0;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
}

.hero p {
  font-size: 1.5rem;
  opacity: 0.9;
}
```

**Result:** Purple-to-pink gradient hero section with centered text.

---

### Example 2: Glass Morphism Card

**CSS:**
```css
.glass-card {
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.1),
    rgba(255, 255, 255, 0)
  );
  backdrop-filter: blur(10px);
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.18);
  padding: 30px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.37);
}
```

**Result:** Frosted glass effect popular in modern UI design.

---

### Example 3: Animated Button

**HTML:**
```html
<button class="gradient-button">Click Me</button>
```

**CSS:**
```css
.gradient-button {
  padding: 15px 40px;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  color: white;
  cursor: pointer;
  background: linear-gradient(90deg, #667eea, #764ba2);
  background-size: 200% auto;
  transition: background-position 0.5s ease;
}

.gradient-button:hover {
  background-position: right center;
}
```

**Result:** Button with sliding gradient on hover.

---

## Common Use Cases

### Use Case 1: Subtle Background Texture
```css
body {
  background: linear-gradient(to bottom, #f8f9fa, #e9ecef);
}
```

---

### Use Case 2: Image Overlay for Text Readability
```css
.hero-image {
  background-image:
    linear-gradient(to bottom, rgba(0,0,0,0.3), rgba(0,0,0,0.7)),
    url('hero.jpg');
  background-size: cover;
}
```

---

### Use Case 3: Loading Skeleton Animation
```css
.skeleton {
  background: linear-gradient(
    90deg,
    #f0f0f0 25%,
    #e0e0e0 50%,
    #f0f0f0 75%
  );
  background-size: 200% 100%;
  animation: loading 1.5s infinite;
}

@keyframes loading {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

---

## Browser Support

| Gradient Type | Chrome | Firefox | Safari | Edge | IE 11 |
|---------------|--------|---------|--------|------|-------|
| `linear-gradient()` | 26+ | 16+ | 6.1+ | 12+ | 10+ (prefix) |
| `radial-gradient()` | 26+ | 16+ | 6.1+ | 12+ | 10+ (prefix) |
| `conic-gradient()` | 69+ | 83+ | 12.1+ | 79+ | None |
| `repeating-*-gradient()` | 26+ | 16+ | 6.1+ | 12+ | 10+ (prefix) |

**IE 11 Prefix:**
```css
background-image: -ms-linear-gradient(to right, red, blue);
```

**Can I Use:** [https://caniuse.com/css-gradients](https://caniuse.com/css-gradients)

---

## Best Practices

### Do This

1. **Use for Performance (Not Images)**
   ```css
   background-image: linear-gradient(to right, #007bff, #0056b3);
   ```

2. **Provide Fallback Colors**
   ```css
   background-color: #007bff; /* Fallback */
   background-image: linear-gradient(to right, #007bff, #0056b3);
   ```

3. **Use Transparency for Overlays**
   ```css
   background-image:
     linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
     url('image.jpg');
   ```

---

### Avoid This

1. **Too Many Colors (Visual Noise)**
   ```css
   /* Avoid */
   background: linear-gradient(red, orange, yellow, green, blue, indigo, violet);
   ```

2. **Forgetting Fallback Color**
   ```css
   /* Bad: No fallback */
   background-image: linear-gradient(to right, red, blue);
   ```

---

## Video Tutorial

**Watch Section:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=3000s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=3000s)

**Additional Resources:**
- [CSS Gradient Generator](https://cssgradient.io/)
- [MDN - CSS Gradients](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Images/Using_CSS_gradients)

---

## Related Topics

**Prerequisites:**
- [Backgrounds](../03-box-model/backgrounds.md)

**Next Steps:**
- [Shadows](shadows.md)
- [Transitions](transitions.md)

---

## Practice Exercise

### Challenge: Build a Gradient Card Collection

**Requirements:**
- [ ] Linear gradient background
- [ ] Radial gradient hover effect
- [ ] Text gradient for heading
- [ ] Animated gradient button

---

### Starter Code

**HTML:**
```html
<div class="card">
  <h2>Gradient Card</h2>
  <p>Hover to see effects</p>
  <button>Learn More</button>
</div>
```

**CSS (Complete this):**
```css
/* Your CSS here */
```

---

## Navigation

**Previous:** [← Attribute Selectors](../08-selectors-advanced/attribute-selectors.md)
**Next:** [Shadows →](shadows.md)
**Up:** [↑ Back to Visual Effects](../README.md#9️⃣-visual-effects-8-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Visual Effects
**Difficulty:** Intermediate
