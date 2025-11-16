---
title: CSS Specificity
category: Selectors Advanced
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Specificity

> **Quick Summary:** Specificity determines which CSS rule applies when multiple rules target the same element. It's calculated based on selector types: inline styles (highest), IDs, classes/attributes/pseudo-classes, and elements (lowest).

## Table of Contents
- [Introduction](#introduction)
- [Specificity Hierarchy](#specificity-hierarchy)
- [Calculating Specificity](#calculating-specificity)
- [Specificity Rules](#specificity-rules)
- [Examples](#examples)
- [Common Issues](#common-issues)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

When multiple CSS rules target the same element, **specificity** determines which one wins. Understanding specificity prevents CSS conflicts and reduces need for `!important`.

**Formula:** `(inline, IDs, classes, elements)`

---

## Specificity Hierarchy

From **highest** to **lowest**:

1. **Inline styles** (1,0,0,0)
2. **IDs** (0,1,0,0)
3. **Classes, attributes, pseudo-classes** (0,0,1,0)
4. **Elements, pseudo-elements** (0,0,0,1)
5. **Universal selector `*`** (0,0,0,0)

---

## Calculating Specificity

### Format: (a, b, c, d)

- **a** = Inline styles
- **b** = IDs
- **c** = Classes, attributes, pseudo-classes
- **d** = Elements, pseudo-elements

### Examples

```css
/* (0, 0, 0, 1) - 1 element */
p {
  color: black;
}

/* (0, 0, 1, 0) - 1 class */
.intro {
  color: blue;
}

/* (0, 1, 0, 0) - 1 ID */
#main {
  color: red;
}

/* (1, 0, 0, 0) - Inline style */
<p style="color: green;">Text</p>
```

**Winner:** Inline style (green) has highest specificity.

---

### Complex Selectors

```css
/* (0, 0, 1, 1) - 1 class + 1 element */
div.container {
  color: blue;
}

/* (0, 1, 0, 1) - 1 ID + 1 element */
div#header {
  color: red;
}

/* (0, 1, 1, 0) - 1 ID + 1 class */
#main .content {
  color: green;
}

/* (0, 0, 2, 1) - 2 classes + 1 element */
.container.active p {
  color: purple;
}
```

**Comparison:**
- `(0, 1, 1, 0)` **beats** `(0, 0, 2, 1)` (ID trumps multiple classes)
- `(0, 1, 0, 1)` **beats** `(0, 0, 1, 1)` (ID trumps class)

---

## Specificity Rules

### Rule 1: Count Each Type

```css
/* (0, 0, 1, 3) */
nav ul li a {
  color: blue;
}

/* (0, 0, 1, 1) */
.nav-link {
  color: red; /* WINS (fewer elements doesn't matter) */
}
```

**Why:** Both have 1 class, so we compare next: elements (3 vs 1). But wait—classes are equal, so red wins due to source order.

**Correction:** They're equal in specificity `(0, 0, 1, X)`, so **source order** decides (last rule wins).

Actually, let me recalculate:
- `nav ul li a` = (0, 0, 0, 4) - 4 elements
- `.nav-link` = (0, 0, 1, 0) - 1 class

**Classes beat elements**, so red wins.

---

### Rule 2: IDs Trump Everything (Except Inline)

```css
/* (0, 1, 0, 0) */
#header {
  color: red; /* WINS */
}

/* (0, 0, 10, 10) */
.class1.class2.class3... p span {
  color: blue;
}
```

**1 ID beats any number of classes.**

---

### Rule 3: Source Order (Tiebreaker)

When specificity is **equal**, last rule wins:

```css
.button { color: blue; }   /* (0, 0, 1, 0) */
.button { color: red; }    /* (0, 0, 1, 0) - WINS (last) */
```

---

### Rule 4: !important Overrides (Nuclear Option)

```css
p {
  color: blue !important; /* Highest priority (avoid!) */
}

#main p {
  color: red; /* Ignored */
}
```

---

## Examples

### Example 1: Specificity Battle

```html
<div id="container" class="main">
  <p class="text">Hello</p>
</div>
```

```css
/* (0, 0, 1, 1) */
div.main p {
  color: blue;
}

/* (0, 1, 0, 1) */
#container p {
  color: red; /* WINS - 1 ID beats class */
}

/* (0, 0, 2, 0) */
.main .text {
  color: green;
}
```

**Result:** Text is red (ID has highest specificity).

---

### Example 2: Navigation Styling

```css
/* (0, 0, 0, 3) */
nav ul li {
  color: gray;
}

/* (0, 0, 1, 2) */
nav li.active {
  color: blue; /* WINS - has class */
}

/* (0, 1, 0, 2) */
#main-nav li {
  color: green; /* WINS - has ID */
}
```

---

## Common Issues

### Issue 1: Over-Specific Selectors

```css
/* Too specific (hard to override) */
body div.container ul li a.link {
  color: blue;
}

/* Better */
.nav-link {
  color: blue;
}
```

---

### Issue 2: ID Overuse

```css
/* Avoid */
#header #nav #menu {
  color: blue;
}

/* Better */
.header .nav .menu {
  color: blue;
}
```

---

## Browser Support

| Concept | Chrome | Firefox | Safari | Edge | IE 11 |
|---------|--------|---------|--------|------|-------|
| Specificity Rules | ✅ All | ✅ All | ✅ All | ✅ All | ✅ Full |

---

## Best Practices

### ✅ Do This

1. **Use classes primarily**
   ```css
   .button { }
   ```

2. **Keep specificity low**
   ```css
   /* Good */
   .nav-link { }

   /* Avoid */
   body header nav ul li a { }
   ```

3. **Use BEM methodology**
   ```css
   .block__element--modifier { }
   ```

### ❌ Avoid This

1. **Overusing IDs**
2. **Deep nesting**
3. **!important (except for utilities)**

---

## Related Topics

**Prerequisites:**
- [CSS Selectors](../01-fundamentals/selectors.md)
- [Combinators](combinators.md)

**Next Steps:**
- [!important Rule](important-rule.md)

---

## Navigation

**Previous:** [← Attribute Selectors](attribute-selectors.md)
**Next:** [!important Rule →](important-rule.md)
**Up:** [↑ Back to Selectors Advanced](../README.md#8️⃣-selectors-advanced-6-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Selectors Advanced
**Difficulty:** Intermediate
