---
title: Viewport Meta Tag
category: Responsive Design
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Viewport Meta Tag

> **Quick Summary:** The viewport meta tag controls how mobile browsers render web pages. Essential for responsive design. Without it, mobile devices display desktop layouts at small sizes. Always include: `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.

## Table of Contents
- [Introduction](#introduction)
- [Basic Viewport Tag](#basic-viewport-tag)
- [Viewport Properties](#viewport-properties)
- [Common Configurations](#common-configurations)
- [Mobile Browser Behavior](#mobile-browser-behavior)
- [Viewport Units](#viewport-units)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**The viewport** is the visible area of a web page on a device. Without the viewport meta tag, mobile browsers render pages at desktop widths (typically 980px) and scale them down, making text unreadable.

**Problem without viewport tag:**
```
Mobile device (375px actual width)
→ Browser renders at 980px
→ Scales down to fit 375px
→ Text becomes tiny and unreadable
```

**Solution with viewport tag:**
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Result:**
```
Mobile device (375px actual width)
→ Browser renders at 375px
→ Text remains readable
→ Media queries work correctly
```

---

## Basic Viewport Tag

### Standard Configuration

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Page</title>
</head>
<body>
  <!-- Content -->
</body>
</html>
```

**This tag should be in EVERY HTML file.**

---

## Viewport Properties

### width

**Controls viewport width.**

```html
<!-- Use device width (responsive) -->
<meta name="viewport" content="width=device-width">

<!-- Fixed width (not recommended) -->
<meta name="viewport" content="width=600">
```

**Values:**
- `device-width`: Use actual device width (e.g., 375px on iPhone)
- Number: Fixed pixel width (avoid this)

---

### initial-scale

**Sets initial zoom level.**

```html
<!-- Start at 100% zoom -->
<meta name="viewport" content="initial-scale=1.0">

<!-- Start zoomed in 150% (avoid) -->
<meta name="viewport" content="initial-scale=1.5">

<!-- Start zoomed out 50% (avoid) -->
<meta name="viewport" content="initial-scale=0.5">
```

**Best practice:** Always use `1.0` (100% zoom).

---

### minimum-scale and maximum-scale

**Controls zoom limits.**

```html
<!-- Allow zoom from 50% to 300% -->
<meta name="viewport" content="minimum-scale=0.5, maximum-scale=3.0">

<!-- Prevent zooming (DO NOT DO THIS) -->
<meta name="viewport" content="minimum-scale=1.0, maximum-scale=1.0">
```

**⚠️ Accessibility Warning:** DO NOT disable zooming. Users with visual impairments need zoom.

---

### user-scalable

**Controls whether users can zoom.**

```html
<!-- Allow zooming (default) -->
<meta name="viewport" content="user-scalable=yes">

<!-- Disable zooming (NEVER DO THIS) -->
<meta name="viewport" content="user-scalable=no">
```

**⚠️ WCAG Violation:** Disabling zoom violates accessibility guidelines.

---

## Common Configurations

### 1. Standard Responsive (Recommended)

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Use case:** 99% of websites.

---

### 2. Allow Zoom with Limits

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=0.5, maximum-scale=3.0">
```

**Use case:** When you want to limit extreme zooming (still accessible).

---

### 3. Legacy Mobile-Only Site

```html
<meta name="viewport" content="width=320">
```

**Use case:** Old mobile-only sites (deprecated approach).

---

## Mobile Browser Behavior

### Without Viewport Tag

```
Desktop site on mobile:
┌─────────────────────────────────────────┐ 980px wide
│ [Header spanning full width]            │
│                                          │
│ [Content in multiple columns]           │
│                                          │
│ [Footer]                                 │
└─────────────────────────────────────────┘
       ↓ Shrunk to fit 375px screen
