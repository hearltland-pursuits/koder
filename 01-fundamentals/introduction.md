---
title: CSS Introduction
category: Fundamentals
order: 1
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Introduction

> **Quick Summary:** CSS (Cascading Style Sheets) is the language used to style and layout web pages. It controls colors, fonts, spacing, positioning, and visual presentation of HTML elements.

## Table of Contents
- [Introduction](#introduction)
- [What is CSS?](#what-is-css)
- [Why CSS Matters](#why-css-matters)
- [How CSS Works](#how-css-works)
- [CSS Syntax](#css-syntax)
- [Your First CSS](#your-first-css)
- [Examples](#examples)
- [The Three Ways to Add CSS](#the-three-ways-to-add-css)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

Imagine building a house. HTML is the structure—the walls, floors, and roof. CSS is everything that makes it beautiful—the paint colors, furniture arrangement, decorations, and lighting. Without CSS, websites would be plain text on white backgrounds. With CSS, we create visually stunning, user-friendly experiences.

CSS was created in 1996 by Håkon Wium Lie and Bert Bos to solve a critical problem: separating content (HTML) from presentation (design). Before CSS, designers had to use HTML attributes like `<font>` tags and tables for layout, making code messy and hard to maintain. CSS revolutionized web development by letting developers write HTML once and style it anywhere.

Today, CSS powers every modern website. From Netflix's dark theme to Airbnb's clean layouts, CSS is the invisible artist behind the web. Learning CSS is essential for anyone building for the web—whether you're creating portfolios, business sites, or complex web applications.

**Key Concept:** CSS doesn't change what content says, it changes how content looks. HTML provides meaning; CSS provides beauty.

---

## What is CSS?

**CSS** stands for **Cascading Style Sheets**. Let's break that down:

- **Cascading:** Multiple style rules can apply to the same element. CSS uses a priority system (specificity) to determine which rules win when conflicts arise. This "cascade" allows you to write general styles and override them as needed.

- **Style:** CSS defines visual presentation—colors, sizes, spacing, positioning, animations, and more.

- **Sheets:** CSS is typically written in `.css` files (stylesheets) that can be linked to multiple HTML pages, promoting reusability.

### CSS is NOT JavaScript

A common beginner mistake: CSS is a **styling language**, not a programming language. It doesn't have logic, loops, or functions (though it has some functional features like `calc()` and variables). CSS describes appearance; JavaScript handles behavior and interactivity.

---

## Why CSS Matters

### 1. **Separation of Concerns**
HTML handles structure and content. CSS handles presentation. This separation makes code:
- **Easier to maintain:** Change site colors in one CSS file instead of editing hundreds of HTML pages
- **More organized:** Designers work on CSS while developers focus on HTML/JavaScript
- **Reusable:** One stylesheet can style an entire website

### 2. **Responsive Design**
CSS enables websites to adapt to different screen sizes (phones, tablets, desktops) using media queries and flexible layouts like Flexbox and Grid.

### 3. **Performance**
CSS files load once and are cached by browsers, making subsequent page loads faster. Compare this to inline styles, which are repeated on every page.

### 4. **Accessibility**
Proper CSS improves accessibility for users with disabilities by controlling focus states, color contrast, and text sizing.

### 5. **Career Opportunities**
CSS is a fundamental skill for:
- **Front-End Developers** ($60-100K+)
- **UI/UX Designers** ($70-110K+)
- **Full-Stack Developers** ($80-130K+)

Mastering CSS is non-negotiable for modern web development careers.

---

## How CSS Works

### The CSS Process (What Happens Behind the Scenes)

1. **Browser Loads HTML:** The browser reads your HTML file
2. **CSS Discovery:** The browser finds CSS (external file, `<style>` tag, or inline styles)
3. **Parsing:** The browser parses CSS into rules
4. **CSSOM Creation:** The browser builds a CSS Object Model (CSSOM) tree
5. **Rendering:** The browser combines HTML (DOM) + CSS (CSSOM) into a visual webpage
6. **Display:** You see the styled page

### The Cascade: How CSS Decides Which Rules Apply

When multiple CSS rules target the same element, CSS uses these factors to decide which rule wins:

1. **Specificity:** More specific selectors win (ID > Class > Element)
2. **Source Order:** Later rules override earlier rules (if specificity is equal)
3. **Importance:** `!important` overrides everything (use sparingly!)

**Example:**
```css
/* Less specific */
p { color: blue; }

/* More specific - this wins */
.intro p { color: red; }
```

---

## CSS Syntax

Every CSS rule follows this structure:

```css
selector {
  property: value;
  property: value;
}
```

### Anatomy of a CSS Rule

```css
h1 {
  color: blue;
  font-size: 32px;
}
```

**Breaking it down:**
- **`h1`** = Selector (what to style)
- **`{ }`** = Declaration block (contains all styles)
- **`color`** = Property (what aspect to style)
- **`blue`** = Value (how to style it)
- **`;`** = Semicolon (ends each declaration)

### Multiple Selectors

Style multiple elements at once:

```css
h1, h2, h3 {
  font-family: Arial, sans-serif;
  color: #333;
}
```

---

## Your First CSS

Let's create a complete example from scratch.

**Step 1: Create `index.html`**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My First CSS Page</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>Welcome to CSS</h1>
  <p>This paragraph is styled with CSS!</p>
</body>
</html>
```

**Step 2: Create `styles.css`**
```css
body {
  background-color: #f0f0f0;
  font-family: Arial, sans-serif;
}

h1 {
  color: #2c3e50;
  text-align: center;
}

p {
  color: #555;
  font-size: 18px;
  line-height: 1.6;
}
```

**Step 3: Open `index.html` in a browser**

You'll see:
- Light gray background
- Centered dark blue heading
- Gray paragraph text with readable spacing

**Congratulations!** You just wrote CSS. 🎉

---

## Examples

### Example 1: Changing Text Colors

**Scenario:** Make headings blue and paragraphs dark gray

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Text Colors</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>This is a Heading</h1>
  <p>This is a paragraph with important information.</p>
</body>
</html>
```

**CSS:**
```css
h1 {
  color: #3498db; /* Blue */
}

p {
  color: #2c3e50; /* Dark gray */
}
```

**Result:** Heading appears blue, paragraph appears dark gray.

---

### Example 2: Styling with Classes

**Scenario:** Create reusable styles for buttons

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Button Styles</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <button class="btn-primary">Primary Button</button>
  <button class="btn-secondary">Secondary Button</button>
</body>
</html>
```

**CSS:**
```css
.btn-primary {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 12px 24px;
  font-size: 16px;
  cursor: pointer;
}

.btn-secondary {
  background-color: #95a5a6;
  color: white;
  border: none;
  padding: 12px 24px;
  font-size: 16px;
  cursor: pointer;
}
```

**Result:** Two styled buttons with different colors but consistent sizing.

---

### Example 3: Real-World Navigation Bar

**Scenario:** Create a horizontal navigation menu

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
  <nav class="navbar">
    <ul>
      <li><a href="#home">Home</a></li>
      <li><a href="#about">About</a></li>
      <li><a href="#services">Services</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>
</body>
</html>
```

**CSS:**
```css
/* Reset default styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.navbar {
  background-color: #2c3e50;
  padding: 1rem;
}

.navbar ul {
  list-style: none; /* Remove bullets */
  display: flex; /* Horizontal layout */
  gap: 2rem; /* Space between items */
}

.navbar a {
  color: white;
  text-decoration: none; /* Remove underline */
  font-size: 18px;
  transition: color 0.3s; /* Smooth color change */
}

.navbar a:hover {
  color: #3498db; /* Blue on hover */
}
```

**Result:** A professional dark navigation bar with horizontally arranged links that turn blue when hovered.

**Notes:**
- `display: flex` creates horizontal layout (modern method)
- `transition` adds smooth animation
- `:hover` pseudo-class triggers on mouse hover

---

## The Three Ways to Add CSS

### 1. External CSS (Recommended)

**Best for:** Multi-page websites, organization, caching

Create a separate `.css` file and link it in HTML:

**HTML:**
```html
<head>
  <link rel="stylesheet" href="styles.css">
</head>
```

**styles.css:**
```css
body {
  background-color: #f0f0f0;
}
```

**Pros:**
- ✅ Reusable across multiple pages
- ✅ Cached by browser (faster load times)
- ✅ Clean separation of concerns
- ✅ Easier to maintain

**Cons:**
- ❌ Requires extra HTTP request (minor)

---

### 2. Internal CSS

**Best for:** Single-page projects, email templates, quick tests

Write CSS inside a `<style>` tag in the HTML `<head>`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Internal CSS Example</title>
  <style>
    body {
      background-color: #f0f0f0;
    }

    h1 {
      color: #2c3e50;
    }
  </style>
</head>
<body>
  <h1>Styled with Internal CSS</h1>
</body>
</html>
```

**Pros:**
- ✅ No external file needed
- ✅ Styles travel with the HTML

**Cons:**
- ❌ Not reusable across pages
- ❌ Makes HTML files larger
- ❌ Harder to maintain

---

### 3. Inline CSS

**Best for:** One-off overrides, dynamic styles via JavaScript

Write CSS directly on HTML elements using the `style` attribute:

```html
<h1 style="color: blue; font-size: 32px;">Inline Styled Heading</h1>
```

**Pros:**
- ✅ Highest specificity (overrides other CSS)
- ✅ Useful for JavaScript-generated styles

**Cons:**
- ❌ Not reusable
- ❌ Makes HTML messy
- ❌ Hard to maintain
- ❌ No caching benefits

---

### Which Method Should You Use?

| Use Case | Method | Reason |
|----------|--------|--------|
| Multi-page website | External CSS | Reusable, cached, organized |
| Single landing page | Internal CSS | Simple, self-contained |
| Dynamic styles (JS) | Inline CSS | Direct manipulation |
| Email templates | Internal CSS | Email clients block external files |
| Quick testing | Internal or Inline | Fast prototyping |

**Best Practice:** Default to **external CSS** unless you have a specific reason to use internal or inline.

---

## Browser Support

CSS has been supported by all major browsers since the 1990s. However, **modern CSS features** vary in support.

| Feature | Chrome | Firefox | Safari | Edge | IE 11 |
|---------|--------|---------|--------|------|-------|
| Basic CSS | 1+ | 1+ | 1+ | 12+ | 5+ |
| Flexbox | 29+ | 28+ | 9+ | 12+ | 11 (partial) |
| Grid | 57+ | 52+ | 10.1+ | 16+ | ❌ None |
| Custom Properties | 49+ | 31+ | 9.1+ | 15+ | ❌ None |

**Key Takeaway:** Basic CSS works everywhere. Modern features (Grid, Variables) require recent browsers. Always check [Can I Use](https://caniuse.com/) for specific features.

---

## Best Practices

### ✅ Do This

1. **Use External Stylesheets**
   ```html
   <link rel="stylesheet" href="styles.css">
   ```
   **Why:** Reusability, caching, clean code

2. **Organize CSS Logically**
   ```css
   /* Reset/Base Styles */
   * { margin: 0; padding: 0; }

   /* Typography */
   h1, h2, h3 { font-family: Arial; }

   /* Layout */
   .container { max-width: 1200px; }

   /* Components */
   .button { padding: 10px 20px; }
   ```
   **Why:** Easier to find and update styles

3. **Use Comments**
   ```css
   /* Navigation Bar Styles */
   .navbar {
     background-color: #333;
   }
   ```
   **Why:** Helps you (and others) understand code later

4. **Write Readable CSS**
   ```css
   /* Good - easy to read */
   .button {
     background-color: #3498db;
     color: white;
     padding: 12px 24px;
   }

   /* Bad - hard to read */
   .button{background-color:#3498db;color:white;padding:12px 24px;}
   ```

5. **Use Classes Over IDs for Styling**
   ```css
   /* Good - reusable */
   .header { background: blue; }

   /* Avoid - not reusable, too specific */
   #header { background: blue; }
   ```
   **Why:** Classes can be reused; IDs are overly specific

---

### ❌ Avoid This

1. **Don't Use Inline Styles for Everything**
   ```html
   <!-- Bad -->
   <p style="color: red; font-size: 18px; line-height: 1.6;">Text</p>

   <!-- Good -->
   <p class="intro-text">Text</p>
   ```
   **Why:** Inline styles are hard to maintain and not reusable

2. **Don't Use `!important` Unless Absolutely Necessary**
   ```css
   /* Bad - creates specificity wars */
   p { color: blue !important; }

   /* Good - use proper specificity */
   .intro p { color: blue; }
   ```
   **Why:** `!important` makes CSS hard to override and debug

3. **Don't Repeat Yourself (DRY Principle)**
   ```css
   /* Bad - repetitive */
   .btn-primary { padding: 12px 24px; font-size: 16px; }
   .btn-secondary { padding: 12px 24px; font-size: 16px; }

   /* Good - reusable base class */
   .btn { padding: 12px 24px; font-size: 16px; }
   .btn-primary { background: blue; }
   .btn-secondary { background: gray; }
   ```

4. **Don't Use Old HTML for Styling**
   ```html
   <!-- Bad - deprecated -->
   <font color="red">Text</font>
   <center>Centered</center>

   <!-- Good - use CSS -->
   <p class="red-text">Text</p>
   <p class="centered">Centered</p>
   ```

---

## Video Tutorial

### 🎥 CSS Tutorial - Full Course for Beginners

**Watch Introduction:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=0s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=0s)

**Relevant Timestamps:**
- `0:00` - What is CSS?
- `2:45` - How CSS works with HTML
- `8:20` - First CSS example
- `15:30` - External vs Internal vs Inline CSS

**What You'll Learn:**
This video section introduces CSS fundamentals, shows how CSS works with HTML, and demonstrates creating your first styled webpage. Perfect for absolute beginners.

**Additional Resources:**
- [W3Schools - CSS Introduction](https://www.w3schools.com/css/css_intro.asp)
- [MDN Web Docs - CSS Basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics)
- [CSS-Tricks - Getting Started](https://css-tricks.com/guides/beginner/)

---

## Related Topics

**Prerequisites (Learn These First):**
- **HTML Basics** - You need to understand HTML structure before styling it
- **Web Development Fundamentals** - How browsers work, basic web concepts

**Related Concepts:**
- [CSS Syntax](syntax.md) - Detailed syntax rules and structure
- [CSS Selectors](selectors.md) - How to target specific HTML elements
- [How to Add CSS](how-to-add-css.md) - Deep dive into the three CSS methods

**Next Steps (Learn These Next):**
- [CSS Selectors](selectors.md) - Master targeting elements
- [CSS Colors](../02-colors/colors-overview.md) - Understanding color systems
- [CSS Box Model](../03-box-model/box-model-concept.md) - Foundation of layout

---

## Practice Exercise

### 🎯 Challenge: Create Your First Styled Webpage

**Objective:** Build a personal introduction page with CSS styling to practice fundamental concepts.

**Requirements:**
- [ ] Create an HTML page with a heading, paragraph, and list
- [ ] Use external CSS (separate `.css` file)
- [ ] Style the heading (color, size, font)
- [ ] Style the paragraph (color, line-height, spacing)
- [ ] Style the list (remove bullets, add spacing)
- [ ] **Bonus:** Add a background color to the page

---

### Starter Code

**HTML (index.html):**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>About Me</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>About Me</h1>
  <p>Hi! I'm learning CSS and web development.</p>
  <h2>My Skills</h2>
  <ul>
    <li>HTML</li>
    <li>CSS (learning now!)</li>
    <li>JavaScript (coming soon)</li>
  </ul>
</body>
</html>
```

**CSS (styles.css - Complete this):**
```css
/* Your CSS here */
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**CSS (styles.css):**
```css
/* Page Background */
body {
  background-color: #f4f4f4; /* Light gray background */
  font-family: Arial, sans-serif; /* Clean, readable font */
  padding: 40px; /* Space around content */
}

/* Main Heading */
h1 {
  color: #2c3e50; /* Dark blue-gray */
  font-size: 36px; /* Large heading */
  text-align: center; /* Centered */
  margin-bottom: 20px; /* Space below */
}

/* Paragraph */
p {
  color: #555; /* Medium gray */
  font-size: 18px; /* Readable size */
  line-height: 1.6; /* Comfortable spacing between lines */
  margin-bottom: 30px; /* Space below */
}

/* Subheading */
h2 {
  color: #3498db; /* Blue */
  font-size: 24px;
  margin-bottom: 15px;
}

/* List */
ul {
  list-style: none; /* Remove default bullets */
  padding: 0; /* Remove default padding */
}

li {
  background-color: #3498db; /* Blue background */
  color: white; /* White text */
  padding: 12px; /* Inner spacing */
  margin-bottom: 10px; /* Space between items */
  border-radius: 5px; /* Rounded corners */
}
```

**Explanation:**
This solution demonstrates:
- External CSS linking
- Basic selectors (element selectors: `body`, `h1`, `p`, `ul`, `li`)
- Color properties (background, text)
- Typography properties (font-family, font-size, line-height)
- Spacing properties (padding, margin)
- Modern design touches (border-radius for rounded corners)

The page now has a clean, professional look with:
- Light gray background
- Centered dark heading
- Readable paragraph with good line spacing
- Styled list items that look like buttons

</details>

---

### Expected Result

**Visual Outcome:** A clean, professional-looking page with:
- Light gray background
- Large, centered heading in dark blue-gray
- Readable paragraph text
- Blue styled list items with rounded corners

**Key Learnings:**
- How to link external CSS to HTML
- Using element selectors to target HTML tags
- Applying colors, fonts, and spacing
- Creating a cohesive design with consistent styling

---

## Navigation

**Previous:** ← First Topic
**Next:** [CSS Syntax →](syntax.md)
**Up:** [↑ Back to Fundamentals](../)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Fundamentals
**Difficulty:** Beginner
