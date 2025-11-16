---
title: HSL & HSLA Colors
category: Colors
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# HSL & HSLA Colors

> **Quick Summary:** HSL defines colors using Hue (color wheel position 0-360°), Saturation (color intensity 0-100%), and Lightness (brightness 0-100%). HSL is the most intuitive color model for creating color schemes and variations.

## Table of Contents
- [Introduction](#introduction)
- [HSL Syntax](#hsl-syntax)
- [Understanding HSL](#understanding-hsl)
- [HSLA with Alpha](#hsla-with-alpha)
- [Color Wheel Visualization](#color-wheel-visualization)
- [Creating Color Schemes](#creating-color-schemes)
- [Examples](#examples)
- [When to Use HSL](#when-to-use-hsl)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)

---

## Introduction

**HSL (Hue, Saturation, Lightness):** A color model that matches how humans perceive color relationships.

**Why HSL is better for designers:**
- **Intuitive:** Matches how we think about colors
- **Easy variations:** Create lighter/darker shades by changing one value
- **Color harmony:** Simple to create complementary/analogous colors
- **Saturation control:** Easy to create muted or vibrant palettes

**Comparison:**
```css
/* RGB: Hard to predict result */
rgb(135, 206, 250)  /* What color is this? */

/* HSL: Obvious what you're getting */
hsl(203, 92%, 75%)  /* Blue, vibrant, light */
```

---

## HSL Syntax

**Format:**
```css
hsl(hue, saturation%, lightness%)
```

**Parameters:**
- **Hue:** 0-360 (degrees on color wheel)
- **Saturation:** 0%-100% (gray to vibrant)
- **Lightness:** 0%-100% (black to white)

**Examples:**
```css
.red { color: hsl(0, 100%, 50%); }
.green { color: hsl(120, 100%, 50%); }
.blue { color: hsl(240, 100%, 50%); }
.gray { color: hsl(0, 0%, 50%); }
```

---

## Understanding HSL

### Hue (0-360)

**Color wheel positions:**
```css
hsl(0, 100%, 50%)    /* Red */
hsl(30, 100%, 50%)   /* Orange */
hsl(60, 100%, 50%)   /* Yellow */
hsl(120, 100%, 50%)  /* Green */
hsl(180, 100%, 50%)  /* Cyan */
hsl(240, 100%, 50%)  /* Blue */
hsl(300, 100%, 50%)  /* Magenta */
hsl(360, 100%, 50%)  /* Red (full circle) */
```

**Hue is a circle:** 0° = 360° (both are red)

### Saturation (0-100%)

**How vibrant the color is:**
```css
/* Same hue and lightness, different saturation */
hsl(240, 0%, 50%)    /* Gray (no color) */
hsl(240, 25%, 50%)   /* Muted blue */
hsl(240, 50%, 50%)   /* Blue */
hsl(240, 75%, 50%)   /* Vibrant blue */
hsl(240, 100%, 50%)  /* Pure blue (max vibrancy) */
```

**Rule:** 0% saturation = always gray (regardless of hue)

### Lightness (0-100%)

**How bright the color is:**
```css
/* Same hue and saturation, different lightness */
hsl(240, 100%, 0%)    /* Black */
hsl(240, 100%, 25%)   /* Dark blue */
hsl(240, 100%, 50%)   /* Pure blue */
hsl(240, 100%, 75%)   /* Light blue */
hsl(240, 100%, 100%)  /* White */
```

**Rule:**
- 0% lightness = always black
- 100% lightness = always white
- 50% lightness = truest color

---

## HSLA with Alpha

**Format with transparency:**
```css
hsla(hue, saturation%, lightness%, alpha)
```

**Alpha:** 0 (transparent) to 1 (opaque)

**Examples:**
```css
.semi-transparent { background: hsla(240, 100%, 50%, 0.5); } /* 50% blue */
.mostly-opaque { background: hsla(0, 100%, 50%, 0.9); } /* 90% red */
.subtle { background: hsla(120, 100%, 50%, 0.1); } /* 10% green */
```

---

## Color Wheel Visualization

```
        Yellow (60°)
           |
   Orange  |  Yellow-Green
    (30°)  |  (90°)
       \   |   /
Red -------|------- Green
 (0°)      |       (120°)
       /   |   \
Magenta    |    Cyan
  (300°)   |    (180°)
           |
        Blue (240°)
```

**Primary colors:** 0°, 120°, 240° (Red, Green, Blue)
**Secondary colors:** 60°, 180°, 300° (Yellow, Cyan, Magenta)

---

## Creating Color Schemes

### Monochromatic (Same Hue)

**Vary lightness only:**
```css
:root {
  --base: hsl(220, 70%, 50%);
  --lighter: hsl(220, 70%, 70%);
  --lightest: hsl(220, 70%, 90%);
  --darker: hsl(220, 70%, 30%);
  --darkest: hsl(220, 70%, 10%);
}
```

### Complementary (Opposite Hues)

**180° apart:**
```css
:root {
  --primary: hsl(220, 70%, 50%);     /* Blue */
  --complement: hsl(40, 70%, 50%);   /* Orange (220 + 180 = 400 - 360 = 40) */
}
```

### Analogous (Adjacent Hues)

**±30° apart:**
```css
:root {
  --main: hsl(220, 70%, 50%);      /* Blue */
  --left: hsl(190, 70%, 50%);      /* Cyan (220 - 30) */
  --right: hsl(250, 70%, 50%);     /* Purple (220 + 30) */
}
```

### Triadic (120° Apart)

```css
:root {
  --color1: hsl(0, 70%, 50%);      /* Red */
  --color2: hsl(120, 70%, 50%);    /* Green */
  --color3: hsl(240, 70%, 50%);    /* Blue */
}
```

---

## Examples

### Example 1: Creating Shades

```css
/* Base color */
.button {
  background: hsl(210, 80%, 50%);
  color: white;
}

/* Lighter shade for hover */
.button:hover {
  background: hsl(210, 80%, 60%); /* +10% lightness */
}

/* Darker shade for active */
.button:active {
  background: hsl(210, 80%, 40%); /* -10% lightness */
}

/* Disabled (desaturated) */
.button:disabled {
  background: hsl(210, 20%, 50%); /* -60% saturation */
}
```

---

### Example 2: Dynamic Theme

```css
:root {
  --hue: 220; /* Blue theme */
  --saturation: 70%;

  --primary: hsl(var(--hue), var(--saturation), 50%);
  --primary-light: hsl(var(--hue), var(--saturation), 70%);
  --primary-dark: hsl(var(--hue), var(--saturation), 30%);

  /* Complementary color (opposite on wheel) */
  --secondary: hsl(calc(var(--hue) + 180), var(--saturation), 50%);
}

/* Switch to green theme by changing --hue to 120 */
```

---

### Example 3: Accessibility-Friendly Palette

```css
/* Ensure sufficient contrast by controlling lightness */
:root {
  --bg-light: hsl(220, 20%, 95%);  /* Very light background */
  --text-dark: hsl(220, 20%, 20%); /* Dark text (sufficient contrast) */

  --primary: hsl(220, 70%, 50%);
  --primary-accessible: hsl(220, 70%, 40%); /* Darker for WCAG AAA */
}
```

---

### Example 4: Grayscale with HSL

```css
/* Saturation = 0% creates perfect grayscale */
.black { color: hsl(0, 0%, 0%); }
.dark-gray { color: hsl(0, 0%, 25%); }
.gray { color: hsl(0, 0%, 50%); }
.light-gray { color: hsl(0, 0%, 75%); }
.white { color: hsl(0, 0%, 100%); }

/* Hue doesn't matter when saturation is 0 */
hsl(120, 0%, 50%) === hsl(240, 0%, 50%) /* Both are gray */
```

---

## When to Use HSL

### Use HSL When:

**1. Creating color variations**
```css
/* Easy to create lighter/darker versions */
.base { background: hsl(200, 70%, 50%); }
.light { background: hsl(200, 70%, 70%); }
.dark { background: hsl(200, 70%, 30%); }
```

**2. Building design systems**
```css
/* Generate entire palette from one hue */
:root {
  --brand-hue: 210;
  --brand-100: hsl(var(--brand-hue), 70%, 95%);
  --brand-300: hsl(var(--brand-hue), 70%, 75%);
  --brand-500: hsl(var(--brand-hue), 70%, 50%);
  --brand-700: hsl(var(--brand-hue), 70%, 25%);
  --brand-900: hsl(var(--brand-hue), 70%, 10%);
}
```

**3. Creating color harmony**
```css
/* Complementary colors */
--primary: hsl(220, 70%, 50%);
--secondary: hsl(40, 70%, 50%); /* 220 + 180 */
```

**4. Dynamic theming**
```javascript
// Easy to manipulate with JavaScript
element.style.backgroundColor = `hsl(${hue}, 70%, 50%)`;
```

### Use RGB/HEX When:

- Converting from design tools (HEX)
- Working with existing brand colors
- Transparency needed (RGBA has better support than HSLA)

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|-----|
| `hsl()` | 1+ | 1+ | 3.1+ | 12+ | 9+ |
| `hsla()` | 1+ | 3+ | 3.1+ | 12+ | 9+ |

**Excellent support** - HSL works in all modern browsers.

---

## Best Practices

### Do This

**1. Use HSL for color systems**
```css
:root {
  --primary-hue: 220;

  --primary-50: hsl(var(--primary-hue), 70%, 95%);
  --primary-500: hsl(var(--primary-hue), 70%, 50%);
  --primary-900: hsl(var(--primary-hue), 70%, 10%);
}
```

**2. Create shades by changing lightness**
```css
/* Intuitive */
.light { color: hsl(220, 70%, 70%); }
.base { color: hsl(220, 70%, 50%); }
.dark { color: hsl(220, 70%, 30%); }
```

**3. Use CSS custom properties for theming**
```css
:root {
  --theme-hue: 220;
}

.theme-blue { --theme-hue: 220; }
.theme-green { --theme-hue: 120; }
.theme-red { --theme-hue: 0; }

.button {
  background: hsl(var(--theme-hue), 70%, 50%);
}
```

### Avoid This

**1. Don't use extreme saturation for text**
```css
/* Bad - too vibrant, hard to read */
.text { color: hsl(240, 100%, 50%); }

/* Good - muted */
.text { color: hsl(240, 30%, 30%); }
```

**2. Don't forget lightness affects all hues**
```css
/* These are all white (100% lightness) */
hsl(0, 100%, 100%)
hsl(120, 100%, 100%)
hsl(240, 100%, 100%)

/* Use 50% for true colors */
hsl(0, 100%, 50%)   /* Red */
hsl(120, 100%, 50%) /* Green */
hsl(240, 100%, 50%) /* Blue */
```

---

**Last Updated:** November 15, 2025
**Category:** Colors
**Difficulty:** Beginner

**Related Topics:**
- [RGB Colors](rgb-colors.md) - RGB color format
- [HEX Colors](hex-colors.md) - Hexadecimal colors
- [Colors Overview](colors-overview.md) - All CSS color systems
