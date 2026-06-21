# Set 5

| S.No. | Question                                                                                                                                             |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [How does browser rendering work with HTML?](#question-1-how-does-browser-rendering-work-with-html)                                                  |
| 2.    | [What is critical rendering path?](#question-2-what-is-critical-rendering-path)                                                                      |
| 3.    | [What is progressive enhancement?](#question-3-what-is-progressive-enhancement)                                                                      |
| 4.    | [What is graceful degradation?](#question-4-what-is-graceful-degradation)                                                                            |
| 5.    | [What is web accessibility?](#question-5-what-is-web-accessibility)                                                                                  |
| 6.    | [What are ARIA roles?](#question-6-what-are-aria-roles)                                                                                              |
| 7.    | [What is the difference between `aria-label` and `aria-labelledby`?](#question-7-what-is-the-difference-between-aria-label-and-aria-labelledby)      |
| 8.    | [How do you make a website accessible?](#question-8-how-do-you-make-a-website-accessible)                                                            |
| 9.    | [What is tabindex?](#question-9-what-is-tabindex)                                                                                                    |
| 10.   | [What is the purpose of alt text for screen readers?](#question-10-what-is-the-purpose-of-alt-text-for-screen-readers)                               |
| 11.   | [What is Web Storage API?](#question-11-what-is-web-storage-api)                                                                                     |
| 12.   | [What is the difference between localStorage and sessionStorage?](#question-12-what-is-the-difference-between-localstorage-and-sessionstorage)       |
| 13.   | [What is the Geolocation API?](#question-13-what-is-the-geolocation-api)                                                                             |
| 14.   | [What is the Canvas API?](#question-14-what-is-the-canvas-api)                                                                                       |
| 15.   | [What is the difference between SVG and Canvas?](#question-15-what-is-the-difference-between-svg-and-canvas)                                         |
| 16.   | [What is the contenteditable attribute?](#question-16-what-is-the-contenteditable-attribute)                                                         |
| 17.   | [What is the draggable attribute?](#question-17-what-is-the-draggable-attribute)                                                                     |
| 18.   | [What is the sandbox attribute in iframes?](#question-18-what-is-the-sandbox-attribute-in-iframes)                                                   |
| 19.   | [What are custom data attributes used for in JavaScript frameworks?](#question-19-what-are-custom-data-attributes-used-for-in-javascript-frameworks) |
| 20.   | [What are Web Components?](#question-20-what-are-web-components)                                                                                     |

## Question 1. How does browser rendering work with HTML?

# Short answer

Browser rendering is the process of turning HTML, CSS, and JavaScript into pixels on the screen. In simplified terms:

1. Parse HTML → build the **DOM (Document Object Model)**.
2. Parse CSS → build the **CSSOM (CSS Object Model)**.
3. Combine DOM + CSSOM → create the **Render Tree**.
4. Calculate layout (size and position of elements).
5. Paint pixels to layers.
6. Composite layers and display the final page.

JavaScript can modify the DOM, CSSOM, or both, causing parts of this pipeline to run again.

---

# Explanation

A modern browser rendering engine (such as the one used in [Google Chrome](https://www.google.com/chrome/?utm_source=chatgpt.com)) follows a pipeline similar to:

```text
HTML
  ↓
DOM
  ↓
DOM + CSSOM
  ↓
Render Tree
  ↓
Layout (Reflow)
  ↓
Paint
  ↓
Composite
  ↓
Screen
```

## 1. HTML Parsing → DOM

The browser receives HTML and parses it into a tree structure called the DOM.

HTML:

```html
<body>
  <h1>Hello</h1>
  <p>Welcome</p>
</body>
```

DOM:

```text
Document
 └── body
      ├── h1
      └── p
```

Semantic HTML (`<header>`, `<main>`, `<article>`, etc.) helps browsers, accessibility tools, and search engines understand document structure.

---

## 2. CSS Parsing → CSSOM

The browser parses CSS into another tree called the CSSOM.

```css
h1 {
  color: blue;
}
```

The CSSOM contains all style rules, selectors, inheritance, and computed values.

CSS is render-blocking by default because the browser generally needs styles before it can accurately render content.

---

## 3. DOM + CSSOM → Render Tree

The browser combines:

- DOM structure
- Computed CSS styles

to create the Render Tree.

Important:

- Elements with `display: none` are excluded.
- Elements with `visibility: hidden` remain in the layout but are not visible.

Example:

```html
<p>Hello</p>
<p style="display:none">Hidden</p>
```

Only the first paragraph appears in the Render Tree.

---

## 4. Layout (Reflow)

The browser calculates:

- Width
- Height
- Position
- Margins
- Padding

for every visible element.

Example:

```html
<div class="card">Content</div>
```

The browser determines exactly where the `.card` appears and how much space it occupies.

Layout is one of the most expensive rendering operations.

---

## 5. Paint

The browser converts layout information into actual pixels:

- Text
- Colors
- Borders
- Shadows
- Images

Example:

```css
.card {
  background: white;
  border: 1px solid #ccc;
}
```

The browser paints these visual properties onto layers.

---

## 6. Compositing

Modern browsers often place certain elements on separate layers (for example, transformed or animated elements).

The GPU combines these layers into the final frame displayed on screen.

This is why animations using:

```css
transform
opacity
```

are usually smoother than animations that trigger layout changes.

---

## Example

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Rendering Example</title>
    <style>
      h1 {
        color: blue;
      }
    </style>
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

What happens:

1. HTML parsed → DOM created.
2. CSS parsed → CSSOM created.
3. Browser builds Render Tree.
4. Layout determines heading position.
5. Paint draws blue text.
6. Composite displays the page.

---

# Accessibility & SEO

## Accessibility

Rendering affects accessibility because browsers also create an **Accessibility Tree** from the DOM.

Semantic HTML:

```html
<header>
  <main>
    <nav>
      <button></button>
    </nav>
  </main>
</header>
```

helps screen readers understand page structure without additional ARIA.

Prefer:

```html
<button>Save</button>
```

instead of:

```html
<div role="button">Save</div>
```

unless there is a compelling reason.

### Accessibility Tree

The browser generates:

```text
DOM
 ├── Accessibility Tree
 └── Render Tree
```

Some elements may exist in one tree but not the other.

Example:

```html
<div aria-hidden="true">Hidden from screen readers</div>
```

---

## SEO

Search engines primarily process the DOM.

Good rendering practices:

- Use semantic HTML.
- Ensure content exists in the HTML when possible.
- Include meaningful headings (`<h1>`–`<h6>`).
- Use descriptive links.
- Provide metadata:

```html
<title>Product Page</title>
<meta name="description" content="Product details" />
```

Server-side rendered HTML is generally easier for crawlers to process than content that appears only after extensive client-side JavaScript execution.

---

# Integration & Trade-offs

## HTML + CSS

CSS affects:

- Render Tree creation
- Layout
- Paint

Heavy selectors and large stylesheets can delay rendering.

---

## HTML + JavaScript

JavaScript can:

```javascript
document.body.append("Hello");
```

which updates the DOM and may trigger:

- Recalculate Style
- Layout
- Paint
- Composite

depending on the change.

---

## SPA Frameworks

Frameworks such as React, Vue, and Angular typically:

1. Render components.
2. Update a virtual representation.
3. Apply minimal DOM changes.

This reduces expensive browser work.

---

## SSR vs CSR

### Server-Side Rendering (SSR)

Server sends ready-to-render HTML.

Benefits:

- Faster first paint
- Better SEO
- Better perceived performance

### Client-Side Rendering (CSR)

Server sends minimal HTML and JavaScript.

Benefits:

- Rich interactivity
- SPA experience

Trade-off:

- Slower initial render
- More JavaScript execution

Modern frameworks often use hybrid rendering.

---

## Progressive Enhancement

Start with functional HTML:

```html
<form action="/search"></form>
```

Then enhance with CSS and JavaScript.

Benefits:

- Faster rendering
- Better accessibility
- More resilient experience

---

# Testing & Validation

### HTML Validation

Use:

- [W3C Markup Validator](https://validator.w3.org/?utm_source=chatgpt.com)

Check for:

- Invalid nesting
- Missing attributes
- Semantic issues

### Performance Analysis

Use:

- [Chrome DevTools Performance Panel](https://developer.chrome.com/docs/devtools/performance/?utm_source=chatgpt.com)
- [Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/?utm_source=chatgpt.com)

Look for:

- Layout shifts
- Render-blocking resources
- Long JavaScript tasks

### Accessibility Testing

Use:

- [axe DevTools](https://www.deque.com/axe/devtools/?utm_source=chatgpt.com)
- Lighthouse Accessibility audits

Verify:

- Semantic structure
- Keyboard navigation
- Screen-reader behavior

---

# Pitfalls

- **Triggering unnecessary reflows** by repeatedly reading and writing layout-related properties (`offsetWidth`, `clientHeight`) inside loops.
- **Blocking rendering with large CSS or synchronous JavaScript**, delaying first paint.
- **Using non-semantic elements for interactive controls** (`div` instead of `button`), which hurts accessibility and increases implementation complexity.

## Question 2. What is critical rendering path?

## Question 3. What is progressive enhancement?

## Question 4. What is graceful degradation?

## Question 5. What is web accessibility?

## Question 6. What are ARIA roles?

## Question 7. What is the difference between `aria-label` and `aria-labelledby`?

## Question 8. How do you make a website accessible?

## Question 9. What is tabindex?

## Question 10. What is the purpose of alt text for screen readers?

## Question 11. What is Web Storage API?

## Question 12. What is the difference between localStorage and sessionStorage?

## Question 13. What is the Geolocation API?

## Question 14. What is the Canvas API?

## Question 15. What is the difference between SVG and Canvas?

## Question 16. What is the contenteditable attribute?

## Question 17. What is the draggable attribute?

## Question 18. What is the sandbox attribute in iframes?

## Question 19. What are custom data attributes used for in JavaScript frameworks?

## Question 20. What are Web Components?
