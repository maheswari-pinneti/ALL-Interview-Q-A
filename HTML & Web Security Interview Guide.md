# HTML & Web Security Interview Guide

## Table of Contents
- [Advanced HTML Questions](#advanced-html-questions)
  - [Document Lifecycle](#1-html-document-lifecycle)
  - [Error Handling](#2-browser-handling-of-invalid-html)
  - [Web Components](#3-web-components-custom-elements-shadow-dom-templates)
  - [Responsive Images](#4-picture-element)
  - [Dialog Element](#5-dialog-element)
- [HTML Security](#html-security-questions)
  - [Common Vulnerabilities](#1-common-html-security-vulnerabilities)
  - [CSP](#2-content-security-policy-csp)
  - [Sanitization](#3-html-sanitization)
  - [SRI](#4-subresource-integrity-sri)
  - [Form Security](#5-securing-html-forms)

---

## Advanced HTML Questions

### 1. HTML Document Lifecycle
```html
<!DOCTYPE html>
<html>
<head>
    <!-- Parsing starts here -->
    <title>Lifecycle Example</title>
</head>
<body>
    <!-- DOM construction -->
    <div id="content"></div>
    
    <script>
        // Render-blocking example
        document.getElementById('content').innerHTML = 'Loaded';
    </script>
</body>
</html>
```
**Key Phases**:
1. 🏗️ **Parsing**: Byte → Characters → Tokens → Nodes → DOM
2. 🌳 **CSSOM**: Parallel CSS parsing
3. 🖼️ **Render Tree**: DOM + CSSOM combination
4. 📐 **Layout**: Calculate element positions
5. 🎨 **Paint**: Pixel rendering

---

### 2. Browser Handling of Invalid HTML
**Error Recovery Examples**:
```html
<!-- Unclosed tag -->
<p>Hello → <p>Hello</p> (Auto-closed)

<!-- Misordered tags -->
<p><span>Text</p></span> → <p><span>Text</span></p>

<!-- Deprecated elements -->
<marquee> → Treated as unknown element
```

---

### 3. Web Components (Custom Elements, Shadow DOM, Templates)
```javascript
class MyCounter extends HTMLElement {
  constructor() {
    super();
    const shadow = this.attachShadow({ mode: 'open' });
    shadow.innerHTML = `
      <style>
        button { color: red; }
      </style>
      <button id="count">0</button>
    `;
  }
}
customElements.define('my-counter', MyCounter);
```
**Key Features**:
- 🔒 **Encapsulation**: Shadow DOM isolates styles
- ♻️ **Reusability**: Templates with `<slot>`
- 🏷️ **Semantics**: Custom element names

---

### 4. Picture Element
```html
<picture>
  <source media="(min-width: 1200px)" srcset="large.webp" type="image/webp">
  <source media="(min-width: 800px)" srcset="medium.jpg">
  <img src="small.jpg" alt="Responsive" loading="lazy">
</picture>
```
**Use Cases**:
- Art direction changes
- Next-gen format fallbacks
- Bandwidth optimization

---

### 5. Dialog Element
```html
<dialog id="modal">
  <h2>Native Modal!</h2>
  <button onclick="modal.close()">Close</button>
</dialog>

<button onclick="modal.showModal()">Open</button>
```
**Benefits**:
- ⚡ Built-in accessibility
- 🎨 `::backdrop` pseudo-element
- 🔐 Focus trapping

---

## HTML Security Questions

### 1. Common HTML Security Vulnerabilities
| Vulnerability | Example | Prevention |
|--------------|---------|------------|
| **XSS** | `<script>alert(1)</script>` | CSP, Sanitization |
| **CSRF** | Hidden form submission | SameSite cookies, Tokens |
| **Clickjacking** | Transparent iframe overlays | `X-Frame-Options` |
| **HTML Injection** | `<img src=x onerror=attack>` | Output encoding |

---

### 2. Content Security Policy (CSP)
```html
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; 
               script-src 'self' https://apis.example.com;
               style-src 'unsafe-inline'">
```
**Directives**:
- `connect-src`: XHR/fetch sources
- `font-src`: Webfont origins
- `frame-src`: Embedded iframe sources

---

### 3. HTML Sanitization
**JavaScript**:
```javascript
// Using DOMPurify
const clean = DOMPurify.sanitize(userInput, {
  ALLOWED_TAGS: ['b', 'i', 'em'],
  FORBID_ATTR: ['style', 'onclick']
});
```

**PHP**:
```php
$safe = htmlspecialchars($input, ENT_QUOTES, 'UTF-8');
```

---

### 4. Subresource Integrity (SRI)
```html
<script src="https://example.com/library.js"
        integrity="sha384-{HASH}"
        crossorigin="anonymous"></script>
```
**Generating Hashes**:
```bash
openssl dgst -sha384 -binary library.js | openssl base64 -A
```

---

### 5. Securing HTML Forms
```html
<form method="POST" action="/submit">
  <!-- CSRF Protection -->
  <input type="hidden" name="_csrf" value="token123">
  
  <!-- Input Validation -->
  <input type="email" name="email" required 
         pattern="[^@]+@[^@]+\.[^@]+">
  
  <!-- Security Headers -->
  <meta http-equiv="X-Content-Type-Options" content="nosniff">
</form>
```

**Additional Measures**:
- 🔄 Rate limiting
- 🛡️ Honeypot fields
- 📛 CAPTCHA integration

---

## Tools & Resources
1. [CSP Evaluator](https://csp-evaluator.withgoogle.com)
2. [DOMPurify](https://github.com/cure53/DOMPurify)
3. [OWASP Cheatsheets](https://cheatsheetseries.owasp.org)


This Markdown document:
- Uses GitHub-flavored syntax
- Includes code blocks with syntax highlighting
- Contains tables for vulnerability comparisons
- Has clear section headers
- Provides executable code examples
- Uses emojis for visual scanning

