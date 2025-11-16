---
title: CSS Pseudo-Classes
category: Selectors Advanced
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Pseudo-Classes

> **Quick Summary:** Pseudo-classes are keywords added to selectors that specify a special **state** of an element (like `:hover`, `:focus`, `:active`) or its **position** in the DOM (like `:first-child`, `:nth-child`). They enable dynamic styling without JavaScript.

## Table of Contents
- [Introduction](#introduction)
- [Why Pseudo-Classes Matter](#why-pseudo-classes-matter)
- [Syntax and Structure](#syntax-and-structure)
- [User Action Pseudo-Classes](#user-action-pseudo-classes)
- [Structural Pseudo-Classes](#structural-pseudo-classes)
- [Form State Pseudo-Classes](#form-state-pseudo-classes)
- [Advanced Pseudo-Classes](#advanced-pseudo-classes)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

**Pseudo-classes** let you style elements based on conditions that can't be expressed with standard selectors. While regular selectors target elements by their tag, class, or ID, pseudo-classes target elements by their **current state**, **position in the DOM**, or **user interaction**.

Think of pseudo-classes as "if statements" for CSS:
- "If the user hovers over this button..." → `:hover`
- "If this is the first child..." → `:first-child`
- "If this input is required..." → `:required`
- "If this link has been visited..." → `:visited`

Before pseudo-classes, these interactions required JavaScript or multiple CSS classes. Now, CSS handles most UI states natively, making websites more performant and maintainable.

**Key Concept:** Pseudo-classes always start with a **single colon** (`:`) and are added to selectors like this: `selector:pseudo-class { property: value; }`

---

## Why Pseudo-Classes Matter

### 1. **Interactivity Without JavaScript**

**Before (JavaScript-heavy):**
```html
<button onmouseover="this.className='btn-hover'" onmouseout="this.className='btn'">Click Me</button>
```

**With Pseudo-Classes (CSS-only):**
```css
button:hover {
  background-color: #007bff;
  transform: scale(1.05);
}
```

### 2. **Form Validation Feedback**

```css
/* Show green border when input is valid */
input:valid {
  border-color: green;
}

/* Show red border when input is invalid */
input:invalid {
  border-color: red;
}

/* Only show validation styling after user interaction */
input:not(:placeholder-shown):invalid {
  border-color: red;
}
```

### 3. **Zebra Striping Tables (Performance)**

```css
/* Old way: Add classes to every other row in HTML/JS */
/* New way: One CSS rule */
tr:nth-child(even) {
  background-color: #f9f9f9;
}
```

### 4. **Career Relevance**
- **Interview question:** "How do you style hover states?" (`:hover`)
- **Common task:** "Implement keyboard navigation styling" (`:focus`)
- **Accessibility requirement:** "Ensure visible focus indicators" (`:focus-visible`)
- **Framework pattern:** React/Vue use `:nth-child` for list styling

---

## Syntax and Structure

### Basic Syntax

```css
selector:pseudo-class {
  property: value;
}
```

**Examples:**
```css
a:hover { color: red; }           /* Link hover state */
li:first-child { font-weight: bold; }  /* First list item */
input:focus { outline: 2px solid blue; } /* Focused input */
```

### Chaining Multiple Pseudo-Classes

```css
/* Link that's been visited AND is being hovered */
a:visited:hover {
  color: purple;
}

/* First child that's also being hovered */
li:first-child:hover {
  background: #f0f0f0;
}
```

### Combining with Combinators

```css
/* First paragraph after heading on hover */
h2 + p:hover {
  background: yellow;
}

/* First child of all direct children */
nav > ul > li:first-child {
  border-left: none;
}
```

---

## User Action Pseudo-Classes

These respond to user interactions.

### `:hover`
**Triggers:** When mouse pointer is over element.

```css
button:hover {
  background-color: #0056b3;
  cursor: pointer;
}

/* Works on any element */
div:hover {
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
}
```

**Use Case:** Visual feedback for interactive elements.

---

### `:active`
**Triggers:** While element is being clicked (mouse button down).

```css
button:active {
  transform: scale(0.98); /* Pressed-down effect */
  background-color: #004085;
}

a:active {
  color: red; /* Color while clicking */
}
```

**Use Case:** "Pressed" button effect.

---

### `:focus`
**Triggers:** When element receives keyboard focus (tab key) or is clicked.

```css
input:focus {
  outline: 2px solid #007bff;
  border-color: #007bff;
}

/* Remove default outline, add custom focus style */
button:focus {
  outline: none; /* ONLY do this if you add a custom style */
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.3);
}
```

**Accessibility:** ALWAYS provide visible focus indicators for keyboard navigation.

---

### `:focus-visible`
**Triggers:** Like `:focus`, but **only** when focus should be visible (keyboard navigation, not mouse clicks).

```css
/* Only show focus ring for keyboard users, not mouse clicks */
button:focus-visible {
  outline: 2px solid #007bff;
}
```

**Why this is better:** Mouse users don't see focus rings, but keyboard users do (best of both worlds).

---

### `:focus-within`
**Triggers:** When element **or any of its descendants** has focus.

```css
/* Highlight form when any input inside is focused */
form:focus-within {
  background-color: #f9f9f9;
  border-color: #007bff;
}
```

**Use Case:** Highlighting entire form sections during user input.

---

## Structural Pseudo-Classes

These select elements based on their position in the DOM.

### `:first-child` and `:last-child`

```css
/* First item in any list */
li:first-child {
  font-weight: bold;
}

/* Last paragraph in article */
article p:last-child {
  margin-bottom: 0;
}
```

**Example:**
```html
<ul>
  <li>First (bold)</li>
  <li>Middle</li>
  <li>Last</li>
</ul>
```

---

### `:nth-child(n)`

**Most powerful structural selector.** Accepts formulas to select patterns.

```css
/* Every odd row */
tr:nth-child(odd) {
  background: #f9f9f9;
}

/* Every even row */
tr:nth-child(even) {
  background: white;
}

/* Specific number */
li:nth-child(3) {
  color: red; /* Third item */
}

/* Every third element */
div:nth-child(3n) {
  border-left: 3px solid blue;
}

/* Every third element starting from the second */
div:nth-child(3n+2) {
  background: yellow;
}
```

**Formula Pattern:** `an + b`
- `a` = cycle interval
- `b` = offset
- `n` = 0, 1, 2, 3, ... (auto-increments)

**Examples:**
- `2n` → 2, 4, 6, 8... (every even)
- `2n+1` → 1, 3, 5, 7... (every odd)
- `3n` → 3, 6, 9, 12... (every third)
- `5n+2` → 2, 7, 12, 17... (every fifth, starting at 2)

---

### `:nth-of-type(n)`

**Difference from `:nth-child`:** Only counts elements of the **same type**.

```html
<div>
  <p>Paragraph 1</p>
  <div>Not a paragraph</div>
  <p>Paragraph 2</p>
  <p>Paragraph 3</p>
</div>
```

```css
/* Selects "Paragraph 2" (second <p>, ignores <div>) */
p:nth-of-type(2) {
  color: blue;
}

/* Would select the <div> (second CHILD, regardless of type) */
div > :nth-child(2) {
  color: red;
}
```

**Use Case:** When HTML has mixed element types, but you want to style only specific types.

---

### `:first-of-type` and `:last-of-type`

```css
/* First paragraph, even if not first child */
p:first-of-type {
  font-size: 1.2rem;
}

/* Last image in container */
img:last-of-type {
  margin-bottom: 0;
}
```

---

### `:only-child`

**Selects:** Elements that are the **only** child of their parent.

```css
/* If list has only one item, center it */
li:only-child {
  text-align: center;
}
```

**HTML Example:**
```html
<ul>
  <li>Only item (centered)</li>
</ul>

<ul>
  <li>First (not centered)</li>
  <li>Second (not centered)</li>
</ul>
```

---

### `:empty`

**Selects:** Elements with **no children** (including text nodes).

```css
/* Hide empty paragraphs */
p:empty {
  display: none;
}

/* Style placeholder boxes */
div:empty::before {
  content: "No content available";
  color: gray;
}
```

---

## Form State Pseudo-Classes

### `:checked`
**Applies to:** Checkboxes, radio buttons, `<option>` elements.

```css
/* Style checked checkbox label */
input[type="checkbox"]:checked + label {
  font-weight: bold;
  color: green;
}

/* Custom checkbox appearance */
input[type="checkbox"]:checked {
  accent-color: #007bff; /* Modern browsers */
}
```

**Real-World Example (Pure CSS Toggle):**
```html
<input type="checkbox" id="theme-toggle">
<label for="theme-toggle">Dark Mode</label>

<style>
  body {
    background: white;
    color: black;
  }

  #theme-toggle:checked ~ body {
    background: #222;
    color: white;
  }
</style>
```

---

### `:disabled` and `:enabled`

```css
/* Grayed-out disabled inputs */
input:disabled {
  background-color: #e9ecef;
  cursor: not-allowed;
  opacity: 0.6;
}

/* Enabled inputs (most inputs by default) */
input:enabled {
  background-color: white;
}
```

---

### `:required` and `:optional`

```css
/* Add asterisk to required fields */
input:required::after {
  content: " *";
  color: red;
}

/* Style optional fields differently */
input:optional {
  border-left: 3px solid gray;
}
```

---

### `:valid` and `:invalid`

**Works with HTML5 validation attributes (`required`, `pattern`, `type="email"`, etc.).**

```css
/* Green border for valid email */
input[type="email"]:valid {
  border-color: green;
}

/* Red border for invalid email */
input[type="email"]:invalid {
  border-color: red;
}

/* Only show validation AFTER user starts typing */
input:not(:placeholder-shown):invalid {
  border-color: red;
}
```

---

### `:in-range` and `:out-of-range`

**Applies to:** `<input type="number">` with `min` and `max` attributes.

```html
<input type="number" min="1" max="10" value="5">
```

```css
input:in-range {
  border-color: green;
}

input:out-of-range {
  border-color: red;
}
```

---

## Advanced Pseudo-Classes

### `:not(selector)`

**Selects:** Elements that do NOT match the selector inside `()`.

```css
/* All buttons except the disabled ones */
button:not(:disabled) {
  cursor: pointer;
}

/* All list items except the first */
li:not(:first-child) {
  margin-top: 10px;
}

/* All paragraphs except those with class "intro" */
p:not(.intro) {
  font-size: 1rem;
}
```

**Chaining multiple `:not()`:**
```css
/* Elements that are NOT first AND NOT last child */
li:not(:first-child):not(:last-child) {
  border-top: 1px solid #ddd;
  border-bottom: 1px solid #ddd;
}
```

---

### `:is(selector1, selector2)`

**Shorthand** for grouping selectors (reduces repetition).

**Before (repetitive):**
```css
header a:hover,
footer a:hover,
aside a:hover {
  color: red;
}
```

**After (with `:is()`):**
```css
:is(header, footer, aside) a:hover {
  color: red;
}
```

---

### `:where(selector1, selector2)`

**Same as `:is()`, but with ZERO specificity.**

```css
/* Both do the same thing */
:is(header, footer) a { color: blue; }   /* Specificity: 0-1-1 */
:where(header, footer) a { color: blue; } /* Specificity: 0-0-1 */
```

**Use Case:** When you want easy overriding (lower specificity = easier to override).

---

### `:has(selector)` (Parent Selector)

**Selects:** Elements that **contain** the specified selector.

```css
/* Card that HAS an image */
.card:has(img) {
  border: 2px solid blue;
}

/* Form that HAS invalid inputs */
form:has(input:invalid) {
  border-color: red;
}

/* Article that HAS a table */
article:has(table) {
  max-width: 1200px; /* Wider layout for table-heavy content */
}
```

**Why this is revolutionary:** First true "parent selector" in CSS (previously impossible without JavaScript).

---

## Examples

### Example 1: Interactive Navigation Menu

**Scenario:** Style navigation links with hover, active, and current page states.

**HTML:**
```html
<nav>
  <a href="#home" class="current">Home</a>
  <a href="#about">About</a>
  <a href="#services">Services</a>
  <a href="#contact">Contact</a>
</nav>
```

**CSS:**
```css
nav a {
  display: inline-block;
  padding: 10px 20px;
  color: #333;
  text-decoration: none;
  border-bottom: 3px solid transparent;
  transition: all 0.3s ease;
}

/* Hover state */
nav a:hover {
  color: #007bff;
  border-bottom-color: #007bff;
}

/* Active (currently clicking) */
nav a:active {
  transform: translateY(2px);
}

/* Current page */
nav a.current {
  color: #007bff;
  border-bottom-color: #007bff;
  font-weight: bold;
}

/* Focus for keyboard navigation */
nav a:focus-visible {
  outline: 2px solid #007bff;
  outline-offset: 4px;
}

/* First link has no left margin */
nav a:first-child {
  margin-left: 0;
}
```

**Result:** Fully interactive navigation with hover effects, click feedback, focus states, and current page highlighting.

---

### Example 2: Styled Form with Validation

**Scenario:** Create a form that shows real-time validation feedback.

**HTML:**
```html
<form>
  <label for="email">Email (required):</label>
  <input type="email" id="email" required placeholder="you@example.com">

  <label for="age">Age (18-100):</label>
  <input type="number" id="age" min="18" max="100">

  <label for="website">Website (optional):</label>
  <input type="url" id="website" placeholder="https://example.com">

  <button type="submit">Submit</button>
</form>
```

**CSS:**
```css
/* Base input styling */
input {
  display: block;
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  border: 2px solid #ddd;
  border-radius: 4px;
  transition: border-color 0.3s;
}

/* Focus state */
input:focus {
  outline: none;
  border-color: #007bff;
}

/* Required fields get a subtle left border */
input:required {
  border-left: 4px solid #ffc107;
}

/* Valid inputs (green) */
input:valid {
  border-color: #28a745;
}

/* Invalid inputs - ONLY after user starts typing */
input:not(:placeholder-shown):invalid {
  border-color: #dc3545;
}

/* Number input in valid range */
input[type="number"]:in-range {
  border-color: #28a745;
}

/* Number input out of range */
input[type="number"]:out-of-range {
  border-color: #dc3545;
}

/* Disabled submit button if form has invalid inputs */
form:has(input:invalid) button {
  opacity: 0.5;
  cursor: not-allowed;
}
```

**Result:** Form that shows green borders for valid inputs, red for invalid, and disables submit button when validation fails—all without JavaScript.

---

### Example 3: Zebra-Striped Table with Hover

**Scenario:** Create a data table with alternating row colors and hover highlighting.

**HTML:**
```html
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Email</th>
      <th>Role</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>John Doe</td><td>john@example.com</td><td>Developer</td></tr>
    <tr><td>Jane Smith</td><td>jane@example.com</td><td>Designer</td></tr>
    <tr><td>Bob Johnson</td><td>bob@example.com</td><td>Manager</td></tr>
    <tr><td>Alice Williams</td><td>alice@example.com</td><td>Developer</td></tr>
  </tbody>
</table>
```

**CSS:**
```css
table {
  width: 100%;
  border-collapse: collapse;
}

/* Header row */
thead tr {
  background: #007bff;
  color: white;
}

/* Zebra striping (every even row) */
tbody tr:nth-child(even) {
  background: #f9f9f9;
}

/* Hover effect on body rows */
tbody tr:hover {
  background: #e3f2fd;
  cursor: pointer;
}

/* First column is bold */
td:first-child {
  font-weight: bold;
}

/* Last row has no bottom border */
tbody tr:last-child td {
  border-bottom: none;
}
```

**Result:** Professional-looking table with alternating row colors, hover highlighting, and no bottom border on the last row.

---

## Common Use Cases

### Use Case 1: Remove Margin from First/Last Elements
**When:** Preventing unwanted spacing in containers.

**How:**
```css
.container > *:first-child {
  margin-top: 0;
}

.container > *:last-child {
  margin-bottom: 0;
}
```

**Why:** Ensures consistent spacing inside components.

---

### Use Case 2: Style Every Third Item in a Grid
**When:** Creating visual patterns in image galleries, product grids.

**How:**
```css
.grid-item:nth-child(3n+1) {
  background: #f0f0f0;
}
```

**Why:** Adds visual interest without manually adding classes.

---

### Use Case 3: Highlight Form Errors Only After User Interaction
**When:** Avoiding "red error state" on page load.

**How:**
```css
/* Don't show errors until user types */
input:not(:focus):not(:placeholder-shown):invalid {
  border-color: red;
}
```

**Why:** Better UX (errors appear only after user attempts input).

---

### Use Case 4: Custom Checkbox/Radio Styling
**When:** Replacing default browser form controls.

**How:**
```css
input[type="checkbox"] {
  appearance: none;
  width: 20px;
  height: 20px;
  border: 2px solid #007bff;
  border-radius: 4px;
}

input[type="checkbox"]:checked {
  background: #007bff;
}

input[type="checkbox"]:checked::before {
  content: "";
  color: white;
  display: block;
  text-align: center;
  line-height: 20px;
}
```

**Why:** Brand-consistent form controls across all browsers.

---

## Browser Support

| Pseudo-Class | Chrome | Firefox | Safari | Edge | IE 11 |
|--------------|--------|---------|--------|------|-------|
| `:hover`, `:active`, `:focus` | All | All | All | All | Full |
| `:nth-child()`, `:nth-of-type()` | All | All | All | All | Full |
| `:checked`, `:disabled`, `:enabled` | All | All | All | All | Full |
| `:valid`, `:invalid` | All | All | All | All | Full |
| `:focus-visible` | 86+ | 85+ | 15.4+ | 86+ | None |
| `:focus-within` | 60+ | 52+ | 10.1+ | 79+ | None |
| `:is()`, `:where()` | 88+ | 78+ | 14+ | 88+ | None |
| `:has()` | 105+ | 103+ | 15.4+ | 105+ | None |

**Fallback Strategy:**
```css
/* Old browsers */
a:focus {
  outline: 2px solid blue;
}

/* Modern browsers (overrides above if supported) */
a:focus-visible {
  outline: 2px solid blue;
}
```

**Can I Use Links:**
- [`:focus-visible`](https://caniuse.com/css-focus-visible)
- [`:has()`](https://caniuse.com/css-has)

---

## Best Practices

### Do This

1. **Always Provide Focus Styles (Accessibility)**
   ```css
   button:focus-visible {
     outline: 2px solid #007bff;
     outline-offset: 2px;
   }
   ```
   **Why:** Keyboard users need visible focus indicators (WCAG requirement).

2. **Use `:not(:placeholder-shown)` for Form Validation**
   ```css
   input:not(:placeholder-shown):invalid {
     border-color: red;
   }
   ```
   **Why:** Shows errors only after user starts typing (better UX).

3. **Combine Pseudo-Classes for Specificity**
   ```css
   a:visited:hover {
     color: purple; /* Visited links on hover */
   }
   ```
   **Why:** Handles multiple states simultaneously.

4. **Use `:nth-child()` for Patterns**
   ```css
   li:nth-child(odd) { background: #f0f0f0; }
   ```
   **Why:** No need for JavaScript or manual class assignment.

---

### Avoid This

1. **Removing Focus Styles Without Replacement**
   ```css
   /* NEVER do this alone */
   *:focus {
     outline: none;
   }
   ```
   **Why Not:** Makes site unusable for keyboard users.
   **Instead:**
   ```css
   *:focus-visible {
     outline: 2px solid #007bff;
   }
   ```

2. **Using `:hover` on Mobile-Only Elements**
   ```css
   /* Problem: Hover doesn't work on touch screens */
   .mobile-menu:hover {
     display: block;
   }
   ```
   **Instead:** Use `:active` or JavaScript for mobile.

3. **Forgetting `:visited` Link Styling**
   ```css
   /* Only new links styled, visited links look broken */
   a:link { color: blue; }
   ```
   **Instead:**
   ```css
   a:link { color: blue; }
   a:visited { color: purple; }
   ```

---

## Video Tutorial

### CSS Tutorial - Full Course for Beginners

**Watch Section:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=1680s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=1680s)

**Relevant Timestamps:**
- `0:28:00` - Introduction to pseudo-classes
- `0:29:20` - `:hover`, `:active`, `:focus` examples
- `0:32:40` - Structural pseudo-classes (`:nth-child`)
- `0:35:10` - Form pseudo-classes (`:valid`, `:invalid`)
- `0:38:00` - Advanced selectors (`:not`, `:is`)

**What You'll Learn:**
Live coding demonstrations of common pseudo-class patterns, including interactive navigation menus, form validation, and table styling.

**Additional Resources:**
- [W3Schools - CSS Pseudo-Classes](https://www.w3schools.com/css/css_pseudo_classes.asp)
- [MDN Web Docs - Pseudo-Classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
- [CSS-Tricks - Meet the Pseudo Class Selectors](https://css-tricks.com/pseudo-class-selectors/)

---

## Related Topics

**Prerequisites (Learn These First):**
- [CSS Selectors](../01-fundamentals/selectors.md) - Basic selector types
- [Combinators](combinators.md) - Combining selectors for complex targeting

**Related Concepts:**
- [Pseudo-Elements](pseudo-elements.md) - `::before`, `::after` (note the double colon)
- [Specificity](specificity.md) - How pseudo-classes affect selector weight
- [Attribute Selectors](attribute-selectors.md) - Select by HTML attributes

**Next Steps (Learn These Next):**
- [Pseudo-Elements](pseudo-elements.md) - Generate content with CSS
- [Transitions](../09-visual-effects/transitions.md) - Animate pseudo-class state changes

---

## Practice Exercise

### Challenge: Build an Interactive Product Card

**Objective:** Create a product card that uses pseudo-classes for hover effects, focus states, and interactive feedback.

**Requirements:**
- [ ] Card scales up slightly on hover
- [ ] "Add to Cart" button changes color on hover and active states
- [ ] Focus-visible styles for keyboard navigation
- [ ] Sale badge shows only if card has `.on-sale` class (use `:has()` or class selector)
- [ ] First card in a grid has no left margin
- [ ] Bonus: Use `:not()` to style all cards except featured ones

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Product Cards</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="product-grid">
    <div class="card">
      <img src="https://via.placeholder.com/300x200" alt="Product 1">
      <h3>Product 1</h3>
      <p class="price">$29.99</p>
      <button>Add to Cart</button>
    </div>

    <div class="card on-sale">
      <span class="sale-badge">SALE</span>
      <img src="https://via.placeholder.com/300x200" alt="Product 2">
      <h3>Product 2</h3>
      <p class="price">$19.99 <span class="original">$29.99</span></p>
      <button>Add to Cart</button>
    </div>

    <div class="card featured">
      <img src="https://via.placeholder.com/300x200" alt="Product 3">
      <h3>Featured Product</h3>
      <p class="price">$49.99</p>
      <button>Add to Cart</button>
    </div>
  </div>
</body>
</html>
```

**CSS (Complete this):**
```css
/* Your CSS here - use pseudo-classes! */
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**CSS:**
```css
body {
  font-family: Arial, sans-serif;
  padding: 40px;
  background: #f5f5f5;
}

.product-grid {
  display: flex;
  gap: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

/* Base card styles */
.card {
  background: white;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  position: relative;
}

/* Hover effect (scale up) */
.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 16px rgba(0,0,0,0.2);
}

/* First card (no left margin if needed) */
.card:first-child {
  margin-left: 0;
}

/* Image styling */
.card img {
  width: 100%;
  border-radius: 4px;
  margin-bottom: 15px;
}

/* Sale badge (only visible on .on-sale cards) */
.sale-badge {
  display: none;
}

.card.on-sale .sale-badge {
  display: block;
  position: absolute;
  top: 10px;
  right: 10px;
  background: #dc3545;
  color: white;
  padding: 5px 10px;
  border-radius: 4px;
  font-weight: bold;
  font-size: 0.8rem;
}

/* Featured card gets border */
.card.featured {
  border: 2px solid #ffc107;
}

/* All cards except featured (using :not) */
.card:not(.featured) {
  border: 1px solid #ddd;
}

/* Price styling */
.price {
  font-size: 1.5rem;
  font-weight: bold;
  color: #007bff;
  margin: 10px 0;
}

/* Original price (strikethrough) */
.original {
  font-size: 1rem;
  color: #999;
  text-decoration: line-through;
  margin-left: 10px;
}

/* Button base styles */
.card button {
  width: 100%;
  padding: 12px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.3s ease, transform 0.1s ease;
}

/* Button hover */
.card button:hover {
  background: #0056b3;
}

/* Button active (pressed) */
.card button:active {
  transform: scale(0.98);
  background: #004085;
}

/* Button focus (keyboard navigation) */
.card button:focus-visible {
  outline: 2px solid #007bff;
  outline-offset: 2px;
}

/* Disabled button (if needed) */
.card button:disabled {
  background: #ccc;
  cursor: not-allowed;
  opacity: 0.6;
}

.card button:disabled:hover {
  background: #ccc; /* No hover effect when disabled */
}
```

**Explanation:**
- **`.card:hover`**: Scales card up and increases shadow (engagement feedback)
- **`.card:first-child`**: Removes left margin for grid alignment
- **`.card.on-sale .sale-badge`**: Shows badge only on sale items
- **`.card:not(.featured)`**: Applies border to non-featured cards
- **`button:hover`**: Darkens background on hover
- **`button:active`**: Shrinks button slightly when clicked (tactile feedback)
- **`button:focus-visible`**: Shows outline only for keyboard users
- **`button:disabled:hover`**: Prevents hover effect on disabled buttons

</details>

---

### Expected Result

**Visual Outcome:**
- Product cards lift up on hover with enhanced shadow
- "Add to Cart" buttons change color on hover and shrink when clicked
- Sale badge appears only on discounted products
- Featured product has a gold border
- Keyboard navigation shows clear focus indicators

**Key Learnings:**
- Pseudo-classes create interactivity without JavaScript
- Combining multiple pseudo-classes (`:hover`, `:focus-visible`, `:not()`) creates rich interactions
- State-based styling (`:active`, `:disabled`) provides user feedback
- Structural pseudo-classes (`:first-child`) handle layout edge cases

---

## Navigation

**Previous:** [← Combinators](combinators.md)
**Next:** [Pseudo-Elements →](pseudo-elements.md)
**Up:** [↑ Back to Selectors Advanced](../README.md#8️⃣-selectors-advanced-6-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Selectors Advanced
**Difficulty:** Intermediate
