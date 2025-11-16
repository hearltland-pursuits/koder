---
title: Google Fonts
category: Typography
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Google Fonts

> **Quick Summary:** Google Fonts is a free library of 1400+ web fonts. Include fonts via `<link>` or `@import`, then use in CSS with `font-family`. Optimize by selecting only needed weights and using `display=swap` for faster loading.

## Table of Contents
- [Introduction](#introduction)
- [How to Use Google Fonts](#how-to-use-google-fonts)
- [Import Methods](#import-methods)
- [Font Selection](#font-selection)
- [Performance Optimization](#performance-optimization)
- [Variable Fonts](#variable-fonts)
- [Examples](#examples)
- [Best Practices](#best-practices)

---

## Introduction

**Google Fonts:** Free, open-source web fonts hosted by Google.

**Benefits:**
- ✅ 1400+ professional fonts
- ✅ Free forever
- ✅ Fast CDN delivery
- ✅ Auto-optimized for web
- ✅ No account/API key needed

**Website:** https://fonts.google.com/

---

## How to Use Google Fonts

### Step 1: Browse and Select

Visit https://fonts.google.com/ and select fonts:
1. Click on a font (e.g., "Roboto")
2. Click "+ Select this style" for each weight you need
3. Click "View selected families" (top-right icon)

### Step 2: Get the Code

Google provides two options:
1. **HTML `<link>`** (recommended)
2. **CSS `@import`** (slightly slower)

### Step 3: Use in CSS

```css
body {
  font-family: 'Roboto', sans-serif;
}
```

---

## Import Methods

### Method 1: HTML Link (Recommended)

**In your HTML `<head>`:**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
```

**Then in CSS:**
```css
body {
  font-family: 'Roboto', sans-serif;
}
```

**Benefits:**
- Faster (parallel download)
- Better caching
- Recommended by Google

### Method 2: CSS @import

**In your CSS file:**
```css
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap');

body {
  font-family: 'Roboto', sans-serif;
}
```

**Drawback:** Blocks CSS parsing until font loads (slower)

---

## Font Selection

### Selecting Font Weights

**Available weights:**
- 100 - Thin
- 200 - Extra Light
- 300 - Light
- 400 - Regular (normal)
- 500 - Medium
- 600 - Semi Bold
- 700 - Bold
- 800 - Extra Bold
- 900 - Black

**Example URL with multiple weights:**
```html
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
```

This loads:
- 300 (Light)
- 400 (Regular)
- 700 (Bold)

### Selecting Italic Styles

**Include italic weights:**
```html
<link href="https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,700;1,400;1,700&display=swap" rel="stylesheet">
```

This loads:
- Normal 400, Normal 700
- Italic 400, Italic 700

### Multiple Font Families

**Load multiple fonts:**
```html
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&family=Open+Sans:wght@300;600&display=swap" rel="stylesheet">
```

**Use in CSS:**
```css
h1, h2, h3 {
  font-family: 'Roboto', sans-serif;
}

body {
  font-family: 'Open Sans', sans-serif;
}
```

---

## Performance Optimization

### 1. Limit Font Weights

**❌ Bad - loads 9 weights (slow):**
```html
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@100;200;300;400;500;600;700;800;900&display=swap">
```

**✅ Good - loads 2-3 weights only:**
```html
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap">
```

### 2. Use font-display: swap

**Already included in Google Fonts URLs:**
```
&display=swap
```

**What it does:**
- Shows fallback font immediately
- Swaps to custom font when loaded
- Prevents invisible text (FOIT)

### 3. Preconnect to Google Fonts

**Add before font link:**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

**Benefit:** Establishes connection earlier (faster loading)

### 4. Self-Host for Maximum Performance

**Download fonts and host yourself:**
1. Download from https://google-webfonts-helper.herokuapp.com/
2. Include in project
3. Use `@font-face` (see example below)

**Benefit:** One less external request

---

## Variable Fonts

**Variable fonts:** One file contains multiple weights/styles

**Example:**
```html
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@100..900&display=swap" rel="stylesheet">
```

**Use any weight from 100-900:**
```css
.light { font-weight: 350; }
.medium { font-weight: 550; }
.bold { font-weight: 750; }
```

**Benefits:**
- Smaller file size
- Infinite weight variations
- Better performance

---

## Examples

### Example 1: Basic Implementation

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">

  <style>
    body {
      font-family: 'Roboto', sans-serif;
      font-weight: 400;
    }

    h1 {
      font-weight: 700;
    }
  </style>
</head>
<body>
  <h1>This uses Roboto Bold (700)</h1>
  <p>This uses Roboto Regular (400)</p>
</body>
</html>
```

---

### Example 2: Heading + Body Font Pairing

```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Lato:wght@400;700&display=swap" rel="stylesheet">
```

```css
h1, h2, h3, h4, h5, h6 {
  font-family: 'Playfair Display', serif; /* Elegant headings */
  font-weight: 700;
}

body {
  font-family: 'Lato', sans-serif; /* Clean body text */
  font-weight: 400;
  line-height: 1.6;
}

strong {
  font-weight: 700; /* Lato Bold */
}
```

---

### Example 3: Self-Hosted Google Font

**Download from https://google-webfonts-helper.herokuapp.com/**

**Include in CSS:**
```css
@font-face {
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 400;
  src: url('../fonts/roboto-v30-latin-regular.woff2') format('woff2'),
       url('../fonts/roboto-v30-latin-regular.woff') format('woff');
}

@font-face {
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 700;
  src: url('../fonts/roboto-v30-latin-700.woff2') format('woff2'),
       url('../fonts/roboto-v30-latin-700.woff') format('woff');
}

body {
  font-family: 'Roboto', sans-serif;
}
```

---

### Example 4: Fallback Fonts

```css
body {
  font-family: 'Roboto', 'Helvetica Neue', Arial, sans-serif;
}

/* If Roboto fails:
   1. Try Helvetica Neue
   2. Try Arial
   3. Use system sans-serif
*/
```

---

## Best Practices

### ✅ Do This

**1. Limit to 2-3 font weights**
```html
<!-- Good - only what you need -->
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap">
```

**2. Always include display=swap**
```html
&display=swap <!-- Prevents invisible text -->
```

**3. Add preconnect links**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

**4. Include fallback fonts**
```css
body {
  font-family: 'Roboto', Arial, sans-serif;
}
```

**5. Choose accessible font pairings**
```css
/* Serif headings + Sans-serif body */
h1 { font-family: 'Playfair Display', serif; }
body { font-family: 'Lato', sans-serif; }
```

### ❌ Avoid This

**1. Don't load too many weights**
```html
<!-- Bad - loads 6 weights (slow!) -->
<link href="...?family=Roboto:wght@100;300;400;500;700;900">
```

**2. Don't load too many fonts**
```html
<!-- Bad - 5 different fonts = slow -->
<link href="...?family=Roboto&family=Lato&family=Montserrat&family=Poppins&family=Raleway">
```

**3. Don't use @import in CSS**
```css
/* Slower - blocks rendering */
@import url('https://fonts.googleapis.com/...');
```

**4. Don't forget fallbacks**
```css
/* Bad - breaks if Google Fonts down */
body { font-family: 'Roboto'; }

/* Good - has fallbacks */
body { font-family: 'Roboto', Arial, sans-serif; }
```

---

## Popular Font Pairings

### Serif + Sans-Serif

```css
/* Classic elegant pairing */
h1 { font-family: 'Playfair Display', serif; }
body { font-family: 'Lato', sans-serif; }
```

### Modern Minimalist

```css
/* Clean and modern */
h1 { font-family: 'Montserrat', sans-serif; }
body { font-family: 'Open Sans', sans-serif; }
```

### Geometric

```css
/* Tech/startup vibe */
h1 { font-family: 'Poppins', sans-serif; }
body { font-family: 'Inter', sans-serif; }
```

### Monospace Accent

```css
/* Developer/tech documentation */
h1 { font-family: 'Roboto', sans-serif; }
code { font-family: 'Roboto Mono', monospace; }
```

---

## Browser Support

**Universal support** - Google Fonts work in all modern browsers (IE9+).

---

**Last Updated:** November 15, 2025
**Category:** Typography
**Difficulty:** Beginner

**Related Topics:**
- [Fonts](fonts.md) - Font properties
- [Text Styling](text-styling.md) - Text formatting
- [Web Performance](../13-modern-css/optimization.md) - Performance optimization
