---
title: CSS Errors & Debugging
category: Fundamentals
order: 6
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Errors & Debugging

> **Quick Summary:** CSS is forgiving—invalid code is ignored, not thrown as errors. Learn common mistakes (missing semicolons, typos, specificity issues) and debugging tools (DevTools Inspector, validation) to troubleshoot styling problems.

## Table of Contents
- [Introduction](#introduction)
- [How CSS Handles Errors](#how-css-handles-errors)
- [Common Syntax Errors](#common-syntax-errors)
- [Common Property Errors](#common-property-errors)
- [Debugging Tools](#debugging-tools)
- [Debugging Techniques](#debugging-techniques)
- [Browser Support Issues](#browser-support-issues)
- [Best Practices](#best-practices)

---

## Introduction

CSS doesn't "crash" like JavaScript—browsers silently ignore invalid CSS and continue rendering. This makes CSS forgiving but harder to debug, since you won't get error messages for typos.

**Key Concept:** If your CSS isn't working, the browser is likely **ignoring** it due to syntax errors or specificity issues.

---

## How CSS Handles Errors

**CSS Error Recovery:**
1. Browser encounters invalid syntax
2. **Ignores that declaration** (property: value pair)
3. Continues parsing the rest of the stylesheet
4. **No error messages** in console (usually)

**Example:**
```css
.box {
  color: blue;
  colr: red; /* Typo - ignored */
  padding: 20px; /* This still works */
}
```

Result: Box has blue text and 20px padding. The `colr: red;` line is silently ignored.

---

## Common Syntax Errors

### 1. Missing Semicolon

```css
/* Error - missing semicolon */
.box {
  color: blue
  padding: 20px;
}
/* Result: padding is ignored */

/* Fixed */
.box {
  color: blue;
  padding: 20px;
}
```

### 2. Missing Curly Braces

```css
/* Error - missing closing brace */
.box {
  color: blue;
  padding: 20px;
/* Everything after this is broken */

.card {
  margin: 10px;
}

/* Fixed */
.box {
  color: blue;
  padding: 20px;
}

.card {
  margin: 10px;
}
```

### 3. Wrong Comment Syntax

```css
/* Error - HTML comments don't work in CSS */
.box {
  color: blue; // This doesn't work
  padding: 20px; <!-- This breaks everything -->
}

/* Fixed */
.box {
  color: blue; /* Use this syntax */
  padding: 20px;
}
```

### 4. Quotes Mismatch

```css
/* Error - mismatched quotes */
.box {
  font-family: "Arial;
  content: 'Hello";
}

/* Fixed */
.box {
  font-family: "Arial";
  content: 'Hello';
}
```

### 5. Missing Colon

```css
/* Error - missing colon */
.box {
  color blue;
  padding 20px;
}

/* Fixed */
.box {
  color: blue;
  padding: 20px;
}
```

---

## Common Property Errors

### 1. Typos in Property Names

```css
/* Common typos */
.box {
  colr: blue; /* Should be: color */
  padd: 20px; /* Should be: padding */
  bakground: red; /* Should be: background */
}

/* Fixed */
.box {
  color: blue;
  padding: 20px;
  background: red;
}
```

### 2. Invalid Property Values

```css
/* Invalid values */
.box {
  color: blu; /* Not a valid color name */
  padding: 20; /* Missing unit */
  display: boxes; /* Not a valid display value */
}

/* Fixed */
.box {
  color: blue;
  padding: 20px;
  display: block;
}
```

### 3. Units Missing

```css
/* Missing units */
.box {
  width: 500; /* Ignored - no unit */
  margin: 10; /* Ignored - no unit */
  padding: 0; /* OK - zero doesn't need unit */
}

/* Fixed */
.box {
  width: 500px;
  margin: 10px;
  padding: 0;
}
```

### 4. Wrong Shorthand Order

```css
/* Wrong order for border shorthand */
.box {
  border: red 2px solid; /* Works but unconventional */
}

/* Correct order: width style color */
.box {
  border: 2px solid red;
}
```

---

## Debugging Tools

### 1. Browser DevTools Inspector

**Chrome/Edge/Firefox:**
1. Right-click element → Inspect
2. View **Computed** tab to see applied styles
3. Check for ~~strikethrough~~ styles (overridden)
4. Look for warning icons (invalid values)

**DevTools Tips:**
```
Green checkmark = Valid property
Yellow warning = Invalid value
~~Strikethrough~~ = Overridden by more specific rule
```

### 2. CSS Validation

**W3C CSS Validator:**
- URL: https://jigsaw.w3.org/css-validator/
- Upload your CSS file
- Get detailed error reports

### 3. Console Warnings

Some browsers show CSS warnings:
```
Invalid property value: 'colr: blue'
```

---

## Debugging Techniques

### Technique 1: Isolation Testing

```css
/* Temporarily add bright background to see if CSS is loading */
.problematic-element {
  background: red !important; /* If this works, CSS is loading */
}
```

### Technique 2: Binary Search

Comment out half your CSS to find the problem:
```css
/* .box {
  color: blue;
  padding: 20px;
  margin: 10px;
} */
```

Uncomment line by line until error appears.

### Technique 3: Specificity Check

```css
/* Is your selector specific enough? */
#header .nav .item { /* Specificity: 1-2-0 */
  color: blue;
}

.item { /* Specificity: 0-1-0 - loses */
  color: red; /* This won't apply */
}
```

**Fix:** Increase specificity or use `!important` (last resort)

### Technique 4: Border Box Debugging

```css
/* Add borders to see element boundaries */
* {
  border: 1px solid red !important;
}
```

Remove after debugging.

---

## Browser Support Issues

### Issue: Property Not Supported

```css
/* Example: older browsers don't support CSS Grid */
.container {
  display: grid; /* Ignored in IE11 */
}
```

**Fix:** Use feature detection or fallbacks
```css
.container {
  display: flex; /* Fallback */
  display: grid; /* Modern browsers override */
}
```

### Issue: Vendor Prefixes Needed

```css
/* Might not work in older Safari */
.box {
  user-select: none;
}

/* Add vendor prefixes */
.box {
  -webkit-user-select: none; /* Safari/Chrome */
  -moz-user-select: none; /* Firefox */
  -ms-user-select: none; /* IE/Edge */
  user-select: none; /* Standard */
}
```

---

## Best Practices

### Do This

**1. Use CSS Linters**
```bash
# Install stylelint
npm install stylelint stylelint-config-standard

# Catch errors before deployment
```

**2. Validate Regularly**
- Use W3C CSS Validator
- Check DevTools for warnings
- Test in multiple browsers

**3. Check Specificity**
```css
/* Use DevTools to see which rule wins */
.button { } /* 0-1-0 */
#header .button { } /* 1-1-0 - wins */
```

**4. Use Browser DevTools**
- Inspect computed styles
- Test changes live
- Check cascade order

### Avoid This

**1. Don't Ignore DevTools Warnings**
```css
/* DevTools shows warning - fix it! */
.box {
  colr: blue; /* Invalid property */
}
```

**2. Don't Overuse !important**
```css
/* Bad - makes debugging harder */
.button {
  color: blue !important;
  padding: 10px !important;
}

/* Good - fix specificity instead */
#header .nav .button {
  color: blue;
}
```

**3. Don't Leave Broken CSS**
```css
/* Bad - breaks entire rule */
.box {
  color blue /* Missing colon AND semicolon */
  padding: 20px;
}
```

---

## Common Error Checklist

When CSS isn't working, check:

- [ ] **Syntax:** Semicolons, colons, braces?
- [ ] **Spelling:** Property names correct?
- [ ] **Units:** px, em, rem included?
- [ ] **Values:** Valid for that property?
- [ ] **Specificity:** Selector specific enough?
- [ ] **Loading:** Is CSS file linked correctly?
- [ ] **Cache:** Hard refresh (Ctrl+Shift+R)?
- [ ] **Browser Support:** Property supported?
- [ ] **Comments:** Using `/* */` syntax?
- [ ] **Quotes:** Matching " or ' pairs?

---

## Browser Support

| Tool | Chrome | Firefox | Safari | Edge |
|------|--------|---------|--------|------|
| DevTools Inspector | | | | |
| Console Warnings | | | Limited | |
| Validation Tools | | | | |

---

**Last Updated:** November 15, 2025
**Category:** Fundamentals
**Difficulty:** Beginner

**Related Topics:**
- [CSS Syntax](syntax.md) - Proper CSS structure
- [CSS Comments](comments.md) - Documenting code
- [Browser DevTools](../13-modern-css/optimization.md) - Debugging workflows
