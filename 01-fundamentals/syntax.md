---
title: CSS Syntax
category: Fundamentals
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Syntax

> **Quick Summary:** CSS syntax defines the structure of CSS rules—how to write selectors, properties, and values correctly. Understanding syntax is essential for writing valid CSS that browsers can interpret.

## Table of Contents
- [Introduction](#introduction)
- [CSS Rule Structure](#css-rule-structure)
- [Selectors](#selectors)
- [Declaration Block](#declaration-block)
- [Properties and Values](#properties-and-values)
- [Comments](#comments)
- [Multiple Rules](#multiple-rules)
- [Common Syntax Errors](#common-syntax-errors)
- [Examples](#examples)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

CSS syntax is the grammar of styling. Just as English has rules for sentences (capitalize first letter, end with period), CSS has rules for style declarations. A single misplaced semicolon or bracket can break your entire stylesheet, turning a beautiful design into chaos.

The good news: CSS syntax is remarkably simple. Every CSS rule follows the same pattern: **select an element, declare what to style, specify how to style it.** Master this pattern once, and you can write any CSS imaginable. The challenge isn't complexity—it's precision. Browsers are unforgiving of typos. `color: blue` works; `colour: blue` doesn't (American spelling required). `margin: 10px;` works; `margin: 10px` without semicolon might work until it doesn't.

Understanding syntax transforms CSS from mysterious code to logical instructions. You'll recognize errors instantly, debug faster, and write cleaner code. Professional developers write syntactically perfect CSS—not because they're perfect, but because they understand the rules.

**Key Concept:** CSS is case-insensitive for properties and values, but precise about punctuation. Missing a `:` or `;` or `}` breaks everything.

---

## CSS Rule Structure

Every CSS rule has two parts: **selector** and **declaration block**.

```css
selector {
  property: value;
}
```

**Visual breakdown:**
```css
h1 {
  ↑ selector (what to style)

  color: blue;
  ↑      ↑  ↑
  |      |  └─ value
  |      └──── colon (required)
  └─────────── property

  font-size: 24px;
             ↑    ↑
             |    └─ semicolon (ends declaration)
             └────── value
}
← closing curly brace (ends declaration block)
```

---

## Selectors

**Purpose:** Targets which HTML elements to style.

**Types:**
```css
/* Element selector */
p {
  color: blue;
}

/* Class selector */
.intro {
  font-size: 18px;
}

/* ID selector */
#header {
  background-color: gray;
}

/* Multiple selectors (comma-separated) */
h1, h2, h3 {
  font-family: Arial;
}

/* Descendant selector */
.container p {
  line-height: 1.6;
}
```

**Rules:**
- Selectors come BEFORE the opening `{`
- Multiple selectors separated by commas
- No punctuation at end of selector (no `;` or `:`)

---

## Declaration Block

**Purpose:** Contains all style declarations for the selector.

**Structure:**
```css
selector {
  /* declarations go here */
}
```

**Rules:**
- Starts with `{` (opening curly brace)
- Ends with `}` (closing curly brace)
- Contains one or more declarations
- Declarations separated by semicolons

**Example:**
```css
.button {
  background-color: blue;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
}
```

---

## Properties and Values

**Format:** `property: value;`

### Property
**What to style** (color, size, spacing, etc.)

```css
.element {
  color: red;        /* text color */
  background: blue;  /* background color */
  font-size: 16px;   /* text size */
  margin: 10px;      /* outer spacing */
}
```

**Rules:**
- Lowercase (convention)
- Followed by `:` (colon)
- Use hyphens for multi-word properties: `font-size`, `background-color`

---

### Value
**How to style** (specific color, size, etc.)

```css
.element {
  color: #3498db;           /* HEX value */
  color: rgb(52, 152, 219); /* RGB value */
  color: blue;              /* keyword value */

  width: 300px;             /* pixel value */
  width: 50%;               /* percentage value */
  width: 100vw;             /* viewport width */

  margin: 10px 20px;        /* multiple values */
}
```

**Rules:**
- Follows `:` (colon)
- Ends with `;` (semicolon)
- Can have multiple values (space-separated)
- Case-insensitive for keywords (`Blue` = `blue` = `BLUE`)

---

### Semicolons

**Critical:** Semicolons separate declarations.

```css
/* CORRECT - semicolons after each declaration */
.element {
  color: blue;
  font-size: 16px;
  margin: 10px;
}

/* WRONG - missing semicolons */
.element {
  color: blue
  font-size: 16px
  margin: 10px
}
/* Browser might guess correctly, but don't rely on it */

/* EXCEPTION - last declaration's semicolon is optional */
.element {
  color: blue;
  font-size: 16px;
  margin: 10px  /* semicolon optional (but recommended) */
}
```

**Best practice:** Always include semicolons—makes adding new properties easier.

---

## Comments

**Purpose:** Document your code, disable rules temporarily.

**Syntax:** `/* comment */`

```css
/* This is a single-line comment */

/*
  This is a
  multi-line comment
  that spans multiple lines
*/

/* Header Styles */
.header {
  background: blue; /* Brand color */
  padding: 20px;
}

/* TODO: Make responsive */
/* .mobile-nav { display: none; } */
```

**Rules:**
- Comments start with `/*`
- Comments end with `*/`
- Can span multiple lines
- Cannot be nested (`/* outer /* inner */ */` breaks)
- NOT like JavaScript/HTML comments (`//` or `<!-- -->`)

---

## Multiple Rules

**Multiple selectors, one rule:**
```css
/* Comma-separated selectors share styles */
h1, h2, h3 {
  font-family: Arial, sans-serif;
  color: #333;
}
```

**Same selector, multiple rules:**
```css
/* Later rules override earlier ones */
p {
  color: blue;
}

p {
  color: red; /* Wins - declared later */
}
/* Result: paragraphs are red */
```

**Specificity matters:**
```css
p {
  color: blue; /* Specificity: 0,0,1 */
}

.intro {
  color: red; /* Specificity: 0,1,0 - higher, wins even if earlier */
}
```

---

## Common Syntax Errors

### 1. Missing Semicolon

```css
/* WRONG */
.element {
  color: blue
  font-size: 16px;
}
/* Browser might combine: color: bluefont-size (breaks) */

/* CORRECT */
.element {
  color: blue;
  font-size: 16px;
}
```

---

### 2. Missing Colon

```css
/* WRONG */
.element {
  color blue;
}

/* CORRECT */
.element {
  color: blue;
}
```

---

### 3. Missing Curly Braces

```css
/* WRONG */
.element
  color: blue;
  font-size: 16px;

/* CORRECT */
.element {
  color: blue;
  font-size: 16px;
}
```

---

### 4. Wrong Property Names

```css
/* WRONG - British spelling */
.element {
  colour: blue;
}

/* CORRECT - American spelling */
.element {
  color: blue;
}

/* WRONG - camelCase */
.element {
  fontSize: 16px;
}

/* CORRECT - kebab-case */
.element {
  font-size: 16px;
}
```

---

### 5. Invalid Values

```css
/* WRONG - invalid unit */
.element {
  width: 300pixels;
}

/* CORRECT */
.element {
  width: 300px;
}

/* WRONG - spaces in values */
.element {
  font-family: Helvetica Neue;
}

/* CORRECT - quotes for multi-word values */
.element {
  font-family: "Helvetica Neue", Arial, sans-serif;
}
```

---

## Examples

### Example 1: Complete CSS Rule

```css
/* Selector: targets <h1> elements */
h1 {
  /* Property: color | Value: #2c3e50 */
  color: #2c3e50;

  /* Property: font-size | Value: 36px */
  font-size: 36px;

  /* Property: font-weight | Value: bold */
  font-weight: bold;

  /* Property: margin-bottom | Value: 20px */
  margin-bottom: 20px;
}
/* Closing brace ends rule */
```

---

### Example 2: Multiple Selectors

```css
/* All headings share these styles */
h1,
h2,
h3,
h4,
h5,
h6 {
  font-family: "Georgia", serif;
  color: #333;
  line-height: 1.2;
}

/* Then h1 gets unique styles */
h1 {
  font-size: 36px;
}

h2 {
  font-size: 28px;
}
```

---

### Example 3: Shorthand vs Longhand

```css
/* Longhand (verbose) */
.element {
  margin-top: 10px;
  margin-right: 20px;
  margin-bottom: 10px;
  margin-left: 20px;
}

/* Shorthand (concise) - same result */
.element {
  margin: 10px 20px; /* top/bottom left/right */
}

/* Even shorter if all sides equal */
.element {
  margin: 10px; /* all sides */
}
```

---

### Example 4: Property Order (Conventional)

```css
/* Common convention: group related properties */
.card {
  /* Positioning */
  position: relative;
  top: 0;
  left: 0;

  /* Display & Box Model */
  display: block;
  width: 300px;
  height: 200px;
  padding: 20px;
  margin: 10px;
  border: 1px solid #ddd;

  /* Typography */
  font-family: Arial, sans-serif;
  font-size: 16px;
  line-height: 1.5;
  color: #333;

  /* Visual */
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
```

**Note:** Property order doesn't affect functionality, but consistency helps readability.

---

## Browser Support

CSS syntax rules are universal across all browsers.

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|----|
| Basic Syntax | 1+ | 1+ | 1+ | 12+ | 3+ |
| Comments | 1+ | 1+ | 1+ | 12+ | 3+ |
| All Selectors | 1+ | 1+ | 1+ | 12+ | 5+ |

**Key Takeaway:** CSS syntax works everywhere. Invalid syntax breaks everywhere.

---

## Best Practices

### ✅ Do This

1. **Always Include Semicolons**
   ```css
   /* Good - easier to add properties */
   .element {
     color: blue;
     font-size: 16px;
   }
   ```

2. **Use Lowercase for Properties**
   ```css
   /* Good - standard convention */
   .element {
     background-color: blue;
     font-size: 16px;
   }
   ```

3. **One Property Per Line**
   ```css
   /* Good - readable */
   .element {
     color: blue;
     font-size: 16px;
     margin: 10px;
   }

   /* Avoid - hard to read */
   .element { color: blue; font-size: 16px; margin: 10px; }
   ```

4. **Indent Declaration Blocks**
   ```css
   /* Good - clear hierarchy */
   .container {
     padding: 20px;
   }

   .container .item {
     margin: 10px;
   }
   ```

5. **Use Comments**
   ```css
   /* Navigation Styles */
   .nav {
     display: flex;
   }

   /* TODO: Make responsive */
   ```

---

### ❌ Avoid This

1. **Don't Omit Semicolons**
   ```css
   /* Bad - risky */
   .element {
     color: blue
     font-size: 16px
   }
   ```

2. **Don't Use Inline Styles (When Possible)**
   ```html
   <!-- Bad - mixes content with presentation -->
   <p style="color: blue; font-size: 16px;">Text</p>

   <!-- Good - separation of concerns -->
   <p class="intro">Text</p>
   ```
   ```css
   .intro {
     color: blue;
     font-size: 16px;
   }
   ```

3. **Don't Misspell Properties**
   ```css
   /* Bad - won't work */
   .element {
     colour: blue;     /* British spelling */
     fontSize: 16px;   /* camelCase */
   }

   /* Good */
   .element {
     color: blue;      /* American spelling */
     font-size: 16px;  /* kebab-case */
   }
   ```

---

## Video Tutorial

**Watch CSS Syntax:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=600s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=600s)

**Timestamps:**
- `10:00` - CSS syntax overview
- `12:30` - Selectors, properties, values
- `15:00` - Common syntax errors
- `18:00` - Comments and best practices

**Resources:**
- [W3Schools - CSS Syntax](https://www.w3schools.com/css/css_syntax.asp)
- [MDN - CSS Syntax](https://developer.mozilla.org/en-US/docs/Web/CSS/Syntax)

---

## Related Topics

**Prerequisites:**
- [CSS Introduction](introduction.md)

**Related:**
- [CSS Selectors](selectors.md)
- [CSS Comments](comments.md)
- [How to Add CSS](how-to-add-css.md)

**Next Steps:**
- [CSS Colors](../02-colors/colors-overview.md)
- [CSS Box Model](../03-box-model/box-model-concept.md)

---

## Practice Exercise

### 🎯 Challenge: Fix Syntax Errors

**Objective:** Identify and fix all syntax errors in the code below.

**Broken Code:**
```css
/* Header Styles
h1
  Color: blue
  font-size: 36px
  margin-bottom 20px;

.intro {
  font-size: 18px
  colour: gray;
}

#main-content
  backgroundColor: white;
  padding: 20px
}

/* Button styles
.button {
  background-color #3498db;
  color: white;
  padding: 10px 20px
  borderRadius: 5px;
}
```

<details>
<summary>Click to reveal solution</summary>

**Fixed Code:**
```css
/* Header Styles */
h1 {
  color: blue; /* Lowercase 'color', added semicolon, added opening brace */
  font-size: 36px;
  margin-bottom: 20px; /* Added colon */
}

.intro {
  font-size: 18px; /* Added semicolon */
  color: gray; /* American spelling 'color' */
}

#main-content {
  background-color: white; /* kebab-case, added opening brace */
  padding: 20px; /* Added semicolon */
}

/* Button styles */
.button {
  background-color: #3498db; /* Added colon */
  color: white;
  padding: 10px 20px; /* Added semicolon */
  border-radius: 5px; /* kebab-case */
}
```

**Errors Fixed:**
1. ✅ Closed comment (`/* Header Styles */`)
2. ✅ Added opening brace after `h1`
3. ✅ Changed `Color` to lowercase `color`
4. ✅ Added semicolon after `blue`
5. ✅ Added colon after `margin-bottom`
6. ✅ Added semicolon after `18px`
7. ✅ Changed `colour` to `color` (American spelling)
8. ✅ Added opening brace after `#main-content`
9. ✅ Changed `backgroundColor` to `background-color` (kebab-case)
10. ✅ Added semicolon after `20px`
11. ✅ Closed comment (`/* Button styles */`)
12. ✅ Added colon after `background-color`
13. ✅ Added semicolon after `20px`
14. ✅ Changed `borderRadius` to `border-radius`

</details>

---

**Last Updated:** November 15, 2025
**Category:** Fundamentals
**Difficulty:** Beginner
