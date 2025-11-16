---
title: CSS Comments
category: Fundamentals
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Comments

> **Quick Summary:** CSS comments document your code and are ignored by browsers. Use `/* comment */` syntax for single-line or multi-line comments. Essential for team collaboration and future code maintenance.

## Table of Contents
- [Introduction](#introduction)
- [Comment Syntax](#comment-syntax)
- [Single-Line Comments](#single-line-comments)
- [Multi-Line Comments](#multi-line-comments)
- [Use Cases](#use-cases)
- [Best Practices](#best-practices)
- [Browser Support](#browser-support)
- [Examples](#examples)

---

## Introduction

Comments are notes in your CSS that browsers ignore. They explain what your code does, why certain decisions were made, and help other developers (including future you) understand your stylesheet.

**Key Points:**
- Comments don't affect rendering or performance
- Invisible to users (but visible in source code)
- Only one comment syntax in CSS: `/* */`

---

## Comment Syntax

**CSS comment structure:**
```css
/* This is a comment */
```

**Note:** Unlike HTML (`<!-- -->`), CSS only has one comment style.

---

## Single-Line Comments

```css
/* Single-line comment */
.button {
  color: blue; /* Inline comment after code */
}
```

**Common uses:**
- Quick notes next to specific properties
- Temporarily disable a single line
- Section markers

---

## Multi-Line Comments

```css
/*
  This is a multi-line comment
  that spans several lines.
  Useful for longer explanations.
*/
.card {
  padding: 20px;
}
```

**Common uses:**
- File headers
- Section descriptions
- Complex logic explanations
- Documentation blocks

---

## Use Cases

### 1. File Headers

```css
/*
  File: styles.css
  Author: Joshua Mark Nanninga
  Date: November 15, 2025
  Description: Main stylesheet for portfolio site
*/
```

### 2. Section Dividers

```css
/* ===================
   Navigation Styles
   =================== */
.nav {
  display: flex;
}

/* ===================
   Footer Styles
   =================== */
.footer {
  background: #333;
}
```

### 3. Explaining Complex Code

```css
/*
  Using flexbox for centering because:
  - Works with unknown heights
  - Responsive by default
  - Better browser support than Grid for older browsers
*/
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

### 4. TODO Comments

```css
/* TODO: Add hover state for buttons */
/* FIXME: Color contrast fails WCAG AAA */
/* HACK: Negative margin fixes Safari bug */
.button {
  padding: 10px 20px;
}
```

### 5. Temporarily Disable Code

```css
.box {
  color: blue;
  /* padding: 20px; */ /* Disabled for testing */
  margin: 10px;
}
```

### 6. Browser Hacks Documentation

```css
/* IE11 flexbox bug workaround */
.flex-item {
  flex: 1 1 auto;
  /* min-width: 0; */ /* Prevents flex overflow in IE11 */
}
```

---

## Best Practices

### ✅ Do This

**1. Explain WHY, not WHAT**
```css
/* Good - explains reasoning */
.container {
  max-width: 1200px; /* Optimal reading width for 16px font */
}

/* Bad - states the obvious */
.container {
  max-width: 1200px; /* Sets max width to 1200px */
}
```

**2. Use Section Comments**
```css
/* ========================================
   Component: Card
   ======================================== */
.card {
  /* Styles here */
}
```

**3. Document Browser Hacks**
```css
/* Safari-only fix for position: sticky bug */
@supports (-webkit-appearance: none) {
  .sticky {
    position: -webkit-sticky;
    position: sticky;
  }
}
```

**4. Use TODO/FIXME Tags**
```css
/* TODO: Replace with CSS Grid when IE11 support drops */
/* FIXME: Contrast ratio fails accessibility check */
/* NOTE: This value matches the design system */
```

### ❌ Avoid This

**1. Don't Over-Comment Obvious Code**
```css
/* Bad - unnecessary */
.red {
  color: red; /* Makes text red */
}

/* Good - only comment when needed */
.red {
  color: red;
}
```

**2. Don't Leave Commented-Out Code**
```css
/* Bad - clutters stylesheet */
.button {
  padding: 10px;
  /* background: blue; */
  /* border: 1px solid red; */
  /* margin: 5px; */
}

/* Good - use version control instead */
.button {
  padding: 10px;
}
```

**3. Don't Use Comments for Version History**
```css
/* Bad - use Git instead */
/*
  v1.0 - Added button styles
  v1.1 - Changed blue to navy
  v1.2 - Updated padding
*/
```

---

## Examples

### Example 1: Component Documentation

```css
/* ========================================
   Component: Primary Button

   Usage: <button class="btn-primary">Click</button>

   States: default, hover, active, disabled

   Design: Matches brand color #3498db
   ======================================== */
.btn-primary {
  background-color: #3498db;
  color: white;
  padding: 12px 24px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.btn-primary:hover {
  background-color: #2980b9; /* Darker on hover */
}

.btn-primary:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

---

### Example 2: Responsive Design Notes

```css
/* Mobile-first approach */
.container {
  width: 100%;
  padding: 20px;
}

/* Tablet: 768px+ */
@media (min-width: 768px) {
  .container {
    max-width: 750px;
    margin: 0 auto;
  }
}

/* Desktop: 1024px+ */
@media (min-width: 1024px) {
  .container {
    max-width: 1200px;
    padding: 40px; /* More breathing room on desktop */
  }
}
```

---

### Example 3: Utility Class Documentation

```css
/* ========================================
   Utility Classes

   These classes can be mixed with components
   for layout and spacing adjustments.
   ======================================== */

/* Spacing utilities */
.mt-1 { margin-top: 10px; }
.mt-2 { margin-top: 20px; }
.mt-3 { margin-top: 30px; }

/* Display utilities */
.d-none { display: none; }
.d-block { display: block; }
.d-flex { display: flex; }
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|-----|
| `/* */` Comments | 1+ | 1+ | 1+ | 12+ | 3+ |

**Universal support** - Comments work in all browsers and all CSS versions.

---

## Summary

**Key Takeaways:**
- Use `/* */` for all CSS comments
- Explain WHY, not WHAT
- Document complex logic and browser hacks
- Use TODO/FIXME for future work
- Don't leave dead code - use version control
- Section comments improve organization
- Comments don't affect performance

**Comment Guidelines:**
```css
/* ✅ Good: Explains reasoning */
/* ❌ Bad: States the obvious */
/* 📝 TODO: Future improvements */
/* 🐛 FIXME: Known bugs */
/* 💡 NOTE: Important context */
```

---

**Last Updated:** November 15, 2025
**Category:** Fundamentals
**Difficulty:** Beginner

**Related Topics:**
- [CSS Syntax](syntax.md) - Understanding CSS rules
- [CSS Errors](errors.md) - Debugging stylesheets
- [Best Practices](../13-modern-css/optimization.md) - Writing maintainable CSS
