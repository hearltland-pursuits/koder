---
title: HEX Colors
category: Colors
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# HEX Colors

> **Quick Summary:** HEX colors use hexadecimal (base-16) notation to define RGB values in a compact format: `#RRGGBB`. Supports 3-digit shorthand (#RGB), 8-digit with alpha (#RRGGBBAA), and is the most common color format in web design.

## Table of Contents
- [Introduction](#introduction)
- [HEX Syntax](#hex-syntax)
- [3-Digit vs 6-Digit HEX](#3-digit-vs-6-digit-hex)
- [How HEX Works](#how-hex-works)
- [HEX with Alpha](#hex-with-alpha)
- [Common HEX Colors](#common-hex-colors)
- [Examples](#examples)
- [Converting Colors](#converting-colors)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)

---

## Introduction

**HEX (Hexadecimal):** A compact way to represent RGB colors using base-16 numbers (0-9, A-F).

**Why HEX is popular:**
- Compact format (`#FF0000` vs `rgb(255, 0, 0)`)
- Industry standard in design tools (Photoshop, Figma)
- Easy to copy/paste from design mockups
- No spaces, easy to share

---

## HEX Syntax

**6-digit format:**
```css
#RRGGBB
```

- **RR** = Red (00-FF)
- **GG** = Green (00-FF)
- **BB** = Blue (00-FF)

**Examples:**
```css
.red { color: #FF0000; }
.green { color: #00FF00; }
.blue { color: #0000FF; }
.white { color: #FFFFFF; }
.black { color: #000000; }
```

**Note:** Case-insensitive (`#FF0000` = `#ff0000`)

---

## 3-Digit vs 6-Digit HEX

### 3-Digit Shorthand

**When both digits in each pair are identical:**
```css
#RGB  →  #RRGGBB

#F00  →  #FF0000  /* Red */
#0F0  →  #00FF00  /* Green */
#00F  →  #0000FF  /* Blue */
#FFF  →  #FFFFFF  /* White */
#000  →  #000000  /* Black */
```

### 6-Digit Full Format

**Use when digits aren't identical:**
```css
#FF5733  /* Orange-red */
#3498DB  /* Blue */
#2ECC71  /* Green */
#E74C3C  /* Red */
```

**Rule:** Always expand to 6 digits if shorthand isn't possible

```css
/* ❌ Can't shorten - digits differ */
#FF5733  /* Must use 6 digits */

/* ✅ Can shorten */
#FFAA00  →  #FA0
```

---

## How HEX Works

### Hexadecimal System

**Base-16 counting:**
```
0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F
```

- **0** = 0 (decimal)
- **9** = 9 (decimal)
- **A** = 10 (decimal)
- **F** = 15 (decimal)
- **FF** = 255 (decimal)
- **00** = 0 (decimal)

### HEX to Decimal Conversion

**Formula:** `(16 × first digit) + (1 × second digit)`

**Examples:**
```
FF = (16 × 15) + (1 × 15) = 240 + 15 = 255
80 = (16 × 8) + (1 × 0) = 128 + 0 = 128
1A = (16 × 1) + (1 × 10) = 16 + 10 = 26
00 = (16 × 0) + (1 × 0) = 0
```

### Breaking Down a HEX Color

**Example:** `#3498DB` (blue)

```
  #  34    98    DB
     ↓     ↓     ↓
    Red  Green  Blue

34 = 52 (decimal)
98 = 152 (decimal)
DB = 219 (decimal)

#3498DB = rgb(52, 152, 219)
```

---

## HEX with Alpha

**8-digit format (with transparency):**
```css
#RRGGBBAA
```

- **AA** = Alpha channel (00 = transparent, FF = opaque)

**Examples:**
```css
#FF0000FF  /* Solid red (100% opacity) */
#FF000080  /* 50% transparent red */
#00000000  /* Fully transparent black */
#FFFFFF99  /* 60% opaque white */
```

**3-digit alpha shorthand:**
```css
#RGBA  →  #RRGGBBAA

#F00F  →  #FF0000FF  /* Solid red */
#F008  →  #FF000088  /* ~50% red */
```

**Alpha conversion table:**
```
FF = 100%  (fully opaque)
CC = 80%
99 = 60%
80 = 50%
66 = 40%
4D = 30%
33 = 20%
1A = 10%
00 = 0%   (fully transparent)
```

---

## Common HEX Colors

### Basic Colors

```css
#FF0000  /* Red */
#00FF00  /* Lime */
#0000FF  /* Blue */
#FFFF00  /* Yellow */
#FF00FF  /* Magenta */
#00FFFF  /* Cyan */
#FFFFFF  /* White */
#000000  /* Black */
```

### Grayscale

```css
#000000  /* Black */
#333333  /* Dark gray */
#666666  /* Medium gray */
#999999  /* Light gray */
#CCCCCC  /* Very light gray */
#FFFFFF  /* White */
```

### Popular Web Colors

```css
#3498DB  /* Dodger blue (Bootstrap primary) */
#2ECC71  /* Emerald green (success) */
#E74C3C  /* Alizarin red (danger) */
#F39C12  /* Orange (warning) */
#9B59B6  /* Amethyst purple */
#1ABC9C  /* Turquoise */
#34495E  /* Wet asphalt (dark gray) */
#ECF0F1  /* Clouds (light gray) */
```

---

## Examples

### Example 1: Brand Colors

```css
:root {
  --brand-primary: #3498DB;
  --brand-secondary: #2ECC71;
  --brand-accent: #E74C3C;
  --brand-dark: #2C3E50;
  --brand-light: #ECF0F1;
}

.button-primary {
  background-color: var(--brand-primary);
  color: #FFFFFF;
}
```

---

### Example 2: Color Palette

```css
/* Monochromatic blue palette */
.blue-lightest { background: #EBF5FB; }
.blue-lighter { background: #AED6F1; }
.blue-light { background: #5DADE2; }
.blue-base { background: #3498DB; }
.blue-dark { background: #2874A6; }
.blue-darkest { background: #1B4F72; }
```

---

### Example 3: Gradients with HEX

```css
.gradient {
  background: linear-gradient(135deg, #667EEA 0%, #764BA2 100%);
}

.gradient-sunset {
  background: linear-gradient(to right, #FF512F, #DD2476);
}
```

---

### Example 4: HEX with Alpha Transparency

```css
.overlay {
  background-color: #00000080; /* 50% black */
}

.modal {
  background-color: #FFFFFFCC; /* 80% white */
  box-shadow: 0 4px 6px #00000033; /* 20% black shadow */
}
```

---

## Converting Colors

### HEX to RGB

**Manual conversion:**
```
#FF5733
  FF = 255 (red)
  57 = 87 (green)
  33 = 51 (blue)

#FF5733 = rgb(255, 87, 51)
```

**Quick reference:**
```css
#FFFFFF → rgb(255, 255, 255)
#000000 → rgb(0, 0, 0)
#FF0000 → rgb(255, 0, 0)
#00FF00 → rgb(0, 255, 0)
#0000FF → rgb(0, 0, 255)
```

### RGB to HEX

**Convert each channel to HEX:**
```
rgb(52, 152, 219)

52 = 34 (hex)
152 = 98 (hex)
219 = DB (hex)

rgb(52, 152, 219) = #3498DB
```

**Online tools:**
- https://htmlcolorcodes.com/
- https://convertingcolors.com/

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|-----|
| 6-digit HEX (`#RRGGBB`) | 1+ | 1+ | 1+ | 12+ | 3+ |
| 3-digit HEX (`#RGB`) | 1+ | 1+ | 1+ | 12+ | 3+ |
| 8-digit HEX (`#RRGGBBAA`) | 52+ | 49+ | 9.1+ | 79+ | ❌ |

**Note:** Alpha channel support limited in older browsers.

---

## Best Practices

### ✅ Do This

**1. Use lowercase for consistency**
```css
/* ✅ Recommended */
.box { color: #3498db; }

/* Also works but inconsistent */
.box { color: #3498DB; }
```

**2. Use shorthand when possible**
```css
/* ✅ Good - compact */
.white { color: #FFF; }
.black { color: #000; }

/* Works but unnecessary */
.white { color: #FFFFFF; }
```

**3. Use CSS variables for brand colors**
```css
:root {
  --primary: #3498DB;
  --secondary: #2ECC71;
}

.button {
  background: var(--primary);
}
```

**4. Add comments for complex colors**
```css
/* Brand primary - matches logo */
.header {
  background: #3498DB;
}
```

### ❌ Avoid This

**1. Don't use HEX for transparency**
```css
/* ❌ Limited browser support */
.overlay { background: #00000080; }

/* ✅ Better - universal support */
.overlay { background: rgba(0, 0, 0, 0.5); }
```

**2. Don't forget the #**
```css
/* ❌ Invalid - won't work */
.box { color: FF0000; }

/* ✅ Must include # */
.box { color: #FF0000; }
```

**3. Don't use invalid characters**
```css
/* ❌ Only 0-9, A-F allowed */
.box { color: #GGHHII; }

/* ✅ Valid hex digits */
.box { color: #AABBCC; }
```

---

## HEX Color Tools

**Color pickers:**
- Chrome DevTools (built-in color picker)
- https://htmlcolorcodes.com/color-picker/
- https://colorhunt.co/ (palettes)

**Palette generators:**
- https://coolors.co/
- https://paletton.com/
- https://mycolor.space/

**Accessibility checkers:**
- https://webaim.org/resources/contrastchecker/
- https://colorable.jxnblk.com/

---

**Last Updated:** November 15, 2025
**Category:** Colors
**Difficulty:** Beginner

**Related Topics:**
- [RGB Colors](rgb-colors.md) - RGB color format
- [HSL Colors](hsl-colors.md) - Hue, saturation, lightness
- [Colors Overview](colors-overview.md) - All CSS color systems
