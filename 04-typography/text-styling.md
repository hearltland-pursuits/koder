---
title: CSS Text Styling
category: Typography
order: 1
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Text Styling

> **Quick Summary:** CSS text properties control how text appears on your webpage—color, alignment, decoration, transformation, spacing, and shadows. Mastering typography creates readable, beautiful, and professional-looking content.

## Table of Contents
- [Introduction](#introduction)
- [Why Typography Matters](#why-typography-matters)
- [Text Color](#text-color)
- [Text Alignment](#text-alignment)
- [Text Decoration](#text-decoration)
- [Text Transformation](#text-transformation)
- [Text Spacing](#text-spacing)
- [Text Shadow](#text-shadow)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

Typography is 95% of web design. While images and colors catch the eye, text communicates your message. Good typography is invisible—readers absorb content effortlessly. Bad typography is exhausting—users leave before reading a paragraph.

CSS text properties let you control every aspect of how text appears: **color** for emphasis, **alignment** for organization, **line-height** for readability, **letter-spacing** for elegance, and **text-shadow** for depth. Professional developers use these properties strategically to create hierarchy (headlines vs body text), improve accessibility (sufficient contrast and spacing), and match brand personality (playful vs formal).

Typography isn't just about looking good—it's about communication. A well-spaced paragraph with proper line height improves reading comprehension by 20%. Proper color contrast makes content accessible to users with visual impairments. Strategic capitalization guides attention. Text shadows add depth without images. Master these properties, and your content becomes more engaging, readable, and professional.

**Key Concept:** Typography creates hierarchy. Readers should instantly know what's important (large, bold headings) vs supplementary (small, light-colored text).

---

## Why Typography Matters

### 1. **Readability**
Poor typography exhausts readers:
- **Tiny text** (< 14px on mobile) → Eye strain
- **Tight line spacing** (line-height < 1.4) → Lines blur together
- **Long line length** (> 75 characters) → Readers lose their place
- **Low contrast** (light gray on white) → Unreadable

Good typography feels effortless.

### 2. **Hierarchy**
Text styling creates visual organization:
- **H1:** Large, bold, dark → Main topic
- **H2:** Medium, semi-bold → Sections
- **Body:** Regular size/weight → Content
- **Captions:** Small, light → Supplementary info

Users scan headings to find relevant content.

### 3. **Accessibility**
Text properties affect users with disabilities:
- **Color contrast:** 4.5:1 minimum for body text (WCAG AA)
- **Font size:** Minimum 16px for body text
- **Line height:** 1.5 minimum for readability
- **Line length:** 50-75 characters for comfortable reading

### 4. **Brand Personality**

| Style | Impression | Use Case |
|-------|------------|----------|
| **ALL CAPS** | Urgent, bold, shouting | Headlines, CTAs |
| **Sentence case** | Professional, formal | Business sites |
| **lowercase** | Casual, friendly, modern | Creative brands |
| **Wide letter-spacing** | Elegant, luxury | Premium products |
| **Tight letter-spacing** | Dense, technical | Data-heavy content |

---

## Text Color

**Property:** `color`

**Syntax:**
```css
.element {
  color: value;
}
```

**Values:** Any CSS color (named, HEX, RGB, HSL)

### Examples

```css
/* Named color */
.red-text {
  color: red;
}

/* HEX */
.brand-blue {
  color: #3498db;
}

/* RGB */
.dark-gray {
  color: rgb(51, 51, 51);
}

/* RGBA (with transparency) */
.faded-text {
  color: rgba(0, 0, 0, 0.5); /* 50% transparent black */
}

/* HSL */
.vibrant-green {
  color: hsl(145, 75%, 50%);
}
```

### Accessible Color Contrast

**Minimum contrast ratios (WCAG):**
- **Body text (< 18pt):** 4.5:1 ratio
- **Large text (≥ 18pt):** 3:1 ratio
- **UI components:** 3:1 ratio

**Good combinations:**
```css
/* ✅ Passes WCAG AA (7.0:1 ratio) */
.readable {
  color: #333333; /* Dark gray */
  background-color: #ffffff; /* White */
}

/* ❌ Fails WCAG (2.1:1 ratio) */
.unreadable {
  color: #aaaaaa; /* Light gray */
  background-color: #ffffff; /* White */
}
```

**Tool:** [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)

---

## Text Alignment

**Property:** `text-align`

**Values:** `left`, `right`, `center`, `justify`

### Examples

```css
/* Left-aligned (default for LTR languages) */
.left-text {
  text-align: left;
}

/* Right-aligned */
.right-text {
  text-align: right;
}

/* Centered */
.centered-text {
  text-align: center;
}

/* Justified (flush with both margins) */
.justified-text {
  text-align: justify;
}
```

### When to Use Each

| Alignment | Best For | Avoid For |
|-----------|----------|-----------|
| **Left** | Body paragraphs (LTR languages) | Headings (sometimes) |
| **Right** | Captions, quotes, dates | Body text (hard to read) |
| **Center** | Headings, short text, callouts | Long paragraphs |
| **Justify** | Formal documents, newspapers | Web content (creates rivers) |

**Note:** Justified text can create awkward spacing ("rivers" of whitespace). Use with `hyphens: auto` for better results.

---

## Text Decoration

**Property:** `text-decoration`

**Values:** `none`, `underline`, `overline`, `line-through`

### Examples

```css
/* Remove underline from links */
a {
  text-decoration: none;
}

/* Underline text */
.underlined {
  text-decoration: underline;
}

/* Strike-through (deleted text) */
.deleted {
  text-decoration: line-through;
}

/* Overline (rare) */
.overline {
  text-decoration: overline;
}

/* Multiple decorations */
.fancy {
  text-decoration: underline overline;
}
```

### Styling Decorations

**Modern CSS allows customizing decoration style:**

```css
.custom-underline {
  text-decoration: underline;
  text-decoration-color: #3498db; /* Blue underline */
  text-decoration-style: wavy; /* Wavy line */
  text-decoration-thickness: 2px; /* Thicker line */
}

/* Shorthand */
.shorthand {
  text-decoration: underline wavy #3498db 2px;
}
```

**Decoration styles:**
- `solid` (default)
- `double`
- `dotted`
- `dashed`
- `wavy`

---

## Text Transformation

**Property:** `text-transform`

**Values:** `none`, `uppercase`, `lowercase`, `capitalize`

### Examples

```css
/* ALL CAPS */
.uppercase {
  text-transform: uppercase;
}

/* all lowercase */
.lowercase {
  text-transform: lowercase;
}

/* Capitalize First Letter Of Each Word */
.capitalize {
  text-transform: capitalize;
}

/* Original text (remove transformation) */
.normal {
  text-transform: none;
}
```

### Use Cases

```css
/* Brand names in caps */
.logo {
  text-transform: uppercase;
  letter-spacing: 2px;
  font-weight: bold;
}

/* Navigation links */
.nav-link {
  text-transform: uppercase;
  font-size: 14px;
}

/* Proper names */
.author-name {
  text-transform: capitalize;
}
```

---

## Text Spacing

### 1. Line Height

**Property:** `line-height`

**Controls:** Vertical spacing between lines of text.

```css
/* Tight spacing (hard to read) */
.tight {
  line-height: 1.0; /* 100% of font size */
}

/* Comfortable reading (recommended) */
.readable {
  line-height: 1.6; /* 160% of font size */
}

/* Loose spacing */
.loose {
  line-height: 2.0; /* 200% of font size */
}

/* Pixel value */
.fixed {
  font-size: 16px;
  line-height: 24px; /* 24px between baselines */
}
```

**Best practice:** Use unitless values (1.5, 1.6) which scale with font size.

**Recommended line-heights:**
- **Body text:** 1.5 - 1.6
- **Headings:** 1.2 - 1.3
- **UI text (buttons):** 1.0 - 1.2

---

### 2. Letter Spacing

**Property:** `letter-spacing`

**Controls:** Horizontal space between characters.

```css
/* Tight spacing */
.tight-letters {
  letter-spacing: -1px;
}

/* Normal spacing (default) */
.normal-letters {
  letter-spacing: normal;
}

/* Loose spacing */
.spaced-letters {
  letter-spacing: 2px;
}

/* Very loose (luxury feel) */
.luxury {
  letter-spacing: 5px;
  text-transform: uppercase;
}
```

**Use cases:**
- **Tight (`-1px to -0.5px`):** Headlines, large text
- **Normal (`0`):** Body text
- **Loose (`1px - 5px`):** Uppercase headings, logos, elegant designs

---

### 3. Word Spacing

**Property:** `word-spacing`

**Controls:** Space between words.

```css
/* Increase word spacing */
.wide-words {
  word-spacing: 10px;
}

/* Decrease word spacing */
.tight-words {
  word-spacing: -2px;
}
```

**Rarely used** — letter-spacing and line-height are more commonly adjusted.

---

## Text Shadow

**Property:** `text-shadow`

**Syntax:** `text-shadow: x-offset y-offset blur-radius color;`

### Examples

```css
/* Basic shadow */
.simple-shadow {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  /*           ↑   ↑   ↑   ↑
               |   |   |   └─ Color (semi-transparent black)
               |   |   └───── Blur radius
               |   └───────── Vertical offset
               └───────────── Horizontal offset */
}

/* No blur (sharp shadow) */
.sharp-shadow {
  text-shadow: 3px 3px 0 #000;
}

/* Glow effect */
.glow {
  color: white;
  text-shadow: 0 0 10px #3498db,
               0 0 20px #3498db,
               0 0 30px #3498db;
}

/* 3D effect (multiple shadows) */
.three-d {
  color: white;
  text-shadow: 1px 1px 0 #ccc,
               2px 2px 0 #aaa,
               3px 3px 0 #888,
               4px 4px 0 #666;
}

/* Subtle depth */
.subtle {
  color: #2c3e50;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}
```

### When to Use

✅ **Good for:**
- Creating depth on headings
- Improving legibility over images
- Glow effects for emphasis
- 3D text effects

❌ **Avoid for:**
- Body text (reduces readability)
- Overusing (looks dated)
- Excessive blur (looks blurry, not shadowy)

---

## Examples

### Example 1: Professional Article Typography

**HTML:**
```html
<article>
  <h1>The Art of Typography</h1>
  <p class="lead">Master text styling to create beautiful, readable content.</p>
  <p class="body-text">
    Typography is more than choosing fonts—it's about creating hierarchy, improving readability,
    and guiding readers through content effortlessly.
  </p>
  <p class="caption">Published on November 15, 2025</p>
</article>
```

**CSS:**
```css
article {
  max-width: 700px;
  margin: 40px auto;
  padding: 20px;
  font-family: Georgia, serif;
}

h1 {
  color: #2c3e50;
  font-size: 42px;
  line-height: 1.2;
  margin-bottom: 16px;
  text-align: center;
}

.lead {
  color: #555;
  font-size: 24px;
  line-height: 1.4;
  text-align: center;
  margin-bottom: 32px;
}

.body-text {
  color: #333;
  font-size: 18px;
  line-height: 1.6;
  margin-bottom: 20px;
  text-align: left;
}

.caption {
  color: #999;
  font-size: 14px;
  text-align: right;
  font-style: italic;
}
```

---

### Example 2: Modern Hero Section

**HTML:**
```html
<section class="hero">
  <h1 class="hero-title">Build Amazing Websites</h1>
  <p class="hero-subtitle">Learn CSS from beginner to professional</p>
</section>
```

**CSS:**
```css
.hero {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  text-align: center;
  padding: 20px;
}

.hero-title {
  font-size: 64px;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 3px;
  margin-bottom: 20px;
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.3);
}

.hero-subtitle {
  font-size: 24px;
  font-weight: 300;
  letter-spacing: 1px;
  text-shadow: 1px 1px 4px rgba(0, 0, 0, 0.2);
}
```

---

## Common Use Cases

### Use Case 1: Link Styling

```css
/* Remove default underline, add on hover */
a {
  color: #3498db;
  text-decoration: none;
  transition: color 0.3s;
}

a:hover {
  color: #2980b9;
  text-decoration: underline;
}
```

---

### Use Case 2: Emphasis Text

```css
/* Highlighted important text */
.highlight {
  color: #e74c3c;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
}
```

---

### Use Case 3: Readable Body Text

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  font-size: 18px;
  line-height: 1.6;
  color: #333;
  max-width: 700px;
  margin: 0 auto;
  padding: 20px;
}
```

---

## Browser Support

All text styling properties have universal browser support.

| Property | Chrome | Firefox | Safari | Edge | IE |
|----------|--------|---------|--------|------|----|
| `color` | 1+ | 1+ | 1+ | 12+ | 3+ |
| `text-align` | 1+ | 1+ | 1+ | 12+ | 3+ |
| `text-decoration` | 1+ | 1+ | 1+ | 12+ | 3+ |
| `text-transform` | 1+ | 1+ | 1+ | 12+ | 4+ |
| `line-height` | 1+ | 1+ | 1+ | 12+ | 4+ |
| `letter-spacing` | 1+ | 1+ | 1+ | 12+ | 4+ |
| `text-shadow` | 4+ | 3.5+ | 4+ | 12+ | 10+ |

---

## Best Practices

### ✅ Do This

1. **Set Base Typography on Body**
   ```css
   body {
     font-family: Arial, sans-serif;
     font-size: 16px;
     line-height: 1.6;
     color: #333;
   }
   ```

2. **Use Relative Units for Line Height**
   ```css
   /* Good - scales with font size */
   p { line-height: 1.6; }

   /* Avoid - fixed value doesn't scale */
   p { line-height: 24px; }
   ```

3. **Ensure Sufficient Contrast**
   ```css
   /* Good - 12:1 contrast */
   .readable { color: #000; background: #fff; }

   /* Bad - 1.5:1 contrast */
   .unreadable { color: #ccc; background: #fff; }
   ```

4. **Limit Line Length**
   ```css
   article {
     max-width: 700px; /* ~75 characters */
   }
   ```

---

### ❌ Avoid This

1. **Don't Use `justify` for Web Content**
   ```css
   /* Bad - creates awkward spacing */
   p { text-align: justify; }
   ```

2. **Don't Make Body Text Too Small**
   ```css
   /* Bad - eye strain */
   body { font-size: 12px; }

   /* Good - readable */
   body { font-size: 16px; }
   ```

3. **Don't Overuse Text Effects**
   ```css
   /* Bad - distracting */
   p {
     text-shadow: 5px 5px 10px red;
     text-transform: uppercase;
     letter-spacing: 10px;
   }
   ```

---

## Video Tutorial

### 🎥 CSS Tutorial - Full Course for Beginners

**Watch Text Styling:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=4500s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=4500s)

**Relevant Timestamps:**
- `1:15:00` - Text color
- `1:20:30` - Text alignment
- `1:25:00` - Text decoration
- `1:30:15` - Text transformation
- `1:35:45` - Line height and spacing
- `1:42:00` - Text shadows

**Additional Resources:**
- [W3Schools - CSS Text](https://www.w3schools.com/css/css_text.asp)
- [MDN - Styling Text](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text)
- [Practical Typography](https://practicaltypography.com/)

---

## Related Topics

**Prerequisites:**
- [CSS Colors](../02-colors/colors-overview.md)

**Related Concepts:**
- [Fonts](fonts.md) - Font families and sizing
- [Google Fonts](google-fonts.md) - Using web fonts

**Next Steps:**
- [CSS Box Model](../03-box-model/box-model-concept.md)
- [CSS Layout](../05-layout-basics/position.md)

---

## Practice Exercise

### 🎯 Challenge: Style a Blog Post

**Objective:** Apply text styling to create professional, readable blog content.

**Requirements:**
- [ ] Heading with text-shadow
- [ ] Lead paragraph (larger, different color)
- [ ] Body text (proper line-height, readable size)
- [ ] Styled links (no underline, hover effect)
- [ ] Caption text (smaller, right-aligned)

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**CSS:**
```css
article {
  max-width: 700px;
  margin: 60px auto;
  padding: 40px;
  font-family: Georgia, serif;
  background-color: white;
}

h1 {
  color: #2c3e50;
  font-size: 48px;
  line-height: 1.2;
  text-align: center;
  margin-bottom: 24px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
}

.lead {
  font-size: 22px;
  color: #555;
  line-height: 1.5;
  text-align: center;
  margin-bottom: 40px;
}

p {
  font-size: 18px;
  line-height: 1.7;
  color: #333;
  margin-bottom: 20px;
}

a {
  color: #3498db;
  text-decoration: none;
  border-bottom: 1px solid transparent;
  transition: border-color 0.3s;
}

a:hover {
  border-bottom-color: #3498db;
}

.caption {
  font-size: 14px;
  color: #999;
  text-align: right;
  font-style: italic;
  margin-top: 40px;
}
```

</details>

---

**Last Updated:** November 15, 2025
**Category:** Typography
**Difficulty:** Beginner
