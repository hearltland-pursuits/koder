---
title: CSS Lists
category: Typography
order: 6
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Lists

> **Quick Summary:** CSS provides properties to style ordered (`<ol>`) and unordered (`<ul>`) lists, including bullet/number types, positioning, and custom markers using `::marker` pseudo-element or `list-style-image`.

## Table of Contents
- [Introduction](#introduction)
- [List Style Properties](#list-style-properties)
- [List Style Type](#list-style-type)
- [List Style Position](#list-style-position)
- [List Style Image](#list-style-image)
- [Custom List Markers](#custom-list-markers)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

HTML lists come in three types:
- **Unordered lists** (`<ul>`) - Bullets
- **Ordered lists** (`<ol>`) - Numbers/letters
- **Description lists** (`<dl>`) - Terms and definitions

CSS lets you control marker appearance, position, and even replace default markers with custom images or content.

---

## List Style Properties

### Shorthand Syntax

```css
list-style: type position image;
```

### Individual Properties

```css
list-style-type: disc;      /* Marker type */
list-style-position: outside; /* Marker position */
list-style-image: url(icon.png); /* Custom marker */
```

---

## List Style Type

**Controls marker appearance** for `<ul>` and `<ol>`.

### Unordered List Types

```css
ul { list-style-type: disc; }      /* Default: filled circle */
ul { list-style-type: circle; }    /* Hollow circle */
ul { list-style-type: square; }    /* Square */
ul { list-style-type: none; }      /* No marker */
```

### Ordered List Types

```css
ol { list-style-type: decimal; }           /* 1, 2, 3 (default) */
ol { list-style-type: decimal-leading-zero; } /* 01, 02, 03 */
ol { list-style-type: lower-alpha; }       /* a, b, c */
ol { list-style-type: upper-alpha; }       /* A, B, C */
ol { list-style-type: lower-roman; }       /* i, ii, iii */
ol { list-style-type: upper-roman; }       /* I, II, III */
ol { list-style-type: lower-greek; }       /* α, β, γ */
```

**Example:**
```css
.roman-list {
  list-style-type: upper-roman;
}
```

**HTML:**
```html
<ol class="roman-list">
  <li>First</li>
  <li>Second</li>
  <li>Third</li>
</ol>
```

**Result:**
```
I.   First
II.  Second
III. Third
```

---

## List Style Position

**Controls marker placement** relative to list item content.

```css
/* Default: Marker outside text block */
list-style-position: outside;

/* Marker inside text block (indented with text) */
list-style-position: inside;
```

**Visual Comparison:**

**Outside (default):**
```
  • This is a long list item that
    wraps to multiple lines. Notice
    how text aligns with first line.
```

**Inside:**
```
  • This is a long list item that
  wraps to multiple lines. Notice
  how marker is part of text flow.
```

**Example:**
```css
.inside-markers {
  list-style-position: inside;
}
```

---

## List Style Image

**Replace default markers** with custom images.

```css
ul {
  list-style-image: url('checkmark.png');
}

/* Better control with background-image */
ul {
  list-style: none;
  padding-left: 0;
}

ul li {
  padding-left: 30px;
  background-image: url('checkmark.png');
  background-repeat: no-repeat;
  background-position: 0 5px;
  background-size: 20px 20px;
}
```

**Why background-image method is better:**
- More positioning control
- Size control
- Better cross-browser consistency

---

## Custom List Markers

### Using ::marker Pseudo-Element

```css
li::marker {
  color: #007bff;
  font-size: 1.5rem;
  content: "";
}
```

### Using Counters

```css
ol {
  counter-reset: custom-counter;
  list-style: none;
}

ol li {
  counter-increment: custom-counter;
}

ol li::before {
  content: counter(custom-counter) ". ";
  color: #007bff;
  font-weight: bold;
  margin-right: 10px;
}
```

### Nested Counters

```css
ol {
  counter-reset: section;
  list-style: none;
}

ol li {
  counter-increment: section;
}

ol li::before {
  content: counters(section, ".") " ";
}
```

**Result:**
```
1 Item
2 Item
  2.1 Nested
  2.2 Nested
3 Item
```

---

## Examples

### Example 1: Styled Checklist

```css
.checklist {
  list-style: none;
  padding: 0;
}

.checklist li {
  padding: 10px;
  padding-left: 40px;
  position: relative;
  border-bottom: 1px solid #eee;
}

.checklist li::before {
  content: "";
  position: absolute;
  left: 10px;
  font-size: 1.5rem;
  color: #ccc;
}

.checklist li.checked::before {
  content: "";
  color: #28a745;
}
```

---

### Example 2: Navigation Menu (No Bullets)

```css
nav ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  gap: 20px;
}

nav li {
  display: inline-block;
}
```

---

### Example 3: Numbered Steps

```css
.steps {
  counter-reset: step;
  list-style: none;
  padding: 0;
}

.steps li {
  counter-increment: step;
  padding: 20px;
  margin-bottom: 20px;
  background: #f8f9fa;
  border-radius: 8px;
  position: relative;
  padding-left: 80px;
}

.steps li::before {
  content: counter(step);
  position: absolute;
  left: 20px;
  top: 50%;
  transform: translateY(-50%);
  background: #007bff;
  color: white;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  font-size: 1.2rem;
}
```

---

## Common Use Cases

### Use Case 1: Remove Default Bullets for Nav
```css
nav ul {
  list-style: none;
}
```

### Use Case 2: Custom Colored Bullets
```css
li::marker {
  color: #007bff;
}
```

### Use Case 3: Icon-Based Lists
```css
ul {
  list-style: none;
}

ul li::before {
  content: "→ ";
  color: #007bff;
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE 11 |
|----------|--------|---------|--------|------|-------|
| `list-style-type` | All | All | All | All | Full |
| `list-style-position` | All | All | All | All | Full |
| `list-style-image` | All | All | All | All | Full |
| `::marker` | 86+ | 68+ | 11.1+ | 86+ | None |

---

## Best Practices

### Do This

1. **Remove bullets for navigation**
   ```css
   nav ul { list-style: none; }
   ```

2. **Use ::marker for modern styling**
   ```css
   li::marker { color: #007bff; }
   ```

3. **Use counters for complex numbering**
   ```css
   ol { counter-reset: item; }
   li::before { content: counter(item) ". "; }
   ```

### Avoid This

1. **Forgetting to reset padding when removing bullets**
   ```css
   /* Missing padding reset */
   ul { list-style: none; } /* Text still indented */

   /* Better */
   ul { list-style: none; padding: 0; }
   ```

---

## Related Topics

**Prerequisites:**
- [Text Styling](text-styling.md)

**Next Steps:**
- [Navigation Bars](../11-components/navigation-bars.md)

---

## Navigation

**Previous:** [← Links](links.md)
**Next:** [Z-Index →](../05-layout-basics/z-index.md)
**Up:** [↑ Back to Typography](../README.md#4️⃣-typography-6-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Typography
**Difficulty:** Beginner
