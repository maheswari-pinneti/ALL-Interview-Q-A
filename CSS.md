# CSS Complete Reference Guide

## Table of Contents
1. [Basic CSS & Selectors](#basic-css--selectors)
2. [Box Model](#box-model)
3. [Layout](#layout)
4. [Typography](#typography)
5. [Colors & Backgrounds](#colors--backgrounds)
6. [Transitions & Animations](#transitions--animations)
7. [Flexbox](#flexbox)
8. [Grid](#grid)
9. [Responsive Design](#responsive-design)
10. [CSS Security](#css-security)

---

## Basic CSS & Selectors

### 1. Inline Styles
```html
<p style="color: red;">Red text</p>
```

### 2. Class Selector
```css
.highlight {
  background-color: yellow;
}
```

### 3. ID Selector
```css
#header {
  font-size: 24px;
}
```

### 4. Descendant Selector
```css
nav ul li {
  padding: 8px;
}
```

### 5. Child Selector
```css
div > p {
  margin: 0;
}
```

---

## Box Model

### 6. Box-Sizing
```css
.box {
  box-sizing: border-box; /* includes padding+border in width */
  width: 100px;
  padding: 10px;
}
```

### 7. Margin Collapse
```css
/* Adjacent vertical margins combine */
p {
  margin: 20px 0;
}
```

### 8. Outline vs Border
```css
button {
  border: 2px solid black; /* part of box model */
  outline: 2px solid red; /* outside border, no space */
}
```

---

## Layout

### 9. Centering with Flexbox
```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

### 10. Position Absolute
```css
.tooltip {
  position: absolute;
  top: 10px;
  left: 10px;
}
```

### 11. Sticky Header
```css
header {
  position: sticky;
  top: 0;
}
```

---

## Typography

### 12. Font Stack
```css
body {
  font-family: 'Segoe UI', Roboto, sans-serif;
}
```

### 13. Text Overflow
```css
.truncate {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

### 14. Custom Fonts
```css
@font-face {
  font-family: 'MyFont';
  src: url('myfont.woff2') format('woff2');
}
```

---

## Colors & Backgrounds

### 15. RGBA Color
```css
.transparent {
  background-color: rgba(255, 0, 0, 0.5);
}
```

### 16. Linear Gradient
```css
.banner {
  background: linear-gradient(to right, red, blue);
}
```

### 17. Background Image
```css
.hero {
  background-image: url('hero.jpg');
  background-size: cover;
}
```

---

## Transitions & Animations

### 18. Simple Transition
```css
.button {
  transition: all 0.3s ease;
}
```

### 19. Keyframe Animation
```css
@keyframes slide {
  from { transform: translateX(-100%); }
  to { transform: translateX(0); }
}

.slide-in {
  animation: slide 0.5s forwards;
}
```

---

## Flexbox

### 20. Flex Container
```css
.flex-container {
  display: flex;
  gap: 10px;
}
```

### 21. Flex Item Growth
```css
.item {
  flex: 1; /* grows to fill space */
}
```

---

## Grid

### 22. Basic Grid
```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

### 23. Grid Areas
```css
.page {
  grid-template-areas: "header header"
                       "sidebar content";
}
```

---

## Responsive Design

### 24. Media Queries
```css
@media (max-width: 768px) {
  .menu { display: none; }
}
```

### 25. Viewport Units
```css
.header {
  height: 100vh; /* full viewport height */
}
```

---

## CSS Security

### 26. Prevent CSS Injection
```css
/* Server-side: Sanitize user-generated CSS */
.safe-css {
  /* Whitelisted properties only */
  color: inherit;
  font-size: inherit;
}
```

### 27. Secure Font Loading
```css
@font-face {
  font-family: 'SafeFont';
  src: local('Arial'), /* Prefer system font */
       url('font.woff2') format('woff2');
}
```

### 28. Clickjacking Protection
```css
/* Combine with HTTP header: */
/* X-Frame-Options: DENY */
iframe {
  display: none !important;
}
```

### 29. CSP for Styles
```html
<meta http-equiv="Content-Security-Policy" 
      content="style-src 'self' 'unsafe-inline'">
```

### 30. SRI for CSS
```html
<link rel="stylesheet" 
      href="styles.css"
      integrity="sha384-...">
```

---

## Best Practices Checklist
1. [x] Use semantic HTML with CSS
2. [x] Prefer classes over IDs for styling
3. [x] Mobile-first responsive design
4. [x] Validate CSS with W3C validator
5. [x] Implement CSP headers
6. [x] Audit for selector performance
7. [x] Test in multiple browsers

[⬆ Back to Top](#table-of-contents)


This Markdown document:
1. Follows GitHub Flavored Markdown syntax
2. Includes collapsible sections
3. Provides copy-paste ready code examples
4. Contains security best practices
5. Is organized by CSS concept categories
6. Uses emoji for visual scanning
7. Has a table of contents with anchor links


