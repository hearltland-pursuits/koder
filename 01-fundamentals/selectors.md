---
title: CSS Selectors
category: Fundamentals
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Selectors

> **Quick Summary:** CSS selectors are patterns that tell the browser which HTML elements to style. They're the targeting system that connects your CSS rules to specific parts of your webpage.

## Table of Contents
- [Introduction](#introduction)
- [Why Selectors Matter](#why-selectors-matter)
- [Basic Selector Types](#basic-selector-types)
- [Element Selector](#element-selector)
- [Class Selector](#class-selector)
- [ID Selector](#id-selector)
- [Universal Selector](#universal-selector)
- [Grouping Selectors](#grouping-selectors)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

Think of CSS selectors as a GPS system for styling. Just as GPS coordinates pinpoint locations on Earth, selectors pinpoint specific elements on your webpage. Want to style all paragraphs? Use the paragraph selector. Want to style just one specific button? Use an ID selector. Want to style multiple elements with similar styles? Use a class selector.

Selectors are the foundation of CSS. Without them, you couldn't apply styles strategically—everything would look the same. Mastering selectors gives you surgical precision: style exactly what you want, when you want, without affecting other elements.

In this guide, we'll cover the **five fundamental selectors** that every CSS developer must know. These form the building blocks for more advanced selectors (combinators, pseudo-classes, attribute selectors) which we'll cover in later sections.

**Key Concept:** Selectors answer the question "What should I style?" Once you know what to target, you can apply any styling you want.

---

## Why Selectors Matter

### 1. **Precision Control**
Selectors let you style specific elements without affecting others:
```css
/* Style ONLY the main heading, not all headings */
h1 { color: blue; }

/* Style ONLY elements with class "alert" */
.alert { background-color: red; }
```

### 2. **Reusability**
Classes let you apply the same styles to multiple elements:
```css
/* Apply to any element with class "btn" */
.btn {
  padding: 12px 24px;
  border-radius: 5px;
}
```

```html
<button class="btn">Click Me</button>
<a href="#" class="btn">Link Button</a>
```

### 3. **Maintainability**
Change styles in one place, update everywhere:
```css
/* Change all buttons site-wide by editing one rule */
.button { background-color: blue; }
```

### 4. **Career Relevance**
Understanding selectors is fundamental for:
- Writing efficient CSS
- Debugging styling issues
- Working with CSS frameworks (Bootstrap, Tailwind)
- JavaScript DOM manipulation (uses same selector syntax)

**85% of front-end job postings require CSS selector knowledge.**

---

## Basic Selector Types

CSS has **five fundamental selectors**:

| Selector | Symbol | Example | Targets |
|----------|--------|---------|---------|
| **Element** | `element` | `p` | All `<p>` tags |
| **Class** | `.classname` | `.intro` | All elements with `class="intro"` |
| **ID** | `#idname` | `#header` | The element with `id="header"` |
| **Universal** | `*` | `*` | All elements |
| **Grouping** | `,` | `h1, h2, h3` | All listed elements |

Let's explore each in detail.

---

## Element Selector

**Syntax:** `element { property: value; }`

**What it does:** Targets all HTML elements of a specific type.

### Example

**HTML:**
```html
<p>First paragraph</p>
<p>Second paragraph</p>
<p>Third paragraph</p>
```

**CSS:**
```css
p {
  color: #333;
  font-size: 16px;
  line-height: 1.6;
}
```

**Result:** All three paragraphs are styled identically.

---

### When to Use Element Selectors

**Good for:**
- Setting base styles for common elements
- Establishing typography defaults
- Resetting default browser styles

```css
/* Good use cases */
body { font-family: Arial, sans-serif; }
h1 { font-size: 32px; }
a { color: blue; text-decoration: none; }
```

**Avoid for:**
- Styling specific instances (use classes instead)
- Complex targeting (use advanced selectors)

---

### Multiple Element Selectors

Each type of element can have its own styles:

```css
h1 {
  font-size: 36px;
  color: #2c3e50;
}

h2 {
  font-size: 28px;
  color: #34495e;
}

p {
  font-size: 16px;
  color: #555;
}
```

---

## Class Selector

**Syntax:** `.classname { property: value; }`

**What it does:** Targets all elements with a specific `class` attribute.

### Example

**HTML:**
```html
<p class="highlight">This paragraph is highlighted.</p>
<p>This paragraph is normal.</p>
<p class="highlight">This paragraph is also highlighted.</p>
```

**CSS:**
```css
.highlight {
  background-color: yellow;
  font-weight: bold;
}
```

**Result:** Only paragraphs with `class="highlight"` get the yellow background and bold text.

---

### Class Naming Conventions

**Best Practices:**
```css
/* Good - descriptive, lowercase, hyphenated */
.main-navigation { }
.btn-primary { }
.error-message { }

/* Bad - unclear, uses underscores or camelCase */
.nav1 { }
.btn_primary { }
.errorMessage { }
```

**Rules:**
- Use lowercase letters
- Separate words with hyphens (`-`)
- Be descriptive
- Avoid abbreviations unless widely understood

---

### Multiple Classes on One Element

HTML elements can have multiple classes:

**HTML:**
```html
<button class="btn btn-large btn-primary">Large Primary Button</button>
```

**CSS:**
```css
.btn {
  padding: 10px 20px;
  border: none;
  cursor: pointer;
}

.btn-large {
  font-size: 20px;
  padding: 15px 30px;
}

.btn-primary {
  background-color: #3498db;
  color: white;
}
```

**Result:** The button gets styles from all three classes combined.

**Why this works:** This is called **composition**—combining small, reusable classes to build complex styles.

---

### When to Use Class Selectors

**Primary use case for styling**

Classes are the **workhorse of CSS**. Use them for:
- Reusable styles
- Component styling
- Styling groups of elements
- Almost everything!

```css
/* Classes for everything */
.card { }
.button { }
.navigation { }
.footer-links { }
```

---

## ID Selector

**Syntax:** `#idname { property: value; }`

**What it does:** Targets the one element with a specific `id` attribute.

### Example

**HTML:**
```html
<header id="main-header">
  <h1>My Website</h1>
</header>
```

**CSS:**
```css
#main-header {
  background-color: #2c3e50;
  color: white;
  padding: 20px;
}
```

**Result:** Only the element with `id="main-header"` is styled.

---

### IDs vs Classes: Critical Differences

| Aspect | ID | Class |
|--------|----|----|
| **Uniqueness** | Must be unique per page | Can be reused |
| **HTML** | `id="name"` | `class="name"` |
| **CSS Symbol** | `#` | `.` |
| **Specificity** | Very high | Medium |
| **Use Case** | Unique elements | Reusable styles |

**HTML Example:**
```html
<!-- ID - can only appear once -->
<div id="main-content">...</div>

<!-- Class - can appear multiple times -->
<div class="sidebar">...</div>
<div class="sidebar">...</div>
<div class="sidebar">...</div>
```

---

### When to Use ID Selectors

**Use sparingly for CSS**

**Good for:**
- JavaScript targeting
- URL anchors (`<a href="#section1">`)
- Unique page landmarks (header, footer, main content)

**Avoid for:**
- General styling (use classes instead)
- Anything you might want to reuse

**Why?** IDs have very high specificity, making them hard to override. This leads to messy CSS.

```css
/* Overly specific - hard to override later */
#header #navigation .menu-item { }

/* Better - flexible, reusable */
.nav-item { }
```

---

## Universal Selector

**Syntax:** `* { property: value; }`

**What it does:** Targets **every single element** on the page.

### Example

**CSS:**
```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

**Result:** All elements have margin and padding removed, and `box-sizing` set to `border-box`.

---

### Common Use Case: CSS Reset

The universal selector is commonly used to reset default browser styles:

```css
/* Basic CSS Reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

**What this does:**
- Removes default margins/padding (browsers add these automatically)
- Sets `box-sizing: border-box` (makes width calculations easier)

**Performance Note:** The universal selector has no negative performance impact in modern browsers.

---

### When to Use Universal Selector

**Good for:**
- CSS resets
- Applying `box-sizing` globally
- Setting base font properties

**Avoid for:**
- Specific styling (too broad)
- Performance-critical animations (use specific selectors)

---

## Grouping Selectors

**Syntax:** `selector1, selector2, selector3 { property: value; }`

**What it does:** Applies the same styles to multiple selectors.

### Example

**Without Grouping (Repetitive):**
```css
h1 {
  font-family: Arial, sans-serif;
  color: #2c3e50;
}

h2 {
  font-family: Arial, sans-serif;
  color: #2c3e50;
}

h3 {
  font-family: Arial, sans-serif;
  color: #2c3e50;
}
```

**With Grouping (DRY - Don't Repeat Yourself):**
```css
h1, h2, h3 {
  font-family: Arial, sans-serif;
  color: #2c3e50;
}
```

**Result:** All three heading types get the same font and color.

---

### Grouping Different Selector Types

You can group any combination of selectors:

```css
/* Elements + Classes + IDs */
h1,
.page-title,
#main-heading {
  font-size: 32px;
  margin-bottom: 20px;
}
```

**Formatting Tip:** Put each selector on its own line for readability (especially with many selectors).

---

### When to Use Grouping

**Perfect for:**
- Shared base styles
- Reducing repetition
- Keeping CSS DRY (Don't Repeat Yourself)

```css
/* All buttons share base styles */
.btn-primary,
.btn-secondary,
.btn-danger {
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

/* Then add unique colors separately */
.btn-primary { background-color: blue; }
.btn-secondary { background-color: gray; }
.btn-danger { background-color: red; }
```

---

## Examples

### Example 1: Building a Simple Card Component

**Scenario:** Create a reusable card design for blog posts, products, or profiles.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Card Component</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="card">
    <h2>Card Title</h2>
    <p>This is a simple card component with some descriptive text.</p>
    <button class="btn">Learn More</button>
  </div>

  <div class="card">
    <h2>Another Card</h2>
    <p>Cards are reusable because we're using classes!</p>
    <button class="btn">Read More</button>
  </div>
</body>
</html>
```

**CSS:**
```css
/* Reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background-color: #f0f0f0;
  padding: 40px;
}

/* Card Component */
.card {
  background-color: white;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.card h2 {
  color: #2c3e50;
  margin-bottom: 12px;
}

.card p {
  color: #555;
  line-height: 1.6;
  margin-bottom: 16px;
}

/* Button */
.btn {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
}

.btn:hover {
  background-color: #2980b9;
}
```

**Result:** Two identical styled cards with white background, shadows, and blue buttons.

**Key Learnings:**
- Class selector (`.card`) makes the design reusable
- Element selectors inside class (`.card h2`) target specific parts
- `:hover` pseudo-class adds interactivity

---

### Example 2: Navigation Menu with Multiple Selector Types

**Scenario:** Create a horizontal navigation bar using element, class, and grouping selectors.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Navigation Example</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <nav id="main-nav">
    <ul>
      <li><a href="#" class="active">Home</a></li>
      <li><a href="#">About</a></li>
      <li><a href="#">Services</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>
</body>
</html>
```

**CSS:**
```css
/* Universal Reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
}

/* ID Selector - Unique navigation bar */
#main-nav {
  background-color: #2c3e50;
  padding: 1rem;
}

/* Element Selector - Remove list styling */
#main-nav ul {
  list-style: none;
  display: flex;
  gap: 2rem;
}

/* Element Selector - Style list items */
#main-nav li {
  display: inline;
}

/* Element Selector - Style all links */
#main-nav a {
  color: white;
  text-decoration: none;
  font-size: 18px;
  transition: color 0.3s;
}

/* Pseudo-class - Hover effect */
#main-nav a:hover {
  color: #3498db;
}

/* Class Selector - Active link */
#main-nav .active {
  color: #3498db;
  font-weight: bold;
}
```

**Result:** Professional dark navigation bar with:
- Horizontal layout
- White text links
- Blue hover effect
- Active link highlighted in blue

---

### Example 3: Typography System with Grouping

**Scenario:** Create consistent typography across all headings and text.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Typography Example</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>Main Heading (H1)</h1>
  <p class="lead">This is a lead paragraph with larger text.</p>

  <h2>Subheading (H2)</h2>
  <p>Regular paragraph text goes here.</p>

  <h3>Section Heading (H3)</h3>
  <p class="small-text">Small print or footnotes use this style.</p>
</body>
</html>
```

**CSS:**
```css
/* Universal Reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Georgia, serif;
  line-height: 1.6;
  color: #333;
  padding: 40px;
  max-width: 800px;
  margin: 0 auto;
}

/* Grouping Selector - All headings */
h1, h2, h3, h4, h5, h6 {
  font-family: Arial, sans-serif;
  color: #2c3e50;
  margin-bottom: 16px;
  line-height: 1.2;
}

/* Individual Heading Sizes */
h1 { font-size: 36px; }
h2 { font-size: 28px; }
h3 { font-size: 22px; }

/* Element Selector - Paragraphs */
p {
  margin-bottom: 20px;
}

/* Class Selector - Lead Paragraph */
.lead {
  font-size: 20px;
  font-weight: 300;
  color: #555;
}

/* Class Selector - Small Text */
.small-text {
  font-size: 14px;
  color: #777;
}
```

**Result:** Consistent, professional typography with:
- All headings share base styles (grouping selector)
- Each heading has appropriate size
- Special paragraph styles (`.lead`, `.small-text`)

---

## Common Use Cases

### Use Case 1: Styling All Buttons Consistently

**When:** You have multiple buttons throughout your site and want them to look identical.

**How:**
```css
.btn {
  background-color: #3498db;
  color: white;
  padding: 12px 24px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}
```

**HTML:**
```html
<button class="btn">Submit</button>
<a href="#" class="btn">Link Button</a>
<input type="submit" class="btn" value="Send">
```

**Why:** Class selector (`.btn`) works on any element—button, link, or input.

---

### Use Case 2: Resetting Browser Defaults

**When:** Browsers add default margins, padding, and styling that you want to remove.

**How:**
```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

**Why:** Universal selector (`*`) targets everything, creating a clean slate.

---

### Use Case 3: Highlighting Active Navigation Item

**When:** You want to show users which page they're currently on.

**How:**
```css
.nav-item {
  color: white;
}

.nav-item.active {
  color: #3498db;
  font-weight: bold;
}
```

**HTML:**
```html
<nav>
  <a href="#" class="nav-item active">Home</a>
  <a href="#" class="nav-item">About</a>
  <a href="#" class="nav-item">Contact</a>
</nav>
```

**Why:** Class selector (`.active`) can be moved to any navigation item dynamically (often with JavaScript).

---

## Browser Support

All basic selectors have been supported since the earliest browsers.

| Selector | Chrome | Firefox | Safari | Edge | IE |
|----------|--------|---------|--------|------|----|
| Element | 1+ | 1+ | 1+ | 12+ | 3+ |
| Class | 1+ | 1+ | 1+ | 12+ | 3+ |
| ID | 1+ | 1+ | 1+ | 12+ | 3+ |
| Universal | 1+ | 1+ | 1+ | 12+ | 7+ |
| Grouping | 1+ | 1+ | 1+ | 12+ | 3+ |

**Key Takeaway:** Basic selectors work everywhere. No compatibility concerns.

---

## Best Practices

### Do This

1. **Prefer Classes for Styling**
   ```css
   /* Good - reusable */
   .button { background-color: blue; }

   /* Avoid - not reusable */
   #submit-button { background-color: blue; }
   ```
   **Why:** Classes are flexible and reusable.

2. **Use Semantic Class Names**
   ```css
   /* Good - describes purpose */
   .error-message { color: red; }
   .success-message { color: green; }

   /* Bad - describes appearance */
   .red-text { color: red; }
   .green-text { color: green; }
   ```
   **Why:** Purpose-based names remain meaningful even if design changes.

3. **Group Related Selectors**
   ```css
   /* Good - DRY principle */
   h1, h2, h3 {
     font-family: Arial, sans-serif;
   }

   /* Bad - repetitive */
   h1 { font-family: Arial, sans-serif; }
   h2 { font-family: Arial, sans-serif; }
   h3 { font-family: Arial, sans-serif; }
   ```

4. **Use Element Selectors for Base Styles**
   ```css
   /* Good - sets defaults for all paragraphs */
   p {
     line-height: 1.6;
     margin-bottom: 1rem;
   }
   ```

---

### Avoid This

1. **Don't Overuse IDs for Styling**
   ```css
   /* Bad - creates specificity issues */
   #header { background: blue; }
   #navigation { font-size: 16px; }

   /* Good - use classes */
   .header { background: blue; }
   .navigation { font-size: 16px; }
   ```
   **Why:** IDs have very high specificity and can't be reused.

2. **Don't Use Overly Generic Class Names**
   ```css
   /* Bad - unclear */
   .box { }
   .item { }
   .thing { }

   /* Good - descriptive */
   .product-card { }
   .menu-item { }
   .user-profile { }
   ```

3. **Don't Forget Universal Selector Performance (In Specific Cases)**
   ```css
   /* Bad - in large, complex pages */
   * { transition: all 0.3s; }

   /* Good - target specific elements */
   a, button { transition: all 0.3s; }
   ```
   **Why:** Applying transitions to everything can slow animations.

---

## Video Tutorial

### CSS Tutorial - Full Course for Beginners

**Watch Selectors Section:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=1200s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=1200s)

**Relevant Timestamps:**
- `20:00` - Introduction to selectors
- `25:15` - Element selectors
- `30:45` - Class selectors
- `35:20` - ID selectors
- `40:00` - Practical selector examples

**What You'll Learn:**
This section covers all basic CSS selectors with live coding examples. You'll see how to target elements, apply classes, and use IDs effectively in real projects.

**Additional Resources:**
- [W3Schools - CSS Selectors](https://www.w3schools.com/css/css_selectors.asp)
- [MDN Web Docs - CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [CSS Selector Tester](https://www.w3schools.com/cssref/trysel.php) - Interactive tool

---

## Related Topics

**Prerequisites (Learn These First):**
- [CSS Introduction](introduction.md) - Understanding CSS basics before selectors

**Related Concepts:**
- [CSS Syntax](syntax.md) - How CSS rules are structured
- [Combinators](../08-selectors-advanced/combinators.md) - Advanced targeting (child, descendant, sibling)
- [Pseudo-Classes](../08-selectors-advanced/pseudo-classes.md) - :hover, :focus, :nth-child
- [Specificity](../08-selectors-advanced/specificity.md) - How CSS decides which rules win

**Next Steps (Learn These Next):**
- [CSS Colors](../02-colors/colors-overview.md) - Applying colors to selected elements
- [CSS Box Model](../03-box-model/box-model-concept.md) - Styling layout properties

---

## Practice Exercise

### Challenge: Build a Product Card with Multiple Selectors

**Objective:** Create a product card using element, class, and grouping selectors to practice targeting elements.

**Requirements:**
- [ ] Use class selector for the card container
- [ ] Use element selectors for heading and paragraph
- [ ] Use grouping selector for multiple button styles
- [ ] Add a class for the "featured" product (different styling)
- [ ] **Bonus:** Use universal selector for a CSS reset

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Product Cards</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="product-card">
    <h2>Basic Product</h2>
    <p class="price">$29.99</p>
    <p class="description">A great product for everyday use.</p>
    <button class="btn btn-primary">Add to Cart</button>
  </div>

  <div class="product-card featured">
    <h2>Featured Product</h2>
    <p class="price">$49.99</p>
    <p class="description">Our best-selling product with premium features.</p>
    <button class="btn btn-primary">Add to Cart</button>
  </div>
</body>
</html>
```

**CSS (Complete this):**
```css
/* Your CSS here */
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**CSS:**
```css
/* Universal Selector - CSS Reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  padding: 40px;
}

/* Class Selector - Product Card */
.product-card {
  background-color: white;
  border-radius: 8px;
  padding: 24px;
  margin-bottom: 20px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  max-width: 400px;
}

/* Element Selectors within Card */
.product-card h2 {
  color: #2c3e50;
  font-size: 24px;
  margin-bottom: 12px;
}

.product-card .price {
  color: #27ae60; /* Green for price */
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 12px;
}

.product-card .description {
  color: #555;
  line-height: 1.6;
  margin-bottom: 20px;
}

/* Grouping Selector - All Buttons */
.btn,
button {
  padding: 12px 24px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

/* Class Selector - Primary Button */
.btn-primary {
  background-color: #3498db;
  color: white;
}

.btn-primary:hover {
  background-color: #2980b9;
}

/* Class Selector - Featured Product (Special Styling) */
.product-card.featured {
  border: 3px solid #f39c12; /* Gold border */
  background-color: #fffbf0; /* Cream background */
}

.product-card.featured h2 {
  color: #f39c12; /* Gold heading */
}
```

**Explanation:**
This solution demonstrates all five basic selectors:

1. **Universal Selector (`*`):** Resets default browser styles
2. **Element Selectors (`h2`, `p`, `button`):** Targets all instances of those elements
3. **Class Selectors (`.product-card`, `.btn`):** Creates reusable component styles
4. **Grouping Selector (`.btn, button`):** Applies shared button styles
5. **Combined Class Selector (`.product-card.featured`):** Targets elements with both classes

The featured product has:
- Gold border and cream background
- Gold heading color
- All other styles inherited from base `.product-card` class

**Key Concept:** Combining classes (`.product-card.featured`) lets you create variations without repeating code.

</details>

---

### Expected Result

**Visual Outcome:**
- Two product cards side-by-side (or stacked on mobile)
- Basic card: white background, blue button
- Featured card: gold border, cream background, gold heading

**Key Learnings:**
- Using class selectors for component-based styling
- Element selectors for consistent typography
- Grouping selectors to reduce repetition
- Combining classes for variations (`.featured`)

---

## Navigation

**Previous:** [← CSS Syntax](syntax.md)
**Next:** [How to Add CSS →](how-to-add-css.md)
**Up:** [↑ Back to Fundamentals](../)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Fundamentals
**Difficulty:** Beginner
