---
title: Mobile-First Design
category: Responsive Design
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Mobile-First Design

> **Quick Summary:** Mobile-first is a design philosophy where you build the mobile experience first, then progressively enhance for larger screens. Uses `min-width` media queries to add complexity as space allows. Results in simpler, more performant code.

## Table of Contents
- [Introduction](#introduction)
- [Mobile-First vs Desktop-First](#mobile-first-vs-desktop-first)
- [min-width Media Queries](#min-width-media-queries)
- [Progressive Enhancement](#progressive-enhancement)
- [Common Breakpoints](#common-breakpoints)
- [Layout Strategies](#layout-strategies)
- [Performance Benefits](#performance-benefits)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Mobile-first design** starts with the mobile experience as the baseline, then adds features for tablets and desktops. This approach is superior to desktop-first because:

✅ **Simpler:** Mobile designs are minimal (fewer features to break)
✅ **Faster:** Mobile devices load less CSS
✅ **Scalable:** Easier to add than remove
✅ **Future-proof:** Works for smartwatches, new devices

**Philosophy:** "Start small, enhance progressively."

---

## Mobile-First vs Desktop-First

### Desktop-First (Old Way)

```css
/* Start with desktop (complex) */
.container {
  display: grid;
  grid-template-columns: 250px 1fr 300px;
  gap: 30px;
  padding: 40px;
}

/* Remove complexity for mobile (harder) */
@media (max-width: 768px) {
  .container {
    grid-template-columns: 1fr;
    gap: 10px;
    padding: 10px;
  }
}
```

**Problems:**
- Mobile devices load desktop CSS first (wasted bytes)
- Harder to simplify complex layouts
- Uses `max-width` (subtractive approach)

---

### Mobile-First (Modern Way)

```css
/* Start with mobile (simple) */
.container {
  display: grid;
  grid-template-columns: 1fr;
  gap: 10px;
  padding: 10px;
}

/* Add complexity for larger screens (easier) */
@media (min-width: 768px) {
  .container {
    grid-template-columns: 250px 1fr 300px;
    gap: 30px;
    padding: 40px;
  }
}
```

**Benefits:**
- Mobile devices only load mobile CSS
- Progressive enhancement (additive approach)
- Uses `min-width` (adds features as space allows)

---

## min-width Media Queries

### Basic Pattern

```css
/* Mobile: Default (no media query) */
.element {
  font-size: 16px;
  padding: 10px;
}

/* Tablet: Add complexity */
@media (min-width: 768px) {
  .element {
    font-size: 18px;
    padding: 20px;
  }
}

/* Desktop: More complexity */
@media (min-width: 1024px) {
  .element {
    font-size: 20px;
    padding: 30px;
  }
}
```

**How it works:**
- Base styles apply to all devices
- `min-width: 768px` adds styles when viewport ≥ 768px
- Each breakpoint builds on the previous

---

### Nesting Breakpoints

```css
/* Mobile */
body {
  font-size: 14px;
  line-height: 1.5;
}

/* Small tablets */
@media (min-width: 600px) {
  body {
    font-size: 15px;
  }
}

/* Tablets */
@media (min-width: 768px) {
  body {
    font-size: 16px;
    line-height: 1.6;
  }
}

/* Desktop */
@media (min-width: 1024px) {
  body {
    font-size: 18px;
  }
}

/* Large desktop */
@media (min-width: 1440px) {
  body {
    font-size: 20px;
  }
}
```

---

## Progressive Enhancement

### Content First, Style Later

**1. Mobile: Show essential content**
```css
.sidebar {
  display: none; /* Hide sidebar on mobile */
}

.main-content {
  width: 100%;
}
```

**2. Tablet: Add sidebar**
```css
@media (min-width: 768px) {
  .sidebar {
    display: block;
  }

  .main-content {
    width: 70%;
  }
}
```

**3. Desktop: Enhance layout**
```css
@media (min-width: 1024px) {
  .container {
    display: grid;
    grid-template-columns: 250px 1fr 300px;
  }

  .sidebar {
    position: sticky;
    top: 20px;
  }
}
```

---

### Navigation Example

```css
/* Mobile: Hamburger menu */
.nav-menu {
  display: none; /* Hidden by default */
  flex-direction: column;
}

.nav-toggle {
  display: block;
}

.nav-menu.active {
  display: flex;
}

/* Tablet: Show horizontal nav */
@media (min-width: 768px) {
  .nav-menu {
    display: flex;
    flex-direction: row;
  }

  .nav-toggle {
    display: none; /* Hide hamburger */
  }
}

/* Desktop: Add dropdowns */
@media (min-width: 1024px) {
  .nav-item:hover .dropdown {
    display: block;
  }
}
```

---

## Common Breakpoints

### Standard Breakpoints

```css
/* Mobile-first breakpoints */

/* Extra small: 0-575px (default mobile) */
/* No media query needed */

/* Small: 576px+ (large phones) */
@media (min-width: 576px) {
  /* Styles */
}

/* Medium: 768px+ (tablets) */
@media (min-width: 768px) {
  /* Styles */
}

/* Large: 1024px+ (desktops) */
@media (min-width: 1024px) {
  /* Styles */
}

/* Extra large: 1440px+ (large desktops) */
@media (min-width: 1440px) {
  /* Styles */
}
```

---

### Bootstrap-Style Breakpoints

```css
/* XS: < 576px (default) */

/* SM: ≥ 576px */
@media (min-width: 576px) { }

/* MD: ≥ 768px */
@media (min-width: 768px) { }

/* LG: ≥ 992px */
@media (min-width: 992px) { }

/* XL: ≥ 1200px */
@media (min-width: 1200px) { }

/* XXL: ≥ 1400px */
@media (min-width: 1400px) { }
```

---

## Layout Strategies

### 1. Single Column → Multi-Column

```css
/* Mobile: Stack everything */
.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 15px;
}

/* Tablet: 2 columns */
@media (min-width: 768px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }
}

/* Desktop: 3-4 columns */
@media (min-width: 1024px) {
  .grid {
    grid-template-columns: repeat(4, 1fr);
    gap: 30px;
  }
}
```

---

### 2. Stacked → Sidebar Layout

```css
/* Mobile: Stack */
.page {
  display: flex;
  flex-direction: column;
}

.sidebar,
.content {
  width: 100%;
}

/* Desktop: Sidebar */
@media (min-width: 1024px) {
  .page {
    flex-direction: row;
  }

  .sidebar {
    width: 300px;
  }

  .content {
    flex: 1;
  }
}
```

---

### 3. Hidden → Visible Elements

```css
/* Mobile: Hide secondary content */
.secondary-info {
  display: none;
}

/* Tablet: Show secondary content */
@media (min-width: 768px) {
  .secondary-info {
    display: block;
  }
}
```

---

## Performance Benefits

### CSS File Size

**Desktop-first approach:**
```css
/* 100 lines of desktop CSS loaded on mobile */
.complex-desktop-layout { /* ... */ }
.desktop-navigation { /* ... */ }
.sidebar-widgets { /* ... */ }

/* Then override 50 lines for mobile */
@media (max-width: 768px) {
  .complex-desktop-layout { display: none; }
  /* ... */
}
```
→ Mobile loads 150 lines of CSS

**Mobile-first approach:**
```css
/* 30 lines of mobile CSS */
.simple-mobile { /* ... */ }

/* Desktop adds 70 lines */
@media (min-width: 768px) {
  .complex-desktop-layout { /* ... */ }
}
```
→ Mobile loads 30 lines of CSS (5x smaller)

---

### Image Loading

```css
/* Mobile: Small images */
.hero {
  background-image: url('hero-mobile.jpg'); /* 200KB */
}

/* Desktop: Large images */
@media (min-width: 1024px) {
  .hero {
    background-image: url('hero-desktop.jpg'); /* 800KB */
  }
}
```

**Savings:** Mobile users don't download 800KB desktop image.

---

## Examples

### Example 1: Responsive Card Grid

```css
/* Mobile: 1 column, minimal spacing */
.card-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 10px;
  padding: 10px;
}

.card {
  padding: 15px;
  font-size: 14px;
}

/* Tablet: 2 columns, more spacing */
@media (min-width: 768px) {
  .card-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
    padding: 20px;
  }

  .card {
    padding: 20px;
    font-size: 16px;
  }
}

/* Desktop: 3 columns, max spacing */
@media (min-width: 1024px) {
  .card-grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
    padding: 30px;
  }
}
```

---

### Example 2: Navigation Bar

```css
/* Mobile: Vertical menu, hidden by default */
.nav {
  position: fixed;
  top: 0;
  left: -100%;
  width: 80%;
  height: 100vh;
  background: white;
  transition: left 0.3s;
  flex-direction: column;
  padding: 60px 20px 20px;
}

.nav.active {
  left: 0;
}

.nav-toggle {
  display: block;
  position: fixed;
  top: 20px;
  right: 20px;
  z-index: 100;
}

/* Tablet: Horizontal menu, always visible */
@media (min-width: 768px) {
  .nav {
    position: static;
    width: auto;
    height: auto;
    left: 0;
    flex-direction: row;
    padding: 0;
    gap: 20px;
  }

  .nav-toggle {
    display: none;
  }
}

/* Desktop: Add hover effects */
@media (min-width: 1024px) {
  .nav-link {
    position: relative;
  }

  .nav-link::after {
    content: '';
    position: absolute;
    bottom: -5px;
    left: 0;
    width: 0;
    height: 2px;
    background: #007bff;
    transition: width 0.3s;
  }

  .nav-link:hover::after {
    width: 100%;
  }
}
```

---

### Example 3: Typography Scaling

```css
/* Mobile: Compact text */
body {
  font-size: 14px;
  line-height: 1.5;
}

h1 { font-size: 24px; }
h2 { font-size: 20px; }
h3 { font-size: 18px; }

p {
  margin-bottom: 15px;
}

/* Tablet: Slightly larger */
@media (min-width: 768px) {
  body {
    font-size: 16px;
    line-height: 1.6;
  }

  h1 { font-size: 32px; }
  h2 { font-size: 24px; }
  h3 { font-size: 20px; }
}

/* Desktop: Full-size text */
@media (min-width: 1024px) {
  body {
    font-size: 18px;
    line-height: 1.7;
  }

  h1 { font-size: 48px; }
  h2 { font-size: 36px; }
  h3 { font-size: 24px; }

  p {
    margin-bottom: 20px;
  }
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `min-width` media queries | All | All | All | All |
| Mobile-first approach | All | All | All | All |

**Support:** Universal (100%).

---

## Best Practices

### ✅ Do This

1. **Start with mobile styles (no media query)**
   ```css
   .element {
     /* Mobile styles */
   }

   @media (min-width: 768px) {
     /* Tablet styles */
   }
   ```

2. **Use min-width, not max-width**
   ```css
   /* Good: Progressive enhancement */
   @media (min-width: 768px) { }

   /* Bad: Desktop-first */
   @media (max-width: 768px) { }
   ```

3. **Keep breakpoints consistent**
   ```css
   /* Define once, reuse everywhere */
   @media (min-width: 768px) { }
   @media (min-width: 1024px) { }
   ```

4. **Test on real devices**
   - Chrome DevTools is good, but not perfect
   - Test on iPhone, Android, iPad

---

### ❌ Avoid This

1. **Don't mix mobile-first and desktop-first**
   ```css
   /* Confusing: Mixed approaches */
   @media (min-width: 768px) { }
   @media (max-width: 1024px) { }
   ```

2. **Don't start with desktop**
   ```css
   /* Bad: Desktop-first */
   .element { width: 1200px; }

   @media (max-width: 768px) {
     .element { width: 100%; }
   }
   ```

3. **Don't hide important content on mobile**
   ```css
   /* Bad: Hiding key info */
   .important-feature {
     display: none; /* Mobile users miss this */
   }
   ```

4. **Don't use too many breakpoints**
   ```css
   /* Overkill: Too granular */
   @media (min-width: 320px) { }
   @media (min-width: 480px) { }
   @media (min-width: 600px) { }
   @media (min-width: 768px) { }
   /* ... 10 more breakpoints ... */
   ```

---

## Related Topics

**Prerequisites:**
- [Viewport Meta Tag](viewport.md)
- [Media Queries](media-queries.md)

**Next Steps:**
- [Responsive Grid](responsive-grid.md)
- [Responsive Typography](../01-fundamentals/typography-intro.md)

---

## Practice Exercise

Convert a desktop-first layout to mobile-first:
- Start with single-column mobile layout
- Add 2-column tablet layout at 768px
- Add 3-column desktop layout at 1024px
- Use `min-width` media queries only
- Test responsiveness at each breakpoint

---

## Navigation

**Previous:** [← Responsive Videos](responsive-videos.md)
**Next:** [Modern CSS →](../13-modern-css/css-functions.md)
**Up:** [↑ Back to Responsive Design](../README.md#1️⃣2️⃣-responsive-design-5-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Responsive Design
**Difficulty:** Intermediate
