---
title: CSS !important Rule
category: Selectors Advanced
order: 6
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS !important Rule

> **Quick Summary:** The `!important` declaration gives a CSS rule the highest priority, overriding all other declarations regardless of specificity. Use sparingly—only for utility classes, third-party overrides, or debugging.

## Table of Contents
- [Introduction](#introduction)
- [Syntax](#syntax)
- [How !important Works](#how-important-works)
- [When to Use !important](#when-to-use-important)
- [When NOT to Use !important](#when-not-to-use-important)
- [Examples](#examples)
- [Overriding !important](#overriding-important)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

`!important` is the **nuclear option** in CSS—it forces a property to take precedence over all other rules. While powerful, it should be used **very sparingly** as it breaks the natural cascade and makes debugging difficult.

**Key Concept:** `!important` beats **all specificity** except another `!important` (then source order decides).

---

## Syntax

```css
selector {
  property: value !important;
}
```

**Examples:**
```css
p {
  color: red !important;
}

.button {
  background: blue !important;
}
```

---

## How !important Works

### Priority Order (Highest to Lowest)

1. **!important in user stylesheet** (accessibility overrides)
2. **!important in author stylesheet** (your CSS)
3. **Normal author styles** (your regular CSS)
4. **Normal user styles**
5. **Browser default styles**

### Example: !important Overrides Specificity

```html
<p id="intro" class="text" style="color: green;">Text</p>
```

```css
/* (0, 0, 0, 1) */
p {
  color: red !important; /* WINS despite low specificity */
}

/* (1, 0, 0, 0) - inline style */
/* Ignored because of !important above */
```

**Result:** Text is red (! important beats inline style).

---

## When to Use !important

### Legitimate Use Cases

#### 1. Utility Classes

```css
.hidden {
  display: none !important;
}

.text-center {
  text-align: center !important;
}

.mt-0 {
  margin-top: 0 !important;
}
```

**Why:** Utilities should always win (Tailwind/Bootstrap pattern).

---

#### 2. Overriding Third-Party CSS

```css
/* Override stubborn plugin styles */
.calendar-widget .date {
  color: blue !important; /* Plugin uses inline styles */
}
```

**Why:** When you can't modify the plugin's code.

---

#### 3. Debugging

```css
* {
  outline: 1px solid red !important; /* Temporarily show all boxes */
}
```

**Why:** Quick visual debugging (remove after).

---

#### 4. Accessibility Overrides

```css
/* User stylesheet for vision impairment */
* {
  font-size: 24px !important;
  color: black !important;
  background: white !important;
}
```

**Why:** User needs trump design.

---

## When NOT to Use !important

### Avoid in These Cases

#### 1. Normal Styling

```css
/* BAD */
.button {
  background: blue !important;
  color: white !important;
}

/* GOOD */
.button {
  background: blue;
  color: white;
}
```

**Why:** Unnecessary and makes future changes harder.

---

#### 2. Fixing Specificity Issues

```css
/* BAD - fighting specificity */
.button {
  color: blue !important;
}

/* GOOD - increase specificity properly */
.nav .button {
  color: blue;
}
```

**Why:** Fix the root cause (specificity), don't mask it.

---

#### 3. Quick Fixes

```css
/* BAD - lazy solution */
#header .nav li a {
  color: red !important; /* "It's not working!" */
}

/* GOOD - understand why it's not working */
#header .nav li a {
  color: red; /* Check specificity, inheritance */
}
```

---

## Examples

### Example 1: Utility Class System

```css
/* Spacing utilities */
.m-0 { margin: 0 !important; }
.mt-1 { margin-top: 0.25rem !important; }
.p-2 { padding: 0.5rem !important; }

/* Display utilities */
.d-none { display: none !important; }
.d-block { display: block !important; }

/* Text utilities */
.text-left { text-align: left !important; }
.text-center { text-align: center !important; }
```

**Usage:**
```html
<div class="card p-2 text-center">
  <!-- Utilities always apply -->
</div>
```

---

### Example 2: Overriding Inline Styles

```html
<!-- Third-party widget with inline styles -->
<div class="widget" style="color: red; font-size: 12px;">Content</div>
```

```css
/* Override inline styles */
.widget {
  color: blue !important;
  font-size: 16px !important;
}
```

---

### Example 3: Debugging Layout

```css
/* Temporary - show all element boundaries */
* {
  outline: 1px solid red !important;
}

/* Temporary - force visibility */
.hidden-element {
  display: block !important;
  opacity: 1 !important;
}
```

---

## Overriding !important

### Only Another !important Wins

```css
/* First !important */
p {
  color: red !important;
}

/* Second !important (later in source = wins) */
p {
  color: blue !important; /* WINS */
}
```

### With Higher Specificity

```css
/* (0, 0, 0, 1) */
p {
  color: red !important;
}

/* (0, 0, 1, 1) - higher specificity */
.text p {
  color: blue !important; /* WINS */
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE 11 |
|----------|--------|---------|--------|------|-------|
| `!important` | All | All | All | All | Full |

---

## Best Practices

### Do This

1. **Use for utility classes only**
   ```css
   .hidden { display: none !important; }
   ```

2. **Document why you used it**
   ```css
   /* !important needed to override plugin inline styles */
   .widget { color: blue !important; }
   ```

3. **Remove after debugging**
   ```css
   /* TODO: Remove after fixing specificity */
   .temp { color: red !important; }
   ```

### Avoid This

1. **Using as a crutch**
2. **Overusing in normal styles**
3. **Fighting !important with more !important**

---

## Related Topics

**Prerequisites:**
- [Specificity](specificity.md)
- [CSS Selectors](../01-fundamentals/selectors.md)

**Next Steps:**
- [Cascade and Inheritance](../01-fundamentals/inheritance.md)

---

## Navigation

**Previous:** [← Specificity](specificity.md)
**Next:** [Tables →](../11-components/tables.md)
**Up:** [↑ Back to Selectors Advanced](../README.md#8️⃣-selectors-advanced-6-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Selectors Advanced
**Difficulty:** Intermediate
