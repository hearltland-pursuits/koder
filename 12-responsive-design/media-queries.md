---
title: CSS Media Queries
category: Responsive Design
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Media Queries

> **Quick Summary:** Media queries let you apply different CSS styles based on device characteristics like screen width, height, orientation, and resolution. They're the foundation of responsive design, enabling websites to adapt seamlessly from mobile phones to desktop monitors.

## Table of Contents
- [Introduction](#introduction)
- [Why Media Queries Matter](#why-media-queries-matter)
- [Basic Syntax](#basic-syntax)
- [Common Breakpoints](#common-breakpoints)
- [Media Features](#media-features)
- [Mobile-First vs Desktop-First](#mobile-first-vs-desktop-first)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

The web is accessed on thousands of different devices: iPhones, Android tablets, laptops, desktop monitors, TVs, smartwatches. Screen sizes range from 2 inches to 50+ inches. A layout perfect for a 27-inch monitor is unusable on a 4-inch phone. Enter **media queries**—CSS's solution to device diversity.

Media queries are conditional CSS rules that apply only when certain conditions are met. "If the screen is smaller than 768px, stack these columns vertically." "If the device is in landscape mode, show a horizontal menu." "If the screen has high pixel density (Retina), use high-resolution images." Without media queries, you'd need separate websites for mobile, tablet, and desktop. With them, one codebase adapts to all devices.

Modern responsive design is built on three pillars: **fluid layouts** (using percentages/flexbox/grid), **flexible images** (max-width: 100%), and **media queries** (adaptive styling). Media queries are the intelligence layer—they detect the environment and activate appropriate styles. Master them, and your sites work beautifully everywhere.

**Key Concept:** Media queries don't change HTML content—they change CSS styles based on device characteristics. Same HTML, different presentation.

---

## Why Media Queries Matter

### 1. **Mobile Traffic Dominates**
- **59% of global web traffic** is mobile (2024)
- **53% of users** abandon sites that take >3 seconds to load on mobile
- **Google prioritizes** mobile-friendly sites in search rankings (Mobile-First Indexing)

**Without media queries:** Users pinch, zoom, scroll horizontally—then leave.
**With media queries:** Content adapts automatically—users stay.

### 2. **One Codebase, All Devices**

**Old approach (pre-2010):**
- `www.site.com` → Desktop site
- `m.site.com` → Separate mobile site
- Twice the development, twice the maintenance

**Modern approach:**
- `www.site.com` → Responsive site (adapts to all devices)
- Media queries handle styling differences
- One codebase, easier maintenance

### 3. **Improved User Experience**
Media queries enable device-appropriate layouts:
- **Mobile:** Single column, larger tap targets, simplified navigation
- **Tablet:** Two columns, moderate density
- **Desktop:** Multi-column, compact density, hover effects

### 4. **Career Relevance**
Responsive design is non-negotiable:
- **100% of front-end jobs** require responsive skills
- **Interview question:** "How do you make a site responsive?" → Media queries
- **Portfolio requirement:** All projects must be mobile-friendly

---

## Basic Syntax

### Structure

```css
@media media-type and (media-feature) {
  /* CSS rules that apply when condition is true */
}
```

### Example

```css
/* Default styles (mobile-first) */
body {
  font-size: 16px;
}

/* Tablet and larger */
@media (min-width: 768px) {
  body {
    font-size: 18px;
  }
}

/* Desktop and larger */
@media (min-width: 1024px) {
  body {
    font-size: 20px;
  }
}
```

---

## Media Types

| Type | Description | Use Case |
|------|-------------|----------|
| `screen` | Computer screens, tablets, phones | **Most common** |
| `print` | Print preview and printed pages | Print stylesheets |
| `all` | All devices | Default (can be omitted) |

**Examples:**

```css
/* Screen only */
@media screen and (max-width: 600px) {
  /* Mobile screen styles */
}

/* Print only */
@media print {
  /* Hide navigation when printing */
  .nav { display: none; }
}

/* All devices (screen, print, etc.) */
@media all and (min-width: 1024px) {
  /* Desktop styles */
}
```

**Note:** `screen` is default for most responsive design. You can usually omit it:

```css
/* These are equivalent */
@media screen and (max-width: 768px) { }
@media (max-width: 768px) { }
```

---

## Common Breakpoints

**Standard responsive breakpoints:**

| Device | Breakpoint | Media Query |
|--------|------------|-------------|
| **Mobile** (portrait) | < 576px | Default styles |
| **Mobile** (landscape) / **Small tablet** | ≥ 576px | `@media (min-width: 576px)` |
| **Tablet** | ≥ 768px | `@media (min-width: 768px)` |
| **Desktop** | ≥ 1024px | `@media (min-width: 1024px)` |
| **Large desktop** | ≥ 1200px | `@media (min-width: 1200px)` |
| **Extra large** | ≥ 1440px | `@media (min-width: 1440px)` |

**Bootstrap's breakpoints:**
```css
/* Extra small (default) */
/* Small */
@media (min-width: 576px) { }
/* Medium */
@media (min-width: 768px) { }
/* Large */
@media (min-width: 992px) { }
/* Extra large */
@media (min-width: 1200px) { }
/* Extra extra large */
@media (min-width: 1400px) { }
```

**Important:** These are conventions, not rules. Choose breakpoints based on your design.

---

## Media Features

### 1. Width-Based

**`min-width`** (Mobile-first approach)
```css
/* Styles apply at 768px and wider */
@media (min-width: 768px) {
  .container { max-width: 750px; }
}
```

**`max-width`** (Desktop-first approach)
```css
/* Styles apply below 768px */
@media (max-width: 767px) {
  .sidebar { display: none; }
}
```

**Range syntax (modern):**
```css
/* Between 768px and 1024px */
@media (min-width: 768px) and (max-width: 1024px) {
  /* Tablet-only styles */
}

/* Modern syntax (cleaner) */
@media (768px <= width <= 1024px) {
  /* Same as above */
}
```

---

### 2. Height-Based

```css
/* Short viewports (landscape phones) */
@media (max-height: 600px) {
  .header { height: 40px; } /* Shorter header */
}

/* Tall viewports */
@media (min-height: 800px) {
  .hero { height: 100vh; } /* Full-screen hero */
}
```

---

### 3. Orientation

```css
/* Portrait (tall) */
@media (orientation: portrait) {
  .menu { flex-direction: column; }
}

/* Landscape (wide) */
@media (orientation: landscape) {
  .menu { flex-direction: row; }
}
```

---

### 4. Resolution (Retina/High-DPI)

```css
/* Standard resolution */
.logo {
  background-image: url('logo.png');
}

/* High resolution (Retina, 2x) */
@media (min-resolution: 2dppx) {
  .logo {
    background-image: url('logo@2x.png');
  }
}
```

---

### 5. Aspect Ratio

```css
/* Widescreen (16:9) */
@media (min-aspect-ratio: 16/9) {
  .video-container { max-width: 1600px; }
}
```

---

### 6. Hover Capability

```css
/* Devices with hover (desktop) */
@media (hover: hover) {
  .button:hover {
    background-color: blue;
  }
}

/* Devices without hover (touch) */
@media (hover: none) {
  .button:active {
    background-color: blue;
  }
}
```

---

### 7. Pointer Accuracy

```css
/* Fine pointer (mouse) */
@media (pointer: fine) {
  .button { padding: 8px 16px; } /* Smaller */
}

/* Coarse pointer (finger) */
@media (pointer: coarse) {
  .button { padding: 16px 24px; } /* Larger tap target */
}
```

---

### 8. Prefers Color Scheme (Dark Mode)

```css
/* Light mode (default) */
body {
  background-color: white;
  color: black;
}

/* Dark mode */
@media (prefers-color-scheme: dark) {
  body {
    background-color: #1a1a1a;
    color: #e0e0e0;
  }
}
```

---

## Combining Media Features

Use `and`, `or` (`,`), and `not` to combine conditions.

### AND (All conditions must be true)

```css
/* Tablet in landscape */
@media (min-width: 768px) and (max-width: 1024px) and (orientation: landscape) {
  /* Tablet landscape styles */
}
```

### OR (Any condition can be true)

```css
/* Small screens OR portrait orientation */
@media (max-width: 600px), (orientation: portrait) {
  /* Mobile or portrait styles */
}
```

### NOT (Inverse condition)

```css
/* Not print */
@media not print {
  /* Screen styles */
}
```

---

## Mobile-First vs Desktop-First

### Mobile-First (Recommended)

**Start with mobile styles, add complexity for larger screens.**

```css
/* Mobile (default) */
.container {
  width: 100%;
  padding: 10px;
}

/* Tablet and up */
@media (min-width: 768px) {
  .container {
    max-width: 750px;
    margin: 0 auto;
    padding: 20px;
  }
}

/* Desktop and up */
@media (min-width: 1024px) {
  .container {
    max-width: 1000px;
    padding: 30px;
  }
}
```

**Benefits:**
- Mobile traffic is majority—prioritize it
- Easier to add features than remove them
- Faster mobile load (less CSS to override)
- Aligns with Google's Mobile-First Indexing

---

### Desktop-First

**Start with desktop styles, simplify for smaller screens.**

```css
/* Desktop (default) */
.container {
  max-width: 1000px;
  margin: 0 auto;
  padding: 30px;
}

/* Tablet and smaller */
@media (max-width: 1023px) {
  .container {
    max-width: 750px;
    padding: 20px;
  }
}

/* Mobile and smaller */
@media (max-width: 767px) {
  .container {
    width: 100%;
    padding: 10px;
  }
}
```

**Use when:**
- Legacy codebases
- Desktop-focused applications (dashboards, admin panels)

---

## Examples

### Example 1: Responsive Navigation

```html
<nav class="navbar">
  <div class="logo">Logo</div>
  <button class="menu-toggle">Menu</button>
  <ul class="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Services</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

```css
/* Mobile (default) */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background-color: #2c3e50;
}

.menu-toggle {
  display: block; /* Show hamburger on mobile */
  background: none;
  border: none;
  color: white;
  font-size: 24px;
}

.nav-links {
  display: none; /* Hide links on mobile */
  flex-direction: column;
  position: absolute;
  top: 60px;
  left: 0;
  width: 100%;
  background-color: #34495e;
}

.nav-links.active {
  display: flex; /* Show when hamburger clicked */
}

/* Tablet and up (768px+) */
@media (min-width: 768px) {
  .menu-toggle {
    display: none; /* Hide hamburger on desktop */
  }

  .nav-links {
    display: flex; /* Always show links */
    flex-direction: row;
    position: static;
    width: auto;
    background: none;
    gap: 2rem;
  }
}
```

---

### Example 2: Responsive Grid

```html
<div class="grid">
  <div class="card">Card 1</div>
  <div class="card">Card 2</div>
  <div class="card">Card 3</div>
  <div class="card">Card 4</div>
</div>
```

```css
/* Mobile (1 column) */
.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
  padding: 20px;
}

/* Tablet (2 columns) */
@media (min-width: 768px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Desktop (4 columns) */
@media (min-width: 1024px) {
  .grid {
    grid-template-columns: repeat(4, 1fr);
  }
}
```

---

### Example 3: Dark Mode

```css
/* Light mode (default) */
:root {
  --bg-color: #ffffff;
  --text-color: #333333;
  --card-bg: #f5f5f5;
}

body {
  background-color: var(--bg-color);
  color: var(--text-color);
}

.card {
  background-color: var(--card-bg);
}

/* Dark mode */
@media (prefers-color-scheme: dark) {
  :root {
    --bg-color: #1a1a1a;
    --text-color: #e0e0e0;
    --card-bg: #2a2a2a;
  }
}
```

---

## Common Use Cases

### Use Case 1: Hide/Show Content

```css
/* Hide on mobile */
.desktop-only {
  display: none;
}

@media (min-width: 1024px) {
  .desktop-only {
    display: block;
  }
}

/* Show only on mobile */
.mobile-only {
  display: block;
}

@media (min-width: 1024px) {
  .mobile-only {
    display: none;
  }
}
```

---

### Use Case 2: Font Scaling

```css
/* Mobile */
body { font-size: 14px; }
h1 { font-size: 28px; }

/* Tablet */
@media (min-width: 768px) {
  body { font-size: 16px; }
  h1 { font-size: 36px; }
}

/* Desktop */
@media (min-width: 1024px) {
  body { font-size: 18px; }
  h1 { font-size: 48px; }
}
```

---

### Use Case 3: Container Width

```css
.container {
  width: 100%;
  padding: 0 15px;
}

@media (min-width: 768px) {
  .container { max-width: 750px; margin: 0 auto; }
}

@media (min-width: 1024px) {
  .container { max-width: 1000px; }
}

@media (min-width: 1200px) {
  .container { max-width: 1140px; }
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|----|
| Basic Media Queries | 4+ | 3.5+ | 4+ | 12+ | 9+ |
| `min-width/max-width` | 4+ | 3.5+ | 4+ | 12+ | 9+ |
| `orientation` | 4+ | 3.5+ | 5+ | 12+ | 9+ |
| `prefers-color-scheme` | 76+ | 67+ | 12.1+ | 79+ | |
| `hover`/`pointer` | 41+ | 64+ | 9+ | 12+ | |

**Key Takeaway:** Basic media queries work everywhere. Modern features (dark mode, hover) have excellent support except IE.

---

## Best Practices

### Do This

1. **Use Mobile-First Approach**
   ```css
   /* Mobile default */
   .element { width: 100%; }

   /* Desktop enhancement */
   @media (min-width: 1024px) {
     .element { width: 50%; }
   }
   ```

2. **Choose Breakpoints Based on Content, Not Devices**
   ```css
   /* When design breaks, add breakpoint */
   @media (min-width: 640px) { /* Content needs two columns here */ }
   ```

3. **Use `em` or `rem` for Breakpoints (Respects User Zoom)**
   ```css
   /* Good - respects user font size */
   @media (min-width: 48em) { /* 768px at 16px base */ }

   /* Avoid - ignores user preferences */
   @media (min-width: 768px) { }
   ```

4. **Test on Real Devices**
   - Browser DevTools are approximations
   - Test on actual phones/tablets when possible

---

### Avoid This

1. **Don't Target Specific Devices**
   ```css
   /* Bad - devices change */
   @media (width: 375px) and (height: 812px) { /* iPhone X specific */ }

   /* Good - flexible */
   @media (min-width: 375px) { }
   ```

2. **Don't Overuse Breakpoints**
   ```css
   /* Bad - too many */
   @media (min-width: 375px) { }
   @media (min-width: 414px) { }
   @media (min-width: 768px) { }
   @media (min-width: 800px) { }

   /* Good - strategic */
   @media (min-width: 576px) { }
   @media (min-width: 1024px) { }
   ```

---

## Video Tutorial

**Watch Media Queries:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=10800s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=10800s)

**Timestamps:**
- `3:00:00` - Introduction to responsive design
- `3:08:00` - Media query syntax
- `3:18:00` - Common breakpoints
- `3:28:00` - Mobile-first approach
- `3:38:00` - Advanced media features

**Resources:**
- [W3Schools - Media Queries](https://www.w3schools.com/css/css3_mediaqueries.asp)
- [MDN - Media Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries)

---

## Related Topics

**Prerequisites:**
- [CSS Introduction](../01-fundamentals/introduction.md)

**Related:**
- [Viewport](viewport.md)
- [Responsive Grid](responsive-grid.md)
- [Flexbox](../06-flexbox/flexbox-intro.md)
- [CSS Grid](../07-grid/grid-intro.md)

---

## Practice Exercise

### Challenge: Build a Responsive Card Layout

**Requirements:**
- [ ] 1 column on mobile
- [ ] 2 columns on tablet (768px+)
- [ ] 3 columns on desktop (1024px+)
- [ ] Hide sidebar on mobile, show on desktop
- [ ] Larger font sizes on desktop

<details>
<summary>Click to reveal solution</summary>

**CSS:**
```css
/* Mobile (default) */
.container {
  padding: 20px;
}

.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
}

.sidebar {
  display: none; /* Hidden on mobile */
}

body {
  font-size: 14px;
}

/* Tablet (768px+) */
@media (min-width: 768px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }

  body {
    font-size: 16px;
  }
}

/* Desktop (1024px+) */
@media (min-width: 1024px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }

  .sidebar {
    display: block; /* Show on desktop */
  }

  body {
    font-size: 18px;
  }
}
```

</details>

---

**Last Updated:** November 15, 2025
**Category:** Responsive Design
**Difficulty:** Intermediate