┌──────┐
│ Tiny │ ← Unreadable text
│ Text │
└──────┘
```

### With Viewport Tag

```
Responsive site on mobile:
┌──────────┐ 375px wide
│ [Header] │
│          │
│ [Content]│ ← Readable
│ (Single  │
│  column) │
│          │
│ [Footer] │
└──────────┘
```

---

## Viewport Units

**CSS units based on viewport size.**

### vw (Viewport Width)

```css
/* 1vw = 1% of viewport width */
.hero {
  width: 100vw; /* Full viewport width */
  font-size: 5vw; /* 5% of viewport width */
}
```

**Example:**
- On 375px mobile: `5vw = 18.75px`
- On 1920px desktop: `5vw = 96px`

---

### vh (Viewport Height)

```css
/* 1vh = 1% of viewport height */
.full-screen {
  height: 100vh; /* Full viewport height */
}

.half-screen {
  min-height: 50vh; /* At least half screen height */
}
```

---

### vmin and vmax

```css
/* vmin: Smaller of vw or vh */
.square {
  width: 50vmin;
  height: 50vmin; /* Always square */
}

/* vmax: Larger of vw or vh */
.responsive-text {
  font-size: 3vmax;
}
```

**Use case:**
- `vmin`: Ensuring elements fit on ANY orientation
- `vmax`: Responsive typography

---

### svh, lvh, dvh (New in 2023)

```css
/* Small viewport height (mobile with UI visible) */
.section {
  height: 100svh;
}

/* Large viewport height (mobile with UI hidden) */
.fullscreen {
  height: 100lvh;
}

/* Dynamic viewport height (changes as UI shows/hides) */
.adaptive {
  height: 100dvh;
}
```

**Mobile address bar problem:**
- `100vh` includes address bar area (content gets cut off)
- `100svh` accounts for visible area only
- `100dvh` adjusts dynamically as address bar appears/disappears

---

## Best Practices

### ✅ Do This

1. **Always include viewport tag**
   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   ```

2. **Use device-width**
   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   ```

3. **Allow zooming (accessibility)**
   ```html
   <!-- No user-scalable=no -->
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   ```

4. **Use viewport units for full-screen sections**
   ```css
   .hero {
     height: 100vh;
     width: 100vw;
   }
   ```

5. **Test on real devices**
   - Chrome DevTools device mode is good, but not perfect
   - Test on actual iPhones, Androids, tablets

---

### ❌ Avoid This

1. **Don't disable zooming**
   ```html
   <!-- NEVER DO THIS -->
   <meta name="viewport" content="user-scalable=no, maximum-scale=1.0">
   ```

2. **Don't use fixed widths**
   ```html
   <!-- Bad: Forces desktop width on mobile -->
   <meta name="viewport" content="width=1024">
   ```

3. **Don't set initial-scale > 1.0**
   ```html
   <!-- Bad: Page starts zoomed in -->
   <meta name="viewport" content="initial-scale=2.0">
   ```

4. **Don't forget the tag**
   ```html
   <!-- Missing viewport tag = broken mobile experience -->
   ```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| Viewport meta tag | All | All | All | All |
| `vw`, `vh` | 26+ | 19+ | 6.1+ | 12+ |
| `vmin`, `vmax` | 26+ | 19+ | 6.1+ | 12+ |
| `svh`, `lvh`, `dvh` | 108+ | 101+ | 15.4+ | 108+ |

**Support:** Viewport tag is universal (100%). Viewport units have excellent support (95%+).

---

## Related Topics

**Prerequisites:**
- [Responsive Design Intro](rwd-intro.md)

**Next Steps:**
- [Media Queries](media-queries.md)
- [Mobile-First Design](mobile-first.md)

**Related:**
- [Responsive Grid](responsive-grid.md)
- [Responsive Typography](../01-fundamentals/typography-intro.md)

---

## Practice Exercise

Create a full-screen hero section:
- Uses 100vh height
- Uses 100vw width
- Centers content vertically and horizontally
- Includes viewport meta tag in HTML
- Test on mobile device simulator

---

## Navigation

**Previous:** [← Responsive Design Intro](rwd-intro.md)
**Next:** [Media Queries →](media-queries.md)
**Up:** [↑ Back to Responsive Design](../README.md#1️⃣2️⃣-responsive-design-5-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Responsive Design
**Difficulty:** Beginner
