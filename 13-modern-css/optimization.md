---
title: CSS Optimization
category: Modern CSS
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Optimization

> **Quick Summary:** CSS optimization improves page load speed and rendering performance. Key techniques: minification, critical CSS, reduce specificity, avoid expensive properties, use CSS containment, optimize selectors, and leverage browser caching.

## Table of Contents
- [Introduction](#introduction)
- [File Size Optimization](#file-size-optimization)
- [Critical CSS](#critical-css)
- [Selector Performance](#selector-performance)
- [Rendering Performance](#rendering-performance)
- [CSS Containment](#css-containment)
- [Avoiding Expensive Properties](#avoiding-expensive-properties)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**CSS optimization** reduces load times and improves rendering performance. This directly impacts Core Web Vitals:
- **LCP** (Largest Contentful Paint): How fast main content loads
- **FID** (First Input Delay): How fast page responds to user
- **CLS** (Cumulative Layout Shift): Visual stability

**Impact on users:**
- ✅ Faster page loads
- ✅ Better mobile experience
- ✅ Improved SEO rankings
- ✅ Lower bounce rates

---

## File Size Optimization

### Minification

**Remove whitespace, comments, and unnecessary characters.**

**Before minification:**
```css
/* Main navigation styles */
.navigation {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 40px;
  background-color: #ffffff;
}

.navigation a {
  color: #333333;
  text-decoration: none;
  font-size: 16px;
}
```

**After minification:**
```css
.navigation{display:flex;justify-content:space-between;align-items:center;padding:20px 40px;background-color:#fff}.navigation a{color:#333;text-decoration:none;font-size:16px}
```

**Tools:**
- **cssnano** (PostCSS plugin)
- **clean-css** (Node.js)
- **csso** (CSS Optimizer)
- **Build tools:** Webpack, Vite, Parcel (automatic minification)

**Savings:** 20-40% file size reduction

---

### Combine Files

```html
<!-- ❌ Bad: Multiple requests -->
<link rel="stylesheet" href="reset.css">
<link rel="stylesheet" href="typography.css">
<link rel="stylesheet" href="layout.css">
<link rel="stylesheet" href="components.css">

<!-- ✅ Good: Single request (or use HTTP/2) -->
<link rel="stylesheet" href="styles.min.css">
```

**With HTTP/2:** Multiple files are okay (parallel loading). But fewer files still better for HTTP/1.1.

---

### Remove Unused CSS

**Identify and remove CSS not used on your pages.**

**Tools:**
- **PurgeCSS:** Scans HTML, removes unused styles
- **UnCSS:** Similar to PurgeCSS
- **Chrome DevTools:** Coverage tab

**Example (PurgeCSS):**
```javascript
// purgecss.config.js
module.exports = {
  content: ['./src/**/*.html', './src/**/*.js'],
  css: ['./src/styles.css'],
  output: './dist/styles.min.css'
}
```

**Typical savings:** 50-90% for frameworks like Bootstrap, Tailwind

---

### Shorthand Properties

```css
/* ❌ Verbose (more bytes) */
.element {
  margin-top: 10px;
  margin-right: 20px;
  margin-bottom: 10px;
  margin-left: 20px;
  background-color: white;
  background-image: url('bg.png');
  background-repeat: no-repeat;
  background-position: center;
}

/* ✅ Shorthand (fewer bytes) */
.element {
  margin: 10px 20px;
  background: white url('bg.png') no-repeat center;
}
```

---

### Compress Colors

```css
/* ❌ Longer */
color: #ffffff;
background: #000000;

/* ✅ Shorter */
color: #fff;
background: #000;

/* ✅ Even shorter for common colors */
color: white; /* 5 bytes vs #fff (4 bytes) - depends on color */
```

---

## Critical CSS

**Inline CSS needed for above-the-fold content** to eliminate render-blocking.

### What is Critical CSS?

**Critical CSS** = CSS needed to render visible content on page load (before user scrolls).

**Strategy:**
1. Identify above-the-fold styles
2. Inline them in `<head>`
3. Load remaining CSS asynchronously

---

### Implementation

```html
<!DOCTYPE html>
<html>
<head>
  <!-- 1. Inline critical CSS -->
  <style>
    /* Only styles for header, hero, and visible content */
    body { margin: 0; font-family: sans-serif; }
    .header { background: #fff; padding: 20px; }
    .hero { height: 100vh; background: url('hero.jpg'); }
  </style>

  <!-- 2. Load full CSS asynchronously -->
  <link rel="preload" href="styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
  <noscript><link rel="stylesheet" href="styles.css"></noscript>
</head>
<body>
  <header class="header">...</header>
  <section class="hero">...</section>
  <section class="content">...</section>
</body>
</html>
```

**Tools:**
- **Critical** (npm package)
- **Penthouse**
- **Critters** (Webpack plugin)

---

### Automatic Critical CSS Extraction

```javascript
// critical.js (Node.js example)
const critical = require('critical');

critical.generate({
  inline: true,
  base: 'dist/',
  src: 'index.html',
  target: 'index-critical.html',
  width: 1300,
  height: 900
});
```

---

## Selector Performance

### Avoid Universal Selector

```css
/* ❌ Slow: Applies to EVERY element */
* {
  margin: 0;
  padding: 0;
}

/* ✅ Better: Target specific elements */
body, h1, h2, h3, p, ul, li {
  margin: 0;
  padding: 0;
}

/* ✅ Or use CSS reset library (once) */
```

---

### Avoid Deep Nesting

```css
/* ❌ Slow: Browser reads right-to-left */
html body div.container section.content article.post p.text span.highlight {
  color: red;
}

/* ✅ Better: Use class */
.highlight-text {
  color: red;
}
```

**Why?** Browsers match selectors right-to-left. Deep nesting = more work.

---

### Prefer Classes Over Tags

```css
/* ❌ Slower */
div p span {
  color: blue;
}

/* ✅ Faster */
.text-span {
  color: blue;
}
```

---

### Avoid Attribute Selectors with Wildcards

```css
/* ❌ Very slow */
[class*="btn"] {
  padding: 10px;
}

/* ✅ Better: Specific class */
.btn {
  padding: 10px;
}
```

---

## Rendering Performance

### Avoid Layout Thrashing

**Don't force reflow/repaint in loops.**

```javascript
// ❌ Bad: Forces reflow on each iteration
for (let i = 0; i < elements.length; i++) {
  elements[i].style.width = elements[i].offsetWidth + 10 + 'px';
  // Reading offsetWidth triggers layout calculation
}

// ✅ Good: Batch reads, then writes
const widths = elements.map(el => el.offsetWidth);
for (let i = 0; i < elements.length; i++) {
  elements[i].style.width = widths[i] + 10 + 'px';
}
```

---

### Use transform Instead of position

```css
/* ❌ Triggers layout */
.element {
  position: relative;
  left: 100px; /* Layout */
}

/* ✅ Only triggers composite (faster) */
.element {
  transform: translateX(100px); /* Composite layer */
}
```

**Performance hierarchy:**
1. **Composite:** Only GPU (fastest) - `transform`, `opacity`
2. **Paint:** Repaints pixels - `color`, `background`
3. **Layout:** Recalculates positions (slowest) - `width`, `height`, `left`, `top`

---

### Avoid Expensive Properties

**Properties that trigger layout (slow):**
- `width`, `height`
- `margin`, `padding`
- `top`, `left`, `right`, `bottom`
- `border`
- `display`
- `float`
- `position`

**Properties that only trigger composite (fast):**
- `transform`
- `opacity`

```css
/* ❌ Slow: Triggers layout */
@keyframes slideIn {
  from { left: -100px; }
  to { left: 0; }
}

/* ✅ Fast: Only composite */
@keyframes slideIn {
  from { transform: translateX(-100px); }
  to { transform: translateX(0); }
}
```

---

## CSS Containment

**Tell browser which elements are independent** (optimizes rendering).

### contain Property

```css
/* Article is self-contained */
.article {
  contain: layout style paint;
}

/* Sidebar doesn't affect main content */
.sidebar {
  contain: layout;
}

/* Widget is fully isolated */
.widget {
  contain: strict; /* layout + style + paint + size */
}
```

**Values:**
- `layout`: Element's layout doesn't affect outside
- `style`: Counters/quotes scoped to element
- `paint`: Element won't paint outside its bounds
- `size`: Element size doesn't depend on children
- `strict`: All containment types
- `content`: `layout + style + paint`

**Benefits:** Browser can skip rendering unrelated elements when this element changes.

---

### content-visibility

**Skip rendering off-screen content** (huge performance boost).

```css
.section {
  content-visibility: auto;
  contain-intrinsic-size: 1000px; /* Placeholder height */
}
```

**How it works:**
- Browser doesn't render off-screen sections
- Placeholder size prevents layout shift
- Renders when section enters viewport

**Use case:** Long pages with many sections (news sites, social feeds)

**Performance gain:** 5-10x faster initial render on long pages

---

## Avoiding Expensive Properties

### Shadows and Filters

```css
/* ⚠️ Expensive: Triggers repaint */
.card {
  box-shadow: 0 10px 30px rgba(0,0,0,0.5);
  filter: blur(5px);
}

/* ✅ Optimize: Reduce blur radius, simplify shadows */
.card {
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

/* ✅ Or use will-change hint */
.card {
  box-shadow: 0 10px 30px rgba(0,0,0,0.5);
  will-change: box-shadow;
}
```

---

### will-change Property

**Hints to browser about upcoming changes** (creates composite layer).

```css
/* ✅ Good: Element will be animated */
.animated-element {
  will-change: transform, opacity;
}

.animated-element:hover {
  transform: scale(1.1);
}

/* ❌ Bad: Too many elements */
* {
  will-change: transform; /* Wastes GPU memory */
}
```

**Best practice:** Use sparingly, only on elements that will actually change.

---

## Best Practices

### ✅ Do This

1. **Minify CSS in production**
   ```bash
   # Build step
   npm run build # Minifies automatically
   ```

2. **Use critical CSS for above-fold**
   ```html
   <style>/* Inline critical CSS */</style>
   <link rel="preload" href="styles.css" as="style">
   ```

3. **Prefer transform over position**
   ```css
   transform: translateX(100px); /* Fast */
   ```

4. **Use content-visibility for long pages**
   ```css
   .section {
     content-visibility: auto;
   }
   ```

5. **Remove unused CSS**
   ```bash
   purgecss --css styles.css --content index.html
   ```

6. **Compress and cache**
   ```nginx
   # nginx config
   gzip on;
   gzip_types text/css;
   ```

---

### ❌ Avoid This

1. **Don't use @import**
   ```css
   /* Blocks rendering */
   @import url('style.css');
   ```

2. **Don't animate layout properties**
   ```css
   /* Slow */
   @keyframes bad {
     from { width: 100px; }
     to { width: 200px; }
   }
   ```

3. **Don't overuse will-change**
   ```css
   /* Wastes GPU memory */
   * { will-change: transform; }
   ```

4. **Don't use deep selectors**
   ```css
   /* Slow */
   div div div p span { }
   ```

5. **Don't load unused frameworks**
   ```html
   <!-- Don't load full Bootstrap for 1 button -->
   <link rel="stylesheet" href="bootstrap.min.css">
   ```

---

## Measurement Tools

### Chrome DevTools

1. **Lighthouse:**
   - Open DevTools → Lighthouse tab
   - Run audit
   - Check "Performance" score

2. **Coverage:**
   - DevTools → More tools → Coverage
   - Shows unused CSS percentage

3. **Performance:**
   - DevTools → Performance tab
   - Record page load
   - Analyze rendering timeline

---

### Web Vitals

```javascript
// Measure Core Web Vitals
import {getCLS, getFID, getLCP} from 'web-vitals';

getCLS(console.log); // Cumulative Layout Shift
getFID(console.log); // First Input Delay
getLCP(console.log); // Largest Contentful Paint
```

---

### Online Tools

- **PageSpeed Insights:** https://pagespeed.web.dev/
- **WebPageTest:** https://www.webpagetest.org/
- **GTmetrix:** https://gtmetrix.com/

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `contain` | 52+ | 69+ | 15.4+ | 79+ |
| `content-visibility` | 85+ | N/A | N/A | 85+ |
| `will-change` | 36+ | 36+ | 9.1+ | 79+ |

---

## Related Topics

**Prerequisites:**
- [CSS Fundamentals](../01-fundamentals/syntax.md)
- [Transforms](../09-visual-effects/transforms-2d.md)

**Next Steps:**
- [Accessibility](accessibility.md)
- [Performance Monitoring](../README.md)

---

## Practice Exercise

Optimize a website:
1. Run Lighthouse audit (identify issues)
2. Minify CSS (use build tool)
3. Extract critical CSS (inline above-fold styles)
4. Remove unused CSS (PurgeCSS)
5. Replace layout animations with transforms
6. Run Lighthouse again (compare scores)

Target: 90+ performance score

---

## Navigation

**Previous:** [← At-Rules](at-rules.md)
**Next:** [Accessibility →](accessibility.md)
**Up:** [↑ Back to Modern CSS](../README.md#1️⃣3️⃣-modern-css-5-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Modern CSS
**Difficulty:** Advanced
