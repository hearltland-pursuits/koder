---
title: CSS Fonts
category: Typography
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Fonts

> **Quick Summary:** Font properties control typeface, size, weight, and style. Use web-safe fonts, Google Fonts, or custom fonts to create readable, branded typography.

## Font Family

**Property:** `font-family`

**Syntax:**
```css
.element {
  font-family: "Primary Font", "Fallback Font", generic-family;
}
```

**Examples:**
```css
body {
  font-family: "Helvetica Neue", Arial, sans-serif;
}

.heading {
  font-family: Georgia, "Times New Roman", serif;
}

.code {
  font-family: "Courier New", Courier, monospace;
}
```

**Generic families:**
- `serif` - Times, Georgia
- `sans-serif` - Arial, Helvetica
- `monospace` - Courier
- `cursive` - Comic Sans
- `fantasy` - Impact

## Font Size

**Property:** `font-size`

**Values:** `px`, `em`, `rem`, `%`, keywords

```css
/* Pixels (absolute) */
.px { font-size: 16px; }

/* Rem (relative to root) */
.rem { font-size: 1rem; } /* 16px if root is 16px */

/* Em (relative to parent) */
.em { font-size: 1.5em; } /* 1.5× parent size */

/* Percentage */
.percent { font-size: 120%; }

/* Keywords */
.small { font-size: small; }
.large { font-size: large; }
```

**Best practice:** Use `rem` for responsive sizing

```css
html { font-size: 16px; }
body { font-size: 1rem; } /* 16px */
h1 { font-size: 2.5rem; } /* 40px */
h2 { font-size: 2rem; } /* 32px */
small { font-size: 0.875rem; } /* 14px */
```

## Font Weight

**Property:** `font-weight`

**Values:** `normal`, `bold`, `100`-`900`

```css
.light { font-weight: 300; }
.normal { font-weight: 400; }
.medium { font-weight: 500; }
.semibold { font-weight: 600; }
.bold { font-weight: 700; }
.extrabold { font-weight: 800; }
.black { font-weight: 900; }
```

## Font Style

**Property:** `font-style`

**Values:** `normal`, `italic`, `oblique`

```css
.italic { font-style: italic; }
.oblique { font-style: oblique; }
.normal { font-style: normal; }
```

## Google Fonts

**1. Import in HTML:**
```html
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
```

**2. Use in CSS:**
```css
body {
  font-family: 'Roboto', sans-serif;
}
```

**Or import in CSS:**
```css
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap');

body {
  font-family: 'Roboto', sans-serif;
}
```

## Custom Fonts

**@font-face:**
```css
@font-face {
  font-family: 'MyCustomFont';
  src: url('fonts/mycustomfont.woff2') format('woff2'),
       url('fonts/mycustomfont.woff') format('woff');
  font-weight: normal;
  font-style: normal;
}

.custom {
  font-family: 'MyCustomFont', Arial, sans-serif;
}
```

## Font Shorthand

```css
.element {
  font: [style] [weight] [size]/[line-height] [family];
}
```

**Examples:**
```css
.shorthand {
  font: italic bold 16px/1.5 Arial, sans-serif;
}

/* Equivalent longhand */
.longhand {
  font-style: italic;
  font-weight: bold;
  font-size: 16px;
  line-height: 1.5;
  font-family: Arial, sans-serif;
}
```

## Browser Support

Universal support for basic fonts. Web fonts: IE9+.

## Best Practices

**Use system fonts for performance**
```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
}
```

**Limit web font weights** (faster loading)
```html
<!-- Good: 2-3 weights -->
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap">
```

**Don't load too many fonts**
```html
<!-- Bad: slow -->
<link href="...font1...">
<link href="...font2...">
<link href="...font3...">
```

---

**Last Updated:** November 15, 2025
**Category:** Typography
**Difficulty:** Beginner
