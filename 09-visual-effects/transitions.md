---
title: CSS Transitions
category: Visual Effects
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Transitions

> **Quick Summary:** Transitions create smooth animations between CSS property changes (e.g., color, size, position) over a specified duration. They're triggered by state changes like `:hover`, `:focus`, or JavaScript class toggles.

## Table of Contents
- [Introduction](#introduction)
- [Why Transitions Matter](#why-transitions-matter)
- [Basic Syntax](#basic-syntax)
- [Transition Properties](#transition-properties)
- [Timing Functions](#timing-functions)
- [Multiple Transitions](#multiple-transitions)
- [Animatable Properties](#animatable-properties)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

Before CSS transitions, creating smooth animations required:
- **JavaScript** (complex, performance-heavy)
- **jQuery animate()** (library dependency)
- **Flash** (deprecated, not accessible)

**CSS Transitions** simplified animation by handling smooth property changes automatically when states change (hover, focus, class addition).

**Key Concept:** Transitions need a **trigger** (`:hover`, `:focus`, `.active` class) to start. They animate **from** the current state **to** the new state.

---

## Why Transitions Matter

### 1. **User Experience (Smooth Interactions)**

**Without Transition:**
```css
button { background: blue; }
button:hover { background: red; } /* Instant jarring change */
```

**With Transition:**
```css
button {
  background: blue;
  transition: background 0.3s ease;
}
button:hover { background: red; } /* Smooth color fade */
```

### 2. **Performance (GPU Accelerated)**

```css
/* Fast (hardware accelerated) */
transition: transform 0.3s, opacity 0.3s;

/* Slow (causes reflow) */
transition: width 0.3s, height 0.3s;
```

### 3. **Modern UI Patterns**

```css
/* Card hover lift */
.card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}
```

### 4. **Career Relevance**
- **Interview question:** "How do you create smooth hover effects?"
- **Common task:** "Add animations to buttons/cards"
- **Framework skill:** React/Vue state transitions use CSS transitions

---

## Basic Syntax

### Shorthand

```css
transition: property duration timing-function delay;
```

### Example

```css
.button {
  transition: background-color 0.3s ease 0s;
}
```

**Breakdown:**
- `background-color` - Property to animate
- `0.3s` - Duration (300 milliseconds)
- `ease` - Timing function (easing curve)
- `0s` - Delay before starting (optional)

---

## Transition Properties

### transition-property

**Specifies which CSS properties** to animate.

```css
/* Single property */
transition-property: background-color;

/* Multiple properties */
transition-property: background-color, transform, opacity;

/* All animatable properties */
transition-property: all;
```

---

### transition-duration

**How long the transition takes** (seconds or milliseconds).

```css
transition-duration: 0.3s;   /* 300 milliseconds */
transition-duration: 500ms;  /* 500 milliseconds */
transition-duration: 1.5s;   /* 1.5 seconds */
```

**Best Practices:**
- **Quick interactions:** 150-300ms (hover, focus)
- **Medium animations:** 300-500ms (slide, fade)
- **Slow animations:** 500-1000ms (page transitions)

---

### transition-timing-function

**Controls animation acceleration** (easing curve).

```css
/* Linear (constant speed) */
transition-timing-function: linear;

/* Ease (slow start, fast middle, slow end) */
transition-timing-function: ease; /* Default */

/* Ease-in (slow start) */
transition-timing-function: ease-in;

/* Ease-out (slow end) */
transition-timing-function: ease-out;

/* Ease-in-out (slow start and end) */
transition-timing-function: ease-in-out;

/* Custom cubic-bezier */
transition-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);
```

**Visual Guide:**
```
linear:      ────────────────
ease:        ╱──────────╲
ease-in:     ╱─────────────
ease-out:    ─────────────╲
ease-in-out: ╱──────────╲
```

**Cubic Bezier Generator:** [https://cubic-bezier.com/](https://cubic-bezier.com/)

---

### transition-delay

**Waits before starting** the transition.

```css
/* Start immediately */
transition-delay: 0s;

/* Wait 0.2 seconds before starting */
transition-delay: 0.2s;

/* Useful for staggered animations */
.item:nth-child(1) { transition-delay: 0s; }
.item:nth-child(2) { transition-delay: 0.1s; }
.item:nth-child(3) { transition-delay: 0.2s; }
```

---

## Timing Functions

### Built-In Easing Curves

```css
/* Linear - constant speed */
transition: all 0.3s linear;

/* Ease - natural acceleration/deceleration (default) */
transition: all 0.3s ease;

/* Ease-in - slow start */
transition: all 0.3s ease-in;

/* Ease-out - slow end (best for user interactions) */
transition: all 0.3s ease-out;

/* Ease-in-out - slow start and end */
transition: all 0.3s ease-in-out;
```

### Custom Cubic Bezier

```css
/* Bounce effect */
transition: transform 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);

/* Smooth deceleration (Material Design) */
transition: all 0.3s cubic-bezier(0.4, 0.0, 0.2, 1);
```

---

## Multiple Transitions

Animate **multiple properties** with different settings.

### Syntax

```css
transition:
  property1 duration timing-function delay,
  property2 duration timing-function delay;
```

### Example

```css
.button {
  transition:
    background-color 0.3s ease 0s,
    transform 0.2s ease-out 0s,
    box-shadow 0.3s ease 0s;
}

.button:hover {
  background-color: #0056b3;
  transform: scale(1.05);
  box-shadow: 0 4px 12px rgba(0,0,0,0.3);
}
```

---

## Animatable Properties

### Recommended (Hardware Accelerated)

These properties animate smoothly with GPU acceleration:

```css
/* Fast animations */
transition:
  transform 0.3s,
  opacity 0.3s;
```

**List:**
- `transform` (translate, rotate, scale)
- `opacity`

---

### Use Cautiously (May Cause Reflow)

These properties can trigger layout recalculation (slower):

```css
/* Potentially slow */
transition:
  width 0.3s,
  height 0.3s,
  padding 0.3s,
  margin 0.3s;
```

**List:**
- `width`, `height`
- `padding`, `margin`
- `top`, `left`, `right`, `bottom`
- `border-width`

**Recommendation:** Use `transform: scale()` instead of animating `width`/`height`.

---

### Other Commonly Animated Properties

```css
transition:
  background-color 0.3s,
  color 0.3s,
  border-color 0.3s,
  box-shadow 0.3s;
```

---

## Examples

### Example 1: Button Hover Effect

**HTML:**
```html
<button class="btn-primary">Click Me</button>
```

**CSS:**
```css
.btn-primary {
  background: #007bff;
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.btn-primary:hover {
  background: #0056b3;
  transform: translateY(-2px);
}

.btn-primary:active {
  transform: translateY(0);
}
```

---

### Example 2: Card Lift on Hover

**CSS:**
```css
.card {
  background: white;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 12px 24px rgba(0,0,0,0.2);
}
```

---

### Example 3: Dropdown Menu Slide

**HTML:**
```html
<div class="dropdown">
  <button>Menu</button>
  <div class="dropdown-content">
    <a href="#">Item 1</a>
    <a href="#">Item 2</a>
  </div>
</div>
```

**CSS:**
```css
.dropdown-content {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.3s ease-out;
}

.dropdown:hover .dropdown-content {
  max-height: 200px;
}
```

---

### Example 4: Loading Spinner Fade

**CSS:**
```css
.spinner {
  opacity: 0;
  transition: opacity 0.3s ease;
}

.spinner.active {
  opacity: 1;
}
```

---

## Common Use Cases

### Use Case 1: Smooth Color Changes
```css
a {
  color: blue;
  transition: color 0.3s ease;
}
a:hover { color: red; }
```

### Use Case 2: Image Zoom on Hover
```css
.image-container img {
  transition: transform 0.5s ease;
}
.image-container:hover img {
  transform: scale(1.1);
}
```

### Use Case 3: Mobile Menu Slide
```css
.mobile-menu {
  transform: translateX(-100%);
  transition: transform 0.3s ease;
}
.mobile-menu.open {
  transform: translateX(0);
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE 11 |
|----------|--------|---------|--------|------|-------|
| `transition` | 26+ | 16+ | 9+ | 12+ | 10+ |
| All timing functions | 26+ | 16+ | 9+ | 12+ | 10+ |

**Can I Use:** [https://caniuse.com/css-transitions](https://caniuse.com/css-transitions)

---

## Best Practices

### Do This

1. **Use `ease-out` for User-Triggered Actions**
   ```css
   button { transition: all 0.3s ease-out; }
   ```

2. **Keep Durations Short (150-300ms)**
   ```css
   transition: transform 0.2s;
   ```

3. **Animate `transform` and `opacity` for Performance**
   ```css
   transition: transform 0.3s, opacity 0.3s;
   ```

4. **Use Specific Properties (Not `all`)**
   ```css
   /* Good */
   transition: background-color 0.3s, transform 0.3s;

   /* Avoid (animates everything) */
   transition: all 0.3s;
   ```

---

### Avoid This

1. **Animating Layout Properties (Slow)**
   ```css
   /* Slow */
   transition: width 0.3s, height 0.3s;

   /* Fast */
   transition: transform 0.3s; /* Use scale() instead */
   ```

2. **Too Long Durations (Feels Sluggish)**
   ```css
   /* Too slow */
   transition: all 2s;
   ```

3. **Forgetting Vendor Prefixes (Old Browsers)**

---

## Video Tutorial

**Watch:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=3800s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=3800s)

**Additional Resources:**
- [MDN - CSS Transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions)
- [Cubic Bezier Generator](https://cubic-bezier.com/)

---

## Related Topics

**Prerequisites:**
- [2D Transforms](transforms-2d.md)

**Next Steps:**
- [Animations](animations.md)

---

## Practice Exercise

### Challenge: Create an Interactive Button Set

**Requirements:**
- [ ] Button changes color on hover (0.3s)
- [ ] Button lifts up on hover (transform)
- [ ] Button has shadow that grows
- [ ] Pressed state (active) with faster transition

---

## Navigation

**Previous:** [← 3D Transforms](transforms-3d.md)
**Next:** [Animations →](animations.md)
**Up:** [↑ Back to Visual Effects](../README.md#9️⃣-visual-effects-8-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Visual Effects
**Difficulty:** Beginner
