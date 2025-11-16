---
title: CSS Pseudo-Elements
category: Selectors Advanced
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Pseudo-Elements

> **Quick Summary:** Pseudo-elements let you style **specific parts** of an element (like the first letter or first line) or **insert content** before/after elements using `::before` and `::after`. They use double colons (`::`) to distinguish from pseudo-classes (`:`).

## Table of Contents
- [Introduction](#introduction)
- [Why Pseudo-Elements Matter](#why-pseudo-elements-matter)
- [Syntax: Double Colon (::) vs Single Colon (:)](#syntax-double-colon--vs-single-colon-)
- [Core Pseudo-Elements](#core-pseudo-elements)
- [::before and ::after](#before-and-after)
- [::first-letter and ::first-line](#first-letter-and-first-line)
- [::selection](#selection)
- [::placeholder](#placeholder)
- [::marker](#marker)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

While **pseudo-classes** (`:hover`, `:focus`) target elements based on their **state**, **pseudo-elements** (`::before`, `::after`) target **specific parts** of elements or let you **insert generated content** into the DOM without changing HTML.

Think of pseudo-elements as virtual elements that CSS creates:
- `::before` → Insert content **before** element's content
- `::after` → Insert content **after** element's content
- `::first-letter` → Style **only the first letter** of a block
- `::first-line` → Style **only the first line** of text
- `::selection` → Style text when user highlights it

Before pseudo-elements, you'd need extra HTML markup (`<span>` tags) or JavaScript to achieve these effects. Now, CSS handles it natively, keeping HTML semantic and clean.

**Key Concept:** Pseudo-elements are **not real DOM elements**—they exist only in the CSS layer. Inspecting the page won't show `::before` or `::after` in the HTML source, but browser DevTools will show them in the "Elements" tab.

---

## Why Pseudo-Elements Matter

### 1. **Cleaner HTML (No Extra Markup)**

**Without Pseudo-Elements (messy HTML):**
```html
<blockquote>
  <span class="quote-icon">"</span>
  This is a quote.
  <span class="quote-icon">"</span>
</blockquote>
```

**With Pseudo-Elements (clean HTML):**
```html
<blockquote>This is a quote.</blockquote>
```

```css
blockquote::before {
  content: """; /* Left quote mark */
}

blockquote::after {
  content: """; /* Right quote mark */
}
```

### 2. **Decorative Elements Without Images**

```css
/* Create a ribbon banner with CSS */
.badge::before {
  content: "NEW";
  background: red;
  color: white;
  padding: 5px 10px;
  position: absolute;
  top: 10px;
  right: -10px;
}
```

### 3. **Typography Effects**

```css
/* Drop cap (first letter larger) */
article p:first-of-type::first-letter {
  font-size: 3rem;
  float: left;
  line-height: 1;
  margin-right: 10px;
  color: #007bff;
}
```

### 4. **Career Relevance**
- **Interview question:** "How do you add decorative elements without JavaScript?"
- **Framework pattern:** Component libraries (Bootstrap, Material-UI) use `::before`/`::after` extensively
- **Common task:** "Add icons to buttons without `<img>` tags"
- **Accessibility skill:** Knowing when to use pseudo-elements vs real HTML (SEO/screen readers)

---

## Syntax: Double Colon (::) vs Single Colon (:)

### Modern Syntax (CSS3)

```css
/* Correct syntax */
element::before { content: "..."; }
element::after { content: "..."; }
element::first-letter { font-size: 2rem; }
```

**Use double colons (`::`)** for pseudo-elements to distinguish them from pseudo-classes.

### Legacy Syntax (CSS2)

```css
/* Old syntax (still works for backward compatibility) */
element:before { content: "..."; }
element:after { content: "..."; }
```

**Recommendation:** Use **double colons (`::`)** for clarity and modern standards.

**Why it matters:** `:hover` (state) vs `::before` (element part)—double colons clarify intent.

---

## Core Pseudo-Elements

| Pseudo-Element | Purpose | Example |
|----------------|---------|---------|
| `::before` | Insert content **before** element | `button::before { content: "→ "; }` |
| `::after` | Insert content **after** element | `a::after { content: " ↗"; }` |
| `::first-letter` | Style first letter of block | `p::first-letter { font-size: 2rem; }` |
| `::first-line` | Style first line of block | `p::first-line { font-weight: bold; }` |
| `::selection` | Style highlighted text | `::selection { background: yellow; }` |
| `::placeholder` | Style input placeholder text | `input::placeholder { color: gray; }` |
| `::marker` | Style list item markers | `li::marker { color: red; }` |

---

## ::before and ::after

**Most powerful pseudo-elements.** Used to insert generated content before or after an element's content.

### Basic Syntax

```css
element::before {
  content: "Text or icon"; /* REQUIRED property */
  /* Other styles */
}

element::after {
  content: "Text or icon"; /* REQUIRED property */
  /* Other styles */
}
```

**Critical Rule:** `content` property is **REQUIRED**, even if empty (`content: "";`). Without it, `::before`/`::after` won't render.

---

### Example 1: Adding Icons to Links

```css
/* External link icon */
a[href^="http"]::after {
  content: " ↗";
  font-size: 0.8rem;
  color: #007bff;
}

/* PDF link icon */
a[href$=".pdf"]::before {
  content: " ";
}
```

**HTML:**
```html
<a href="https://example.com">External Link</a> <!-- Shows ↗ after -->
<a href="/document.pdf">Download PDF</a> <!-- Shows  before -->
```

**Result:**
- "External Link ↗"
- " Download PDF"

---

### Example 2: Creating Shapes (Triangles, Arrows)

```css
/* Triangle tooltip arrow */
.tooltip::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border: 5px solid transparent;
  border-top-color: black; /* Creates downward triangle */
}
```

**Visual:**
```
┌─────────┐
│ Tooltip │
└─────┬───┘
      ▼ (::after element)
```

---

### Example 3: Decorative Quotation Marks

```css
blockquote {
  position: relative;
  padding: 20px;
  font-style: italic;
}

blockquote::before {
  content: """;
  font-size: 4rem;
  position: absolute;
  top: -10px;
  left: -10px;
  color: #ccc;
  line-height: 1;
}

blockquote::after {
  content: """;
  font-size: 4rem;
  position: absolute;
  bottom: -40px;
  right: 10px;
  color: #ccc;
  line-height: 1;
}
```

**Result:** Fancy quotation marks without extra HTML.

---

### Example 4: Clearfix (Fixing Float Collapse)

```css
/* Old-school clearfix hack */
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

**Why this works:** Forces parent to contain floated children (prevents collapse).

---

### Example 5: Counter (Numbered List Alternative)

```css
/* Custom numbered list */
.custom-list {
  counter-reset: item;
  list-style: none;
}

.custom-list li {
  counter-increment: item;
}

.custom-list li::before {
  content: counter(item) ". ";
  font-weight: bold;
  color: #007bff;
  margin-right: 10px;
}
```

**HTML:**
```html
<ul class="custom-list">
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
</ul>
```

**Result:**
```
1. First item
2. Second item
3. Third item
```

---

## ::first-letter and ::first-line

### ::first-letter

**Styles only the first letter** of a block-level element.

```css
/* Drop cap effect */
article p:first-of-type::first-letter {
  font-size: 3rem;
  font-weight: bold;
  float: left;
  line-height: 1;
  margin-right: 10px;
  color: #007bff;
}
```

**HTML:**
```html
<article>
  <p>This paragraph will have a large first letter.</p>
</article>
```

**Result:**
```
T his paragraph will have
  a large first letter.
```
(T is 3x larger and floated)

**Allowed Properties:**
- Font properties (`font-size`, `font-weight`, etc.)
- Color properties
- Background properties
- Text decorations
- Margins, padding (limited)

---

### ::first-line

**Styles only the first line** of a block-level element (dynamically adjusts as viewport resizes).

```css
p::first-line {
  font-weight: bold;
  color: #333;
  text-transform: uppercase;
}
```

**HTML:**
```html
<p>This is the first line that will be bold and uppercase.
This is the second line, which will be normal styling.</p>
```

**Result:**
```
THIS IS THE FIRST LINE THAT WILL BE BOLD AND UPPERCASE.
This is the second line, which will be normal styling.
```

**Note:** First line changes dynamically based on viewport width (responsive behavior).

---

## ::selection

**Styles text when user highlights it** (drag selection).

```css
/* Default browser selection: blue background, white text */
::selection {
  background: #007bff;
  color: white;
}

/* Firefox prefix (older versions) */
::-moz-selection {
  background: #007bff;
  color: white;
}
```

**Allowed Properties:**
- `color`
- `background-color`
- `text-shadow`
- `text-decoration`

**Use Case:** Brand-consistent highlighting (matching company colors).

---

## ::placeholder

**Styles placeholder text** in form inputs.

```css
input::placeholder {
  color: #999;
  font-style: italic;
  opacity: 0.7;
}

/* Focus state */
input:focus::placeholder {
  color: transparent; /* Hide placeholder on focus */
}
```

**HTML:**
```html
<input type="text" placeholder="Enter your name...">
```

**Result:** Gray, italic placeholder text that disappears when input is focused.

**Browser Prefixes (older browsers):**
```css
input::-webkit-input-placeholder { color: #999; } /* Chrome/Safari */
input::-moz-placeholder { color: #999; } /* Firefox */
input:-ms-input-placeholder { color: #999; } /* IE 10-11 */
```

---

## ::marker

**Styles list item markers** (bullets, numbers).

```css
li::marker {
  color: #007bff;
  font-weight: bold;
  font-size: 1.2rem;
}

/* Custom bullet character */
ul li::marker {
  content: "";
}
```

**HTML:**
```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

**Result:**
```
Item 1
Item 2
```

**Allowed Properties:**
- `color`
- `font` properties
- `content`

**Browser Support:** Chrome 86+, Firefox 68+, Safari 11.1+

---

## Examples

### Example 1: Fancy Button with Icon

**Scenario:** Add a right arrow to all buttons without changing HTML.

**HTML:**
```html
<button class="cta-button">Get Started</button>
```

**CSS:**
```css
.cta-button {
  background: #007bff;
  color: white;
  padding: 12px 40px 12px 20px;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  position: relative;
}

.cta-button::after {
  content: "→";
  position: absolute;
  right: 15px;
  top: 50%;
  transform: translateY(-50%);
  transition: right 0.3s ease;
}

.cta-button:hover::after {
  right: 10px; /* Arrow moves right on hover */
}
```

**Result:** Button displays "Get Started →" with animated arrow on hover.

---

### Example 2: Required Field Asterisk

**Scenario:** Automatically add red asterisks to required form fields.

**HTML:**
```html
<form>
  <label for="name">Name</label>
  <input type="text" id="name" required>

  <label for="email">Email</label>
  <input type="email" id="email" required>
</form>
```

**CSS:**
```css
/* Add asterisk to labels of required inputs */
input:required + label::after,
label:has(+ input:required)::after {
  content: " *";
  color: red;
  font-weight: bold;
}
```

**Result:**
```
Name *
[input field]

Email *
[input field]
```

---

### Example 3: Ribbon Badge

**Scenario:** Create a "NEW" badge on product cards.

**HTML:**
```html
<div class="product-card new">
  <img src="product.jpg" alt="Product">
  <h3>Amazing Product</h3>
  <p>$29.99</p>
</div>
```

**CSS:**
```css
.product-card {
  position: relative;
  border: 1px solid #ddd;
  padding: 20px;
  overflow: hidden; /* Clips ribbon overflow */
}

.product-card.new::before {
  content: "NEW";
  position: absolute;
  top: 10px;
  right: -30px;
  background: #dc3545;
  color: white;
  padding: 5px 40px;
  transform: rotate(45deg);
  font-size: 0.8rem;
  font-weight: bold;
  box-shadow: 0 2px 5px rgba(0,0,0,0.3);
}
```

**Result:** Diagonal "NEW" ribbon in top-right corner.

---

### Example 4: Loading Dots Animation

**Scenario:** Create animated loading dots without images.

**HTML:**
```html
<div class="loading">Loading</div>
```

**CSS:**
```css
.loading::after {
  content: "";
  animation: dots 1.5s steps(4, end) infinite;
}

@keyframes dots {
  0% { content: ""; }
  25% { content: "."; }
  50% { content: ".."; }
  75% { content: "..."; }
  100% { content: ""; }
}
```

**Result:** "Loading", "Loading.", "Loading..", "Loading..." (cycling animation)

---

### Example 5: Breadcrumb Separators

**Scenario:** Add separators between breadcrumb links.

**HTML:**
```html
<nav class="breadcrumb">
  <a href="/">Home</a>
  <a href="/category">Category</a>
  <a href="/subcategory">Subcategory</a>
  <span>Current Page</span>
</nav>
```

**CSS:**
```css
.breadcrumb a::after {
  content: " / ";
  color: #999;
  margin: 0 10px;
}

/* No separator after last item */
.breadcrumb a:last-of-type::after,
.breadcrumb span::after {
  content: "";
}
```

**Result:** Home / Category / Subcategory / Current Page

---

## Common Use Cases

### Use Case 1: Icon Before/After Text
**When:** Adding icons to buttons, links, labels without images.

**How:**
```css
.download-link::before {
  content: "⬇ ";
}

.external-link::after {
  content: " ↗";
}
```

**Why:** No need for `<img>` tags or icon fonts in HTML.

---

### Use Case 2: Clearfix for Floated Elements
**When:** Parent container collapses because children are floated.

**How:**
```css
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

**Why:** Forces parent to contain floated children (legacy layout technique).

---

### Use Case 3: Custom List Styling
**When:** Creating numbered lists with custom formatting.

**How:**
```css
ol {
  counter-reset: item;
  list-style: none;
}

ol li {
  counter-increment: item;
}

ol li::before {
  content: counter(item) ". ";
  font-weight: bold;
  color: #007bff;
}
```

**Why:** More control than default `list-style-type`.

---

### Use Case 4: Tooltip Arrows
**When:** Creating speech bubble effects.

**How:**
```css
.tooltip::after {
  content: "";
  border: 10px solid transparent;
  border-top-color: black;
  position: absolute;
  bottom: -20px;
  left: 50%;
  margin-left: -10px;
}
```

**Why:** Pure CSS tooltips without JavaScript.

---

## Browser Support

| Pseudo-Element | Chrome | Firefox | Safari | Edge | IE 11 |
|----------------|--------|---------|--------|------|-------|
| `::before`, `::after` | All | All | All | All | Full (with `:`) |
| `::first-letter`, `::first-line` | All | All | All | All | Full |
| `::selection` | All | All (`::-moz-selection`) | All | All | Full |
| `::placeholder` | 57+ | 51+ | 10.1+ | 79+ | Prefix `-ms-` |
| `::marker` | 86+ | 68+ | 11.1+ | 86+ | None |

**Fallback for ::before/::after in IE:**
```css
/* Use single colon in IE 11 */
element:before { content: "..."; }
element:after { content: "..."; }
```

**Can I Use Links:**
- [`::marker`](https://caniuse.com/css-marker-pseudo)
- [`::placeholder`](https://caniuse.com/css-placeholder)

---

## Best Practices

### Do This

1. **Always Include `content` Property**
   ```css
   button::before {
     content: ""; /* Required, even if empty */
     display: inline-block;
     width: 20px;
     height: 20px;
     background: url(icon.svg);
   }
   ```
   **Why:** `::before`/`::after` won't render without `content`.

2. **Use for Decorative Content Only**
   ```css
   /* Good: Decorative icon */
   .icon::before { content: ""; }

   /* Bad: Essential text (not accessible to screen readers) */
   .email::before { content: "Email: "; } /* */
   ```
   **Why:** Pseudo-elements are invisible to screen readers and search engines.

3. **Combine with `:hover` for Interactions**
   ```css
   a::after {
     content: "→";
     opacity: 0;
     transition: opacity 0.3s;
   }

   a:hover::after {
     opacity: 1;
   }
   ```
   **Why:** Creates smooth reveal effects.

4. **Use Double Colon (::) Syntax**
   ```css
   /* Modern */
   div::before { content: ""; }

   /* Legacy (avoid) */
   div:before { content: ""; }
   ```
   **Why:** Clarity and modern standards.

---

### Avoid This

1. **Adding Semantic Content with Pseudo-Elements**
   ```css
   /* BAD: Screen readers won't read this */
   .price::before {
     content: "Price: ";
   }
   ```
   **Why Not:** Essential content should be in HTML (accessibility).
   **Instead:** Put "Price:" in HTML, use pseudo-elements for icons/decorations.

2. **Forgetting `content` Property**
   ```css
   /* Won't work (no content) */
   div::before {
     background: red;
     width: 50px;
     height: 50px;
   }
   ```
   **Fix:**
   ```css
   div::before {
     content: ""; /* NOW it works */
     background: red;
     width: 50px;
     height: 50px;
     display: block;
   }
   ```

3. **Using on Self-Closing Elements**
   ```css
   /* WON'T WORK on <img>, <input>, <br> */
   img::before { content: "Icon"; } /* */
   input::before { content: "Label"; } /* */
   ```
   **Why Not:** Self-closing elements can't have content (no opening/closing tags).

---

## Video Tutorial

### CSS Tutorial - Full Course for Beginners

**Watch Section:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=1920s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=1920s)

**Relevant Timestamps:**
- `0:32:00` - Introduction to pseudo-elements
- `0:33:20` - `::before` and `::after` explained
- `0:35:40` - Creating shapes with pseudo-elements
- `0:37:00` - `::first-letter` and `::first-line`
- `0:39:10` - Real-world examples (tooltips, badges)

**What You'll Learn:**
Live coding demonstrations of common pseudo-element patterns, including icon injection, clearfix, and decorative effects.

**Additional Resources:**
- [W3Schools - CSS Pseudo-Elements](https://www.w3schools.com/css/css_pseudo_elements.asp)
- [MDN Web Docs - Pseudo-Elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)
- [CSS-Tricks - A Whole Bunch of Amazing Stuff Pseudo Elements Can Do](https://css-tricks.com/pseudo-element-roundup/)

---

## Related Topics

**Prerequisites (Learn These First):**
- [CSS Selectors](../01-fundamentals/selectors.md) - Basic selector types
- [Pseudo-Classes](pseudo-classes.md) - Understand `:hover`, `:focus`, etc.
- [Position Property](../05-layout-basics/position.md) - For absolute positioning tricks

**Related Concepts:**
- [Content Property](https://developer.mozilla.org/en-US/docs/Web/CSS/content) - The `content` property reference
- [Transitions](../09-visual-effects/transitions.md) - Animate pseudo-element state changes
- [Counters](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Counter_Styles) - Advanced `counter()` usage

**Next Steps (Learn These Next):**
- [Attribute Selectors](attribute-selectors.md) - Select elements by attributes
- [Gradients](../09-visual-effects/gradients.md) - Use in `::before`/`::after` backgrounds

---

## Practice Exercise

### Challenge: Create a Styled Blockquote Component

**Objective:** Build a fancy blockquote using pseudo-elements for decorative quotation marks, author attribution, and a visual accent line.

**Requirements:**
- [ ] Large decorative quotation marks using `::before`
- [ ] Author name added with `::after` (e.g., "— Author Name")
- [ ] Vertical accent line on the left using `::before` on container
- [ ] First line of quote text is bold (using `::first-line`)
- [ ] Bonus: Animated quotation mark on hover

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Styled Blockquote</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <blockquote class="quote" data-author="Albert Einstein">
    Imagination is more important than knowledge. Knowledge is limited.
    Imagination encircles the world.
  </blockquote>
</body>
</html>
```

**CSS (Complete this):**
```css
/* Your CSS here - use pseudo-elements! */
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**CSS:**
```css
body {
  font-family: Georgia, serif;
  padding: 50px;
  background: #f5f5f5;
}

.quote {
  position: relative;
  max-width: 600px;
  margin: 0 auto;
  padding: 30px 30px 30px 50px;
  background: white;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  font-size: 1.2rem;
  line-height: 1.8;
  color: #333;
}

/* Vertical accent line (left border) */
.quote::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 5px;
  height: 100%;
  background: linear-gradient(180deg, #007bff, #0056b3);
  border-radius: 8px 0 0 8px;
}

/* Large decorative quote mark */
.quote::after {
  content: """;
  position: absolute;
  top: -20px;
  left: 40px;
  font-size: 6rem;
  color: #007bff;
  opacity: 0.2;
  line-height: 1;
  transition: opacity 0.3s ease, transform 0.3s ease;
}

/* Hover effect on quote mark */
.quote:hover::after {
  opacity: 0.4;
  transform: scale(1.1);
}

/* Bold first line */
.quote::first-line {
  font-weight: bold;
  color: #000;
}

/* Author attribution (from data attribute) */
.quote {
  padding-bottom: 50px; /* Space for author */
}

.quote::before {
  /* We already used ::before for the line, so we'll use a different approach */
}

/* Alternative: Add author in HTML with a <cite> tag, or use JavaScript */
/* For pure CSS solution using data attribute: */
.quote::after {
  content: "— " attr(data-author);
  position: absolute;
  bottom: 20px;
  right: 30px;
  font-size: 1rem;
  font-style: italic;
  color: #666;
}

/* Redefine ::after to include both quote mark and author */
/* Since we can only use ::after once, let's restructure: */

/* Final approach: Use ::before for quote mark, ::after for author */
.quote::before {
  content: """;
  position: absolute;
  top: -20px;
  left: 40px;
  font-size: 6rem;
  color: #007bff;
  opacity: 0.2;
  line-height: 1;
  z-index: -1;
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.quote:hover::before {
  opacity: 0.4;
  transform: scale(1.1);
}

.quote::after {
  content: "— " attr(data-author);
  display: block;
  margin-top: 20px;
  font-size: 1rem;
  font-style: italic;
  color: #666;
  text-align: right;
}

/* Add left border separately (no pseudo-element) */
.quote {
  border-left: 5px solid #007bff;
}
```

**Refined Solution (Using both pseudo-elements efficiently):**
```css
body {
  font-family: Georgia, serif;
  padding: 50px;
  background: #f5f5f5;
}

.quote {
  position: relative;
  max-width: 600px;
  margin: 0 auto;
  padding: 40px 40px 60px 60px;
  background: white;
  border-left: 5px solid #007bff;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  font-size: 1.2rem;
  line-height: 1.8;
  color: #333;
}

/* Large decorative quote mark (::before) */
.quote::before {
  content: """;
  position: absolute;
  top: 10px;
  left: 15px;
  font-size: 5rem;
  color: #007bff;
  opacity: 0.15;
  line-height: 1;
  font-family: Georgia, serif;
  transition: opacity 0.3s, transform 0.3s;
}

.quote:hover::before {
  opacity: 0.3;
  transform: scale(1.1);
}

/* Author attribution (::after) */
.quote::after {
  content: "— " attr(data-author);
  display: block;
  margin-top: 20px;
  font-size: 1rem;
  font-style: italic;
  font-weight: normal;
  color: #666;
  text-align: right;
}

/* Bold first line */
.quote::first-line {
  font-weight: 600;
}
```

**Explanation:**
- **`border-left`**: Creates the accent line (simpler than `::before`)
- **`::before`**: Large, semi-transparent quotation mark (decorative)
- **`::after`**: Author name pulled from `data-author` attribute using `attr()`
- **`::first-line`**: Makes first line bold for emphasis
- **Hover effect**: Quote mark scales up and becomes more opaque

</details>

---

### Expected Result

**Visual Outcome:**
- Large, faded quotation mark behind text
- Blue vertical line on the left
- First line of quote is bold
- Author name appears at bottom-right in italics
- Quotation mark animates on hover

**Key Learnings:**
- `::before` and `::after` can create complex decorative elements
- `attr()` function pulls data from HTML attributes
- Pseudo-elements can be animated with transitions
- `::first-line` dynamically styles text based on viewport width
- Combining pseudo-elements with borders creates layered designs

---

## Navigation

**Previous:** [← Pseudo-Classes](pseudo-classes.md)
**Next:** [Attribute Selectors →](attribute-selectors.md)
**Up:** [↑ Back to Selectors Advanced](../README.md#8️⃣-selectors-advanced-6-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Selectors Advanced
**Difficulty:** Intermediate
