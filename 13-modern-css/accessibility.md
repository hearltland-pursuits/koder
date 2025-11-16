---
title: CSS Accessibility
category: Modern CSS
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Accessibility

> **Quick Summary:** CSS accessibility ensures websites are usable by people with disabilities. Key areas: color contrast (WCAG AA/AAA), focus states, reduced motion, screen reader compatibility, keyboard navigation, and semantic styling.

## Table of Contents
- [Introduction](#introduction)
- [Color Contrast](#color-contrast)
- [Focus States](#focus-states)
- [Reduced Motion](#reduced-motion)
- [Text Accessibility](#text-accessibility)
- [Screen Reader Compatibility](#screen-reader-compatibility)
- [Keyboard Navigation](#keyboard-navigation)
- [Skip Links](#skip-links)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Web accessibility (a11y)** means designing for ALL users, including those with:
- Visual impairments (blindness, low vision, color blindness)
- Motor disabilities (can't use mouse)
- Cognitive disabilities
- Hearing impairments

**Legal requirement:** ADA (USA), AODA (Canada), EAA (EU) require WCAG compliance.

**WCAG Levels:**
- **Level A:** Minimum (basic accessibility)
- **Level AA:** Standard (most laws require this) ✅ **Target this**
- **Level AAA:** Enhanced (ideal but not always required)

---

## Color Contrast

### WCAG Contrast Requirements

**Text:**
- **Normal text:** 4.5:1 contrast ratio (AA), 7:1 (AAA)
- **Large text** (18px+ or 14px+ bold): 3:1 (AA), 4.5:1 (AAA)

**Non-text:**
- **UI components:** 3:1 contrast ratio (AA)

---

### Good Contrast Examples

```css
/* ✅ Good: 7.5:1 contrast ratio */
.text-primary {
  color: #212529; /* Very dark gray */
  background: #ffffff; /* White */
}

/* ✅ Good: 4.8:1 contrast ratio */
.button {
  color: #ffffff; /* White */
  background: #0066cc; /* Blue */
}

/* ❌ Bad: 2.1:1 contrast ratio (fails AA) */
.text-gray {
  color: #999999; /* Light gray */
  background: #ffffff; /* White */
}
```

---

### Testing Contrast

**Tools:**
- **Chrome DevTools:** Inspect element → Color picker shows contrast ratio
- **WebAIM Contrast Checker:** https://webaim.org/resources/contrastchecker/
- **Lighthouse:** Accessibility audit

**Example:**
```css
/* Check in DevTools */
.element {
  color: #6c757d; /* Inspect this */
  background: white;
}
/* DevTools will show: Contrast ratio: 4.54 ✅ (passes AA) */
```

---

### Color Blindness Considerations

```css
/* ❌ Bad: Only relies on color */
.error {
  color: red; /* Color-blind users may miss this */
}

/* ✅ Good: Color + icon + text */
.error {
  color: #dc3545;
}

.error::before {
  content: '⚠ '; /* Visual indicator */
}
```

**Types of color blindness:**
- **Protanopia:** Can't see red
- **Deuteranopia:** Can't see green
- **Tritanopia:** Can't see blue
- **Achromatopsia:** No color (rare)

**Test with:** Chrome DevTools → Rendering → Emulate vision deficiencies

---

## Focus States

### Visible Focus Indicators

```css
/* ❌ NEVER DO THIS */
*:focus {
  outline: none; /* Removes accessibility */
}

/* ✅ Always provide visible focus */
a:focus,
button:focus,
input:focus {
  outline: 2px solid #0066cc;
  outline-offset: 2px;
}

/* ✅ Or custom focus ring */
.button:focus {
  outline: none; /* OK if replaced */
  box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.5);
}
```

---

### focus-visible (Modern)

**Show focus only for keyboard navigation**, not mouse clicks.

```css
/* No focus ring on click */
button:focus {
  outline: none;
}

/* Focus ring only for keyboard */
button:focus-visible {
  outline: 2px solid #0066cc;
  outline-offset: 2px;
}
```

**Browser support:** Chrome 86+, Firefox 85+, Safari 15.4+

---

### Custom Focus Styles

```css
/* High-contrast focus */
.link:focus-visible {
  outline: 3px dashed #ff6b6b;
  outline-offset: 4px;
  background: #fff3cd;
}

/* Animated focus ring */
.button:focus-visible {
  outline: none;
  box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.5);
  animation: pulse-focus 1s infinite;
}

@keyframes pulse-focus {
  0%, 100% {
    box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.5);
  }
  50% {
    box-shadow: 0 0 0 6px rgba(0, 102, 204, 0.3);
  }
}
```

---

## Reduced Motion

### prefers-reduced-motion

**Respect user's motion preference** (Settings → Accessibility → Reduce Motion).

```css
/* Default: Animations enabled */
.element {
  transition: transform 0.3s ease;
}

.element:hover {
  transform: scale(1.1);
}

/* User prefers reduced motion: Disable animations */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

---

### Conditional Animations

```css
/* Only animate if user allows motion */
.card {
  transition: none; /* Default: No animation */
}

@media (prefers-reduced-motion: no-preference) {
  .card {
    transition: transform 0.3s ease;
  }

  .card:hover {
    transform: translateY(-5px);
  }
}
```

---

## Text Accessibility

### Font Size

```css
/* ❌ Bad: Fixed pixel sizes prevent zooming */
body {
  font-size: 14px;
}

/* ✅ Good: Relative units respect user preferences */
body {
  font-size: 1rem; /* User can zoom */
}

h1 {
  font-size: 2.5rem; /* Scales with user zoom */
}
```

---

### Line Height and Spacing

```css
/* WCAG recommendations */
body {
  font-size: 16px; /* Minimum for body text */
  line-height: 1.5; /* WCAG: At least 1.5 for paragraphs */
  letter-spacing: normal; /* WCAG: At least 0.12x font size */
  word-spacing: normal; /* WCAG: At least 0.16x font size */
}

p {
  margin-bottom: 1em; /* Space between paragraphs */
}
```

---

### Text Readability

```css
/* ✅ Good: High contrast, readable font */
.content {
  font-family: 'Segoe UI', Arial, sans-serif;
  font-size: 18px; /* Larger for readability */
  line-height: 1.6;
  color: #212529;
  background: #ffffff;
  max-width: 70ch; /* 70 characters per line (optimal readability) */
}

/* ❌ Bad: Low contrast, tiny text */
.content-bad {
  font-size: 12px;
  color: #999;
  line-height: 1.2;
}
```

---

## Screen Reader Compatibility

### Visually Hidden (Screen Reader Only)

```css
/* ✅ Hide visually, but accessible to screen readers */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}

/* Use for icon-only buttons */
.icon-button {
  /* Visual icon */
}

.icon-button .sr-only {
  /* Screen reader text: "Close menu" */
}
```

**HTML:**
```html
<button class="icon-button">
  <svg><!-- Icon --></svg>
  <span class="sr-only">Close menu</span>
</button>
```

---

### Display: none vs Visibility: hidden

```css
/* ❌ Hidden from screen readers too */
.hidden {
  display: none; /* Screen readers ignore this */
}

/* ✅ Hidden visually, but screen readers can access */
.visually-hidden {
  visibility: hidden; /* Only hides visually */
  position: absolute;
}

/* ✅ Or use .sr-only class above */
```

---

## Keyboard Navigation

### Tab Order

```css
/* Elements with tabindex are focusable */

/* Default: Natural tab order (DOM order) */
/* tabindex="0" = Include in natural order */
/* tabindex="-1" = Not in tab order, but focusable via JS */
/* tabindex="1+" = Custom order (avoid, breaks expectations) */
```

**HTML:**
```html
<!-- ✅ Good: Natural order -->
<nav>
  <a href="#home">Home</a>
  <a href="#about">About</a>
  <a href="#contact">Contact</a>
</nav>

<!-- ❌ Bad: Custom tab order (confusing) -->
<a href="#contact" tabindex="3">Contact</a>
<a href="#home" tabindex="1">Home</a>
<a href="#about" tabindex="2">About</a>
```

---

### Interactive Element Sizing

```css
/* WCAG: Touch targets must be at least 44×44px */
button,
a,
input[type="checkbox"],
input[type="radio"] {
  min-width: 44px;
  min-height: 44px;
}

/* Or use padding to increase clickable area */
.link {
  padding: 12px 16px; /* Makes link larger */
}
```

---

## Skip Links

**Allow keyboard users to skip navigation** and jump to main content.

### Implementation

```html
<body>
  <a href="#main-content" class="skip-link">Skip to main content</a>

  <nav>
    <!-- Long navigation -->
  </nav>

  <main id="main-content">
    <!-- Main content -->
  </main>
</body>
```

```css
/* Hidden by default */
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  background: #000;
  color: #fff;
  padding: 8px 16px;
  text-decoration: none;
  z-index: 1000;
}

/* Visible when focused */
.skip-link:focus {
  top: 0;
}
```

---

## Best Practices

### ✅ Do This

1. **Always provide focus states**
   ```css
   button:focus-visible {
     outline: 2px solid #0066cc;
   }
   ```

2. **Use sufficient contrast (4.5:1 minimum)**
   ```css
   color: #212529;
   background: #ffffff;
   /* Contrast: 16.1:1 ✅ */
   ```

3. **Respect prefers-reduced-motion**
   ```css
   @media (prefers-reduced-motion: reduce) {
     * {
       animation: none !important;
       transition: none !important;
     }
   }
   ```

4. **Use relative units (rem, em)**
   ```css
   font-size: 1rem; /* Respects user zoom */
   ```

5. **Provide text alternatives for icons**
   ```html
   <button>
     <svg><!-- Icon --></svg>
     <span class="sr-only">Delete</span>
   </button>
   ```

6. **Make touch targets 44×44px minimum**
   ```css
   button {
     min-width: 44px;
     min-height: 44px;
   }
   ```

---

### ❌ Avoid This

1. **Don't remove focus outlines**
   ```css
   /* NEVER */
   *:focus {
     outline: none;
   }
   ```

2. **Don't use color alone to convey meaning**
   ```css
   /* Bad: Color-blind users miss this */
   .required {
     color: red;
   }

   /* Good: Add asterisk */
   .required::after {
     content: ' *';
     color: red;
   }
   ```

3. **Don't use fixed pixel fonts**
   ```css
   /* Prevents user zoom */
   font-size: 14px;
   ```

4. **Don't hide content with display: none if screen readers need it**
   ```css
   /* Screen readers can't access */
   .hidden {
     display: none;
   }
   ```

5. **Don't set max font size**
   ```css
   /* Prevents zooming */
   html {
     font-size: 16px;
     max-font-size: 20px; /* Don't do this */
   }
   ```

---

## Testing Tools

### Browser Extensions

- **axe DevTools** (Chrome/Firefox)
- **WAVE** (WebAIM)
- **Lighthouse** (Chrome DevTools)

### Screen Readers

- **NVDA** (Windows, free)
- **JAWS** (Windows, paid)
- **VoiceOver** (Mac/iOS, built-in)
- **TalkBack** (Android, built-in)

### Contrast Checkers

- **Chrome DevTools** (inspect color picker)
- **WebAIM Contrast Checker**
- **Colour Contrast Analyser** (desktop app)

### Keyboard Testing

**Test navigation:**
1. Unplug mouse
2. Use only Tab, Shift+Tab, Enter, Space
3. Verify all interactive elements are reachable
4. Check focus indicators are visible

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `:focus-visible` | 86+ | 85+ | 15.4+ | 86+ |
| `prefers-reduced-motion` | 74+ | 63+ | 10.1+ | 79+ |
| `prefers-color-scheme` | 76+ | 67+ | 12.1+ | 79+ |

---

## Related Topics

**Prerequisites:**
- [CSS Fundamentals](../01-fundamentals/syntax.md)
- [Media Queries](../12-responsive-design/media-queries.md)

**Next Steps:**
- [ARIA Attributes](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA)
- [WCAG Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)

---

## Practice Exercise

Accessibility audit:
1. Run Lighthouse accessibility audit
2. Check all links/buttons have focus states
3. Test keyboard navigation (unplug mouse)
4. Verify color contrast (4.5:1 minimum)
5. Add skip link
6. Test with screen reader (VoiceOver/NVDA)
7. Add prefers-reduced-motion support

Target: 100 accessibility score in Lighthouse

---

## Navigation

**Previous:** [← Optimization](optimization.md)
**Next:** [Course Complete! 🎉](../README.md)
**Up:** [↑ Back to Modern CSS](../README.md#1️⃣3️⃣-modern-css-5-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Modern CSS
**Difficulty:** Intermediate
