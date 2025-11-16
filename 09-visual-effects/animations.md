---
title: CSS Animations
category: Visual Effects
order: 6
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Animations

> **Quick Summary:** CSS animations use `@keyframes` to define multi-step animations that run automatically (without user interaction). Unlike transitions (which need triggers), animations can loop, reverse, and play on page load.

## Table of Contents
- [Introduction](#introduction)
- [Why Animations Matter](#why-animations-matter)
- [Keyframes](#keyframes)
- [Animation Properties](#animation-properties)
- [Animation Shorthand](#animation-shorthand)
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

**Transitions** animate from **state A to state B** (triggered by hover, focus, etc.).

**Animations** create **complex, multi-step sequences** that run:
- Automatically on page load
- In loops (infinite or counted)
- With delays and direction control

Before CSS animations:
- **JavaScript** (complex timing logic)
- **jQuery** (library dependency)
- **Flash** (deprecated, accessibility issues)

**CSS Animations** simplified complex motion design with pure CSS.

**Key Concept:** Animations = `@keyframes` (define steps) + `animation` property (apply to element).

---

## Why Animations Matter

### 1. **Attention-Grabbing (No User Interaction Needed)**

```css
/* Loading spinner - runs automatically */
.spinner {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
```

### 2. **Complex Multi-Step Sequences**

```css
/* Bounce effect with multiple stages */
@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  25% { transform: translateY(-20px); }
  50% { transform: translateY(0); }
  75% { transform: translateY(-10px); }
}
```

### 3. **Brand Identity (Logo Animations, Mascots)**

```css
.logo {
  animation: fadeInScale 1s ease-out;
}

@keyframes fadeInScale {
  from {
    opacity: 0;
    transform: scale(0.5);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
```

### 4. **Career Relevance**
- **Interview question:** "How do you create a loading spinner?"
- **Common task:** "Add page load animations"
- **Framework skill:** React Transition Group, Vue transitions use CSS animations

---

## Keyframes

**Defines animation steps** using percentages or `from`/`to`.

### Basic Syntax

```css
@keyframes animation-name {
  from { /* Starting state */ }
  to { /* Ending state */ }
}
```

### Percentage-Based Keyframes

```css
@keyframes slideIn {
  0% {
    transform: translateX(-100%);
    opacity: 0;
  }
  50% {
    transform: translateX(-10%);
    opacity: 0.5;
  }
  100% {
    transform: translateX(0);
    opacity: 1;
  }
}
```

### Combining Keyframes

```css
/* Multiple properties at each step */
@keyframes complexAnimation {
  0% {
    transform: translateX(0) rotate(0deg);
    background-color: red;
  }
  50% {
    transform: translateX(100px) rotate(180deg);
    background-color: blue;
  }
  100% {
    transform: translateX(0) rotate(360deg);
    background-color: red;
  }
}
```

---

## Animation Properties

### animation-name

**Specifies which `@keyframes`** to use.

```css
animation-name: slideIn;
animation-name: bounce, fadeIn; /* Multiple animations */
```

---

### animation-duration

**How long the animation takes** (full cycle).

```css
animation-duration: 2s;     /* 2 seconds */
animation-duration: 500ms;  /* 500 milliseconds */
```

---

### animation-timing-function

**Easing curve** (same as transitions).

```css
animation-timing-function: ease;           /* Default */
animation-timing-function: linear;         /* Constant speed */
animation-timing-function: ease-in;        /* Slow start */
animation-timing-function: ease-out;       /* Slow end */
animation-timing-function: ease-in-out;    /* Slow start and end */
animation-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);
```

---

### animation-delay

**Waits before starting** animation.

```css
animation-delay: 0s;    /* Start immediately */
animation-delay: 1s;    /* Wait 1 second */
animation-delay: -1s;   /* Start 1 second into animation */
```

---

### animation-iteration-count

**How many times to repeat**.

```css
animation-iteration-count: 1;        /* Run once (default) */
animation-iteration-count: 3;        /* Run 3 times */
animation-iteration-count: infinite; /* Loop forever */
```

---

### animation-direction

**Playback direction**.

```css
animation-direction: normal;            /* Forward (default) */
animation-direction: reverse;           /* Backward */
animation-direction: alternate;         /* Forward, then backward */
animation-direction: alternate-reverse; /* Backward, then forward */
```

**Example (Pendulum Effect):**
```css
.pendulum {
  animation: swing 2s ease-in-out infinite alternate;
}

@keyframes swing {
  from { transform: rotate(-30deg); }
  to { transform: rotate(30deg); }
}
```

---

### animation-fill-mode

**Styles before/after animation**.

```css
animation-fill-mode: none;      /* Default (no styles applied) */
animation-fill-mode: forwards;  /* Keep final state */
animation-fill-mode: backwards; /* Apply first keyframe before start */
animation-fill-mode: both;      /* Both forwards and backwards */
```

**Example:**
```css
.fade-in {
  opacity: 0;
  animation: fadeIn 1s ease-out forwards; /* Stays visible after */
}

@keyframes fadeIn {
  to { opacity: 1; }
}
```

---

### animation-play-state

**Pause/resume animation**.

```css
animation-play-state: running; /* Default */
animation-play-state: paused;  /* Freeze animation */
```

**Use Case:**
```css
.animated-element {
  animation: spin 2s linear infinite;
}

.animated-element:hover {
  animation-play-state: paused; /* Pause on hover */
}
```

---

## Animation Shorthand

```css
animation: name duration timing-function delay iteration-count direction fill-mode play-state;
```

### Examples

```css
/* Name, duration */
animation: fadeIn 1s;

/* Name, duration, timing, delay */
animation: slideIn 0.5s ease-out 0.2s;

/* Name, duration, infinite loop */
animation: spin 2s linear infinite;

/* Full shorthand */
animation: bounce 1s ease-in-out 0s infinite alternate both running;

/* Multiple animations */
animation:
  fadeIn 1s ease-out,
  slideUp 0.5s ease-out 0.5s;
```

---

## Advanced Techniques

### Staggered Animations (Cascade Effect)

```css
.item:nth-child(1) { animation-delay: 0s; }
.item:nth-child(2) { animation-delay: 0.1s; }
.item:nth-child(3) { animation-delay: 0.2s; }
.item:nth-child(4) { animation-delay: 0.3s; }
```

### Chaining Animations

```css
.element {
  animation:
    fadeIn 0.5s ease-out,
    slideUp 0.5s ease-out 0.5s; /* Starts after fadeIn */
}
```

### Pausing on Hover

```css
.card {
  animation: float 3s ease-in-out infinite;
}

.card:hover {
  animation-play-state: paused;
}
```

---

## Examples

### Example 1: Loading Spinner

**HTML:**
```html
<div class="spinner"></div>
```

**CSS:**
```css
.spinner {
  width: 50px;
  height: 50px;
  border: 5px solid #f3f3f3;
  border-top: 5px solid #007bff;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
```

---

### Example 2: Pulse Effect (Call-to-Action Button)

**CSS:**
```css
.cta-button {
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% {
    transform: scale(1);
    box-shadow: 0 0 0 0 rgba(0, 123, 255, 0.7);
  }
  50% {
    transform: scale(1.05);
    box-shadow: 0 0 0 20px rgba(0, 123, 255, 0);
  }
}
```

---

### Example 3: Fade In on Page Load

**CSS:**
```css
.hero-section {
  opacity: 0;
  animation: fadeInUp 1s ease-out forwards;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

---

### Example 4: Bouncing Ball

**CSS:**
```css
.ball {
  width: 50px;
  height: 50px;
  background: #007bff;
  border-radius: 50%;
  animation: bounce 1s ease-in-out infinite;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
    animation-timing-function: ease-out;
  }
  50% {
    transform: translateY(-100px);
    animation-timing-function: ease-in;
  }
}
```

---

### Example 5: Typing Effect

**CSS:**
```css
.typing {
  width: 0;
  overflow: hidden;
  white-space: nowrap;
  border-right: 2px solid #333;
  animation:
    typing 3s steps(30) forwards,
    blink 0.75s step-end infinite;
}

@keyframes typing {
  from { width: 0; }
  to { width: 100%; }
}

@keyframes blink {
  50% { border-color: transparent; }
}
```

---

## Common Use Cases

### Use Case 1: Loading Indicators
```css
@keyframes spin {
  to { transform: rotate(360deg); }
}
```

### Use Case 2: Attention Grabbers (Pulse, Shake)
```css
@keyframes shake {
  0%, 100% { transform: translateX(0); }
  25% { transform: translateX(-10px); }
  75% { transform: translateX(10px); }
}
```

### Use Case 3: Page Entrance Animations
```css
@keyframes slideInFromLeft {
  from { transform: translateX(-100%); }
  to { transform: translateX(0); }
}
```

### Use Case 4: Infinite Background Animations
```css
@keyframes gradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE 11 |
|----------|--------|---------|--------|------|-------|
| `@keyframes` | 43+ | 16+ | 9+ | 12+ | 10+ |
| `animation` | 43+ | 16+ | 9+ | 12+ | 10+ |

**Vendor Prefixes (Older Browsers):**
```css
@-webkit-keyframes spin {
  to { -webkit-transform: rotate(360deg); }
}

.element {
  -webkit-animation: spin 1s linear infinite;
  animation: spin 1s linear infinite;
}
```

**Can I Use:** [https://caniuse.com/css-animation](https://caniuse.com/css-animation)

---

## Best Practices

### Do This

1. **Use `transform` and `opacity` for Performance**
   ```css
   @keyframes fade {
     to { opacity: 0; transform: translateY(20px); }
   }
   ```

2. **Keep Animations Short (< 1s for UI)**
   ```css
   animation: fadeIn 0.5s;
   ```

3. **Use `forwards` to Keep Final State**
   ```css
   animation: slideIn 1s forwards;
   ```

4. **Respect `prefers-reduced-motion`**
   ```css
   @media (prefers-reduced-motion: reduce) {
     * {
       animation: none !important;
       transition: none !important;
     }
   }
   ```

---

### Avoid This

1. **Too Many Simultaneous Animations**
2. **Animating Layout Properties (width, height)**
3. **Ignoring Accessibility (Motion Sickness)**

---

## Video Tutorial

**Watch:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=4000s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=4000s)

**Additional Resources:**
- [Animate.css](https://animate.style/) - Pre-built animations
- [MDN - CSS Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations)

---

## Related Topics

**Prerequisites:**
- [Transitions](transitions.md)
- [2D Transforms](transforms-2d.md)

**Next Steps:**
- [Filters](filters.md) (if continuing visual effects)

---

## Practice Exercise

### Challenge: Create a Loading Screen with Multiple Animations

**Requirements:**
- [ ] Spinning loader icon (infinite rotation)
- [ ] Pulsing "Loading..." text
- [ ] Fade in animation on appearance
- [ ] Fade out when loading completes (`.loaded` class)

---

### Starter Code

**HTML:**
```html
<div class="loading-screen">
  <div class="spinner"></div>
  <p class="loading-text">Loading...</p>
</div>
```

**CSS (Complete this):**
```css
/* Your CSS here */
```

---

## Navigation

**Previous:** [← Transitions](transitions.md)
**Next:** [Image Styling →](../10-images-media/image-styling.md)
**Up:** [↑ Back to Visual Effects](../README.md#9️⃣-visual-effects-8-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Visual Effects
**Difficulty:** Intermediate
