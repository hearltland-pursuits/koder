---
title: CSS Attribute Selectors
category: Selectors Advanced
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Attribute Selectors

> **Quick Summary:** Attribute selectors target HTML elements based on the **presence** or **value** of their attributes (like `href`, `title`, `data-*`). They let you style elements without adding classes, using patterns like "starts with," "ends with," or "contains."

## Table of Contents
- [Introduction](#introduction)
- [Why Attribute Selectors Matter](#why-attribute-selectors-matter)
- [Basic Syntax](#basic-syntax)
- [Types of Attribute Selectors](#types-of-attribute-selectors)
- [Pattern Matching Selectors](#pattern-matching-selectors)
- [Case-Insensitive Matching](#case-insensitive-matching)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

**Attribute selectors** let you style HTML elements based on their **attributes and attribute values**, not just their class or ID. This means you can target elements like:
- All links to PDF files → `a[href$=".pdf"]`
- All required form inputs → `input[required]`
- All elements with a specific data attribute → `[data-role="admin"]`

Before attribute selectors, you'd need to manually add classes to every element you wanted to style. Now, CSS can "read" HTML attributes and apply styles automatically, making your stylesheets more dynamic and maintainable.

**Key Concept:** Attribute selectors use **square brackets `[ ]`** and can match attributes in seven different ways, from simple presence checks to complex pattern matching.

---

## Why Attribute Selectors Matter

### 1. **Automatic Styling Based on File Types**

```css
/* Style PDF links with an icon */
a[href$=".pdf"]::after {
  content: " ";
}

/* Style external links */
a[href^="http"]::after {
  content: " ↗";
}

/* Style email links */
a[href^="mailto:"]::before {
  content: " ";
}
```

**Result:** No need to add classes like `.pdf-link` to every PDF link in your HTML.

### 2. **Form Validation Styling**

```css
/* Required fields get a red border */
input[required] {
  border-left: 3px solid red;
}

/* Disabled inputs are grayed out */
input[disabled] {
  background: #f0f0f0;
  cursor: not-allowed;
}
```

### 3. **Data Attribute Styling (JavaScript Integration)**

```html
<button data-state="loading">Submit</button>
```

```css
button[data-state="loading"] {
  background: gray;
  cursor: wait;
}

button[data-state="loading"]::after {
  content: "...";
}
```

**Result:** CSS reacts to JavaScript-driven data attributes (no class toggling needed).

### 4. **Career Relevance**
- **Interview question:** "How do you style different link types without classes?"
- **Framework pattern:** React/Vue use `data-*` attributes that CSS can target
- **Common task:** "Automatically style required form fields"
- **Accessibility:** Targeting `[aria-*]` attributes for screen reader states

---

## Basic Syntax

### Square Bracket Notation

```css
selector[attribute] {
  property: value;
}
```

**Examples:**
```css
a[href] { color: blue; }              /* Links with href attribute */
input[type="text"] { border: 1px solid #ccc; }  /* Text inputs */
div[data-role] { background: #f0f0f0; }  /* Divs with data-role attribute */
```

---

## Types of Attribute Selectors

### 1. **`[attribute]` — Presence Check**

**Selects:** Elements that **have** the specified attribute (regardless of value).

```css
/* All links with a title attribute */
a[title] {
  text-decoration: underline dotted;
  cursor: help;
}
```

**HTML:**
```html
<a href="#" title="More information">Hover me</a> <!-- Selected -->
<a href="#">No title</a> <!-- Not selected -->
```

---

### 2. **`[attribute="value"]` — Exact Match**

**Selects:** Elements where attribute **equals exactly** the specified value.

```css
/* Only text inputs */
input[type="text"] {
  background: white;
}

/* Only checkboxes */
input[type="checkbox"] {
  width: 20px;
  height: 20px;
}
```

**HTML:**
```html
<input type="text"> <!-- Selected -->
<input type="email"> <!-- Not selected -->
```

---

### 3. **`[attribute~="value"]` — Word Match**

**Selects:** Elements where attribute **contains the value as a whole word** (space-separated).

```css
/* Class contains "featured" as a whole word */
div[class~="featured"] {
  border: 2px solid gold;
}
```

**HTML:**
```html
<div class="card featured">...</div> <!-- Selected (whole word) -->
<div class="card featured-item">...</div> <!-- NOT selected (part of word) -->
```

**Use Case:** Targeting specific class names when element has multiple classes.

---

### 4. **`[attribute|="value"]` — Prefix Match (Hyphen-Separated)**

**Selects:** Elements where attribute **starts with value** followed by a hyphen or is exactly the value.

```css
/* Language variants (en, en-US, en-GB) */
html[lang|="en"] {
  font-family: "Arial", sans-serif;
}
```

**HTML:**
```html
<html lang="en"> <!-- Selected -->
<html lang="en-US"> <!-- Selected -->
<html lang="en-GB"> <!-- Selected -->
<html lang="fr"> <!-- Not selected -->
```

**Use Case:** Internationalization (targeting language variants).

---

## Pattern Matching Selectors

### 5. **`[attribute^="value"]` — Starts With**

**Selects:** Elements where attribute **begins with** the specified value.

```css
/* All links to external sites (http/https) */
a[href^="http"] {
  color: blue;
}

a[href^="http"]::after {
  content: " ↗";
}

/* All telephone links */
a[href^="tel:"] {
  color: green;
}
```

**HTML:**
```html
<a href="https://example.com">External</a> <!-- Selected -->
<a href="/internal">Internal</a> <!-- Not selected -->
<a href="tel:+1234567890">Call Us</a> <!-- Selected -->
```

---

### 6. **`[attribute$="value"]` — Ends With**

**Selects:** Elements where attribute **ends with** the specified value.

```css
/* PDF links */
a[href$=".pdf"]::after {
  content: "  PDF";
  font-size: 0.8rem;
  color: red;
}

/* Image files */
a[href$=".jpg"],
a[href$=".png"],
a[href$=".gif"] {
  font-weight: bold;
}
```

**HTML:**
```html
<a href="/document.pdf">Download PDF</a> <!-- Selected -->
<a href="/page.html">HTML Page</a> <!-- Not selected -->
```

**Use Case:** Automatically styling file download links by extension.

---

### 7. **`[attribute*="value"]` — Contains**

**Selects:** Elements where attribute **contains** the value anywhere.

```css
/* Links containing "youtube" anywhere in URL */
a[href*="youtube"] {
  color: red;
  font-weight: bold;
}

/* Elements with "admin" in data-role */
div[data-role*="admin"] {
  background: #ffe0e0;
}
```

**HTML:**
```html
<a href="https://www.youtube.com/watch?v=123">Video</a> <!-- Selected -->
<a href="https://youtu.be/123">Short Link</a> <!-- NOT selected (different pattern) -->
```

---

## Case-Insensitive Matching

**By default**, attribute selectors are **case-sensitive**. Add **`i`** flag for case-insensitive matching.

### Syntax: `[attribute="value" i]`

```css
/* Match "PDF", "pdf", "Pdf", etc. */
a[href$=".pdf" i]::after {
  content: " ";
}

/* Match input types regardless of case */
input[type="text" i] {
  background: white;
}
```

**HTML:**
```html
<a href="/doc.PDF">File</a> <!-- Selected (case-insensitive) -->
<a href="/doc.pdf">File</a> <!-- Selected -->
```

**Browser Support:** Chrome 49+, Firefox 47+, Safari 9+

---

## Examples

### Example 1: Automatic Link Icon Styling

**Scenario:** Automatically add icons to different link types without adding classes.

**HTML:**
```html
<nav>
  <a href="/about.html">About Us</a>
  <a href="https://example.com">External Site</a>
  <a href="/guide.pdf">User Guide</a>
  <a href="mailto:info@example.com">Email Us</a>
  <a href="tel:+1234567890">Call Us</a>
</nav>
```

**CSS:**
```css
/* Base link styling */
nav a {
  display: block;
  padding: 10px;
  color: #333;
  text-decoration: none;
}

/* External links (http/https) */
a[href^="http"]::after {
  content: " ↗";
  color: #007bff;
}

/* PDF links */
a[href$=".pdf"]::after {
  content: " ";
  color: #dc3545;
}

/* Email links */
a[href^="mailto:"]::before {
  content: " ";
  color: #28a745;
}

/* Phone links */
a[href^="tel:"]::before {
  content: " ";
  color: #ffc107;
}
```

**Result:**
```
About Us
External Site ↗
 User Guide
 Email Us
 Call Us
```

---

### Example 2: Form Input Styling by Type

**Scenario:** Style different input types with visual cues.

**HTML:**
```html
<form>
  <input type="text" placeholder="Name">
  <input type="email" placeholder="Email" required>
  <input type="password" placeholder="Password">
  <input type="number" min="1" max="10">
  <input type="text" disabled placeholder="Disabled">
</form>
```

**CSS:**
```css
/* Base input styling */
input {
  display: block;
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 2px solid #ddd;
  border-radius: 4px;
}

/* Text inputs */
input[type="text"] {
  border-color: #007bff;
}

/* Email inputs */
input[type="email"] {
  border-color: #28a745;
}

/* Password inputs */
input[type="password"] {
  border-color: #dc3545;
}

/* Number inputs */
input[type="number"] {
  border-color: #ffc107;
}

/* Required fields (red asterisk) */
input[required] {
  border-left: 4px solid red;
}

/* Disabled inputs */
input[disabled] {
  background: #f0f0f0;
  cursor: not-allowed;
  opacity: 0.6;
}
```

**Result:** Each input type has a unique border color, required fields have a red left border, and disabled inputs are grayed out.

---

### Example 3: Data Attribute Theming

**Scenario:** Use data attributes to control component themes.

**HTML:**
```html
<button data-theme="primary">Primary Button</button>
<button data-theme="danger">Danger Button</button>
<button data-theme="success">Success Button</button>
```

**CSS:**
```css
/* Base button */
button {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.3s;
}

/* Primary theme */
button[data-theme="primary"] {
  background: #007bff;
  color: white;
}

button[data-theme="primary"]:hover {
  background: #0056b3;
}

/* Danger theme */
button[data-theme="danger"] {
  background: #dc3545;
  color: white;
}

button[data-theme="danger"]:hover {
  background: #c82333;
}

/* Success theme */
button[data-theme="success"] {
  background: #28a745;
  color: white;
}

button[data-theme="success"]:hover {
  background: #218838;
}
```

**Result:** Buttons styled based on `data-theme` attribute (JavaScript can change themes by updating the attribute).

---

### Example 4: Image Alt Text Fallback

**Scenario:** Show alt text when images fail to load.

**HTML:**
```html
<img src="broken-link.jpg" alt="Descriptive text about image">
```

**CSS:**
```css
img[alt] {
  font-style: italic;
  color: #999;
}

/* Show alt text when image doesn't load */
img[alt]::after {
  content: " [Image: " attr(alt) "]";
  display: block;
  font-size: 0.9rem;
}
```

**Result:** If image doesn't load, displays "Image: Descriptive text about image" instead of broken image icon.

---

## Common Use Cases

### Use Case 1: Styling Links to Specific Domains
**When:** Highlighting official/trusted links.

**How:**
```css
a[href*="github.com"] {
  color: #333;
  font-weight: bold;
}

a[href*="github.com"]::before {
  content: " ";
}
```

**Why:** Instantly recognizable GitHub links.

---

### Use Case 2: Accessibility (ARIA Attributes)
**When:** Styling elements based on screen reader states.

**How:**
```css
/* Expanded accordion sections */
[aria-expanded="true"] {
  background: #f0f0f0;
}

/* Hidden content (visually hide but keep for screen readers) */
[aria-hidden="true"] {
  display: none;
}
```

**Why:** CSS responds to accessibility attributes (better than class toggling).

---

### Use Case 3: Download Link Indicators
**When:** Showing file size/type next to download links.

**How:**
```html
<a href="/file.pdf" data-size="2.5MB">Download PDF</a>
```

```css
a[data-size]::after {
  content: " (" attr(data-size) ")";
  font-size: 0.9rem;
  color: #666;
}
```

**Result:** "Download PDF (2.5MB)"

**Why:** File size info added via CSS, no JavaScript needed.

---

### Use Case 4: Language-Specific Styling
**When:** Targeting elements in specific languages.

**How:**
```css
/* English content */
[lang="en"] {
  font-family: "Arial", sans-serif;
}

/* Japanese content */
[lang="ja"] {
  font-family: "Hiragino Sans", sans-serif;
}

/* Arabic content (RTL) */
[lang="ar"] {
  direction: rtl;
  text-align: right;
}
```

**Why:** Automatic font/direction changes for multilingual sites.

---

## Browser Support

| Selector | Chrome | Firefox | Safari | Edge | IE 11 |
|----------|--------|---------|--------|------|-------|
| `[attribute]` | All | All | All | All | Full |
| `[attribute="value"]` | All | All | All | All | Full |
| `[attribute^="value"]` | All | All | All | All | Full |
| `[attribute$="value"]` | All | All | All | All | Full |
| `[attribute*="value"]` | All | All | All | All | Full |
| `[attribute~="value"]` | All | All | All | All | Full |
| `[attribute\|="value"]` | All | All | All | All | Full |
| `[attribute="value" i]` | 49+ | 47+ | 9+ | 79+ | None |

**Verdict:** All attribute selectors have **100% support** except case-insensitive flag (`i`).

**Can I Use Link:** [https://caniuse.com/css-case-insensitive](https://caniuse.com/css-case-insensitive)

---

## Best Practices

### Do This

1. **Use for Dynamic Content (File Types, Links)**
   ```css
   a[href$=".pdf"]::after { content: " "; }
   a[href^="http"]::after { content: " ↗"; }
   ```
   **Why:** Automatically styles links without manual class assignment.

2. **Combine with Pseudo-Classes for State**
   ```css
   input[required]:invalid {
     border-color: red;
   }
   ```
   **Why:** Precise targeting (required AND invalid inputs only).

3. **Use Data Attributes for JavaScript Integration**
   ```css
   [data-state="loading"] {
     opacity: 0.5;
     cursor: wait;
   }
   ```
   **Why:** CSS reacts to JavaScript state changes cleanly.

4. **Target Accessibility Attributes**
   ```css
   [aria-expanded="true"] {
     background: #f0f0f0;
   }
   ```
   **Why:** Visual feedback matches screen reader state.

---

### Avoid This

1. **Over-Relying on Attribute Selectors (Performance)**
   ```css
   /* Slow: Scans every div for data-role */
   div[data-role="admin"] {
     background: red;
   }
   ```
   **Why Not:** Slower than class selectors (browsers can't optimize as well).
   **Instead:** Use classes for frequently-targeted elements.

2. **Case-Sensitive Matching Without `i` Flag**
   ```css
   /* Won't match "PDF", "Pdf", etc. */
   a[href$=".pdf"]::after { content: " "; }
   ```
   **Problem:** Users might upload files as `.PDF` (uppercase).
   **Instead:**
   ```css
   a[href$=".pdf" i]::after { content: " "; }
   ```

3. **Using for Critical Styling**
   ```css
   /* BAD: If attribute is removed, layout breaks */
   div[data-column] {
     width: 50%;
   }
   ```
   **Why Not:** Fragile (attributes can change/be removed).
   **Instead:** Use classes for structural styling, attributes for enhancements.

---

## Video Tutorial

### CSS Tutorial - Full Course for Beginners

**Watch Section:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=2100s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=2100s)

**Relevant Timestamps:**
- `0:35:00` - Introduction to attribute selectors
- `0:36:20` - Exact match and prefix/suffix patterns
- `0:38:00` - Real-world examples (file type styling)
- `0:39:40` - Data attributes and JavaScript integration
- `0:41:00` - Accessibility attributes (ARIA)

**What You'll Learn:**
Practical demonstrations of automatically styling links, forms, and components using attribute selectors.

**Additional Resources:**
- [W3Schools - CSS Attribute Selectors](https://www.w3schools.com/css/css_attribute_selectors.asp)
- [MDN Web Docs - Attribute Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)
- [CSS-Tricks - The Skinny on CSS Attribute Selectors](https://css-tricks.com/attribute-selectors/)

---

## Related Topics

**Prerequisites (Learn These First):**
- [CSS Selectors](../01-fundamentals/selectors.md) - Basic selector types
- [Combinators](combinators.md) - Combining selectors

**Related Concepts:**
- [Pseudo-Classes](pseudo-classes.md) - Combine with `:hover`, `:focus`, etc.
- [Data Attributes](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes) - Using `data-*` in HTML
- [ARIA Attributes](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA) - Accessibility attributes

**Next Steps (Learn These Next):**
- [Specificity](specificity.md) - How attribute selectors affect CSS weight
- [Forms](../11-components/forms.md) - Styling forms with attribute selectors

---

## Practice Exercise

### Challenge: Build a File Library with Automatic Icons

**Objective:** Create a file download list that automatically styles links based on file type using attribute selectors.

**Requirements:**
- [ ] PDF files show a red PDF icon
- [ ] Word documents (.doc, .docx) show a blue Word icon
- [ ] Excel files (.xls, .xlsx) show a green Excel icon
- [ ] External links (http) show an external link icon
- [ ] Required downloads (data-required="true") have a red asterisk
- [ ] Bonus: Case-insensitive file extension matching

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>File Library</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="file-library">
    <h2>Document Downloads</h2>
    <ul>
      <li><a href="/files/report.pdf" data-required="true">Annual Report</a></li>
      <li><a href="/files/guide.PDF">User Guide</a></li>
      <li><a href="/files/contract.docx">Contract Template</a></li>
      <li><a href="/files/data.xlsx">Sales Data</a></li>
      <li><a href="https://example.com/external.pdf">External Resource</a></li>
      <li><a href="/files/presentation.doc">Presentation</a></li>
    </ul>
  </div>
</body>
</html>
```

**CSS (Complete this):**
```css
/* Your CSS here - use attribute selectors! */
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

.file-library {
  max-width: 600px;
  margin: 0 auto;
  background: white;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

h2 {
  margin-top: 0;
  color: #333;
  border-bottom: 2px solid #007bff;
  padding-bottom: 10px;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin-bottom: 15px;
}

/* Base link styling */
a {
  display: inline-block;
  padding: 10px 15px;
  color: #333;
  text-decoration: none;
  border-left: 4px solid #ddd;
  transition: background 0.3s;
}

a:hover {
  background: #f0f0f0;
}

/* PDF files (case-insensitive) */
a[href$=".pdf" i]::before {
  content: " ";
  color: #dc3545;
  font-weight: bold;
}

a[href$=".pdf" i] {
  border-left-color: #dc3545;
}

/* Word documents */
a[href$=".doc" i]::before,
a[href$=".docx" i]::before {
  content: " ";
  color: #007bff;
  font-weight: bold;
}

a[href$=".doc" i],
a[href$=".docx" i] {
  border-left-color: #007bff;
}

/* Excel files */
a[href$=".xls" i]::before,
a[href$=".xlsx" i]::before {
  content: " ";
  color: #28a745;
  font-weight: bold;
}

a[href$=".xls" i],
a[href$=".xlsx" i] {
  border-left-color: #28a745;
}

/* External links */
a[href^="http"]::after {
  content: " ↗";
  color: #007bff;
  font-size: 0.8rem;
  margin-left: 5px;
}

/* Required downloads */
a[data-required="true"]::after {
  content: " *";
  color: red;
  font-weight: bold;
  font-size: 1.2rem;
  margin-left: 5px;
}

/* Handle both external AND required (stacking ::after content) */
a[href^="http"][data-required="true"]::after {
  content: " ↗ *";
  color: #007bff;
}

/* Styling required files differently */
a[data-required="true"] {
  background: #fff3cd;
}
```

**Explanation:**
- **`[href$=".pdf" i]`**: Matches PDF links (case-insensitive `i` flag)
- **`[href$=".doc" i], [href$=".docx" i]`**: Matches Word documents
- **`[href$=".xls" i], [href$=".xlsx" i]`**: Matches Excel files
- **`[href^="http"]`**: Matches external links (starts with http)
- **`[data-required="true"]`**: Matches required downloads
- **Stacking icons**: Uses `::before` for file type icons, `::after` for external/required indicators
- **Border colors**: Different border colors per file type for visual distinction

</details>

---

### Expected Result

**Visual Outcome:**
- PDF files: Red PDF icon () and red left border
- Word files: Blue book icon () and blue left border
- Excel files: Green chart icon () and green left border
- External links: External link icon (↗) after text
- Required files: Red asterisk (*) and yellow background

**Key Learnings:**
- Attribute selectors automate styling based on HTML attributes
- Case-insensitive flag (`i`) handles inconsistent file extensions
- `^=` (starts with) and `$=` (ends with) enable powerful pattern matching
- `data-*` attributes create JavaScript-CSS integration points
- Combining multiple attribute selectors creates precise targeting

---

## Navigation

**Previous:** [← Pseudo-Elements](pseudo-elements.md)
**Next:** [Gradients →](../09-visual-effects/gradients.md)
**Up:** [↑ Back to Selectors Advanced](../README.md#8️⃣-selectors-advanced-6-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Selectors Advanced
**Difficulty:** Intermediate
