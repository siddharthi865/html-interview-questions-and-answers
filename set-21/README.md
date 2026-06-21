# Set 21

| S.No. | Question                                                                                                                                                          |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What happens if you place `<html>` tag inside `<body>`?](#question-1-what-happens-if-you-place-html-tag-inside-body)                                             |
| 2.    | [Can an HTML document have multiple `<head>` tags?](#question-2-can-an-html-document-have-multiple-head-tags)                                                     |
| 3.    | [Can an HTML document have multiple `<body>` tags?](#question-3-can-an-html-document-have-multiple-body-tags)                                                     |
| 4.    | [What happens if `<title>` is missing?](#question-4-what-happens-if-title-is-missing)                                                                             |
| 5.    | [What happens if `<meta charset>` is placed at the bottom of the head?](#question-5-what-happens-if-meta-charset-is-placed-at-the-bottom-of-the-head)             |
| 6.    | [What is the parsing behavior of self-closing tags in HTML vs XHTML?](#question-6-what-is-the-parsing-behavior-of-self-closing-tags-in-html-vs-xhtml)             |
| 7.    | [Why does `<script />` not self-close in HTML?](#question-7-why-does-script--not-self-close-in-html)                                                              |
| 8.    | [What is the adoption agency algorithm in HTML parsing?](#question-8-what-is-the-adoption-agency-algorithm-in-html-parsing)                                       |
| 9.    | [What is foster parenting in HTML parsing?](#question-9-what-is-foster-parenting-in-html-parsing)                                                                 |
| 10.   | [What happens if you nest interactive elements (e.g., button inside anchor)?](#question-10-what-happens-if-you-nest-interactive-elements-eg-button-inside-anchor) |
| 11.   | [What are interactive content categories?](#question-11-what-are-interactive-content-categories)                                                                  |
| 12.   | [What is phrasing content?](#question-12-what-is-phrasing-content)                                                                                                |
| 13.   | [What is flow content?](#question-13-what-is-flow-content)                                                                                                        |
| 14.   | [What is sectioning content?](#question-14-what-is-sectioning-content)                                                                                            |
| 15.   | [What is heading content?](#question-15-what-is-heading-content)                                                                                                  |
| 16.   | [What defines palpable content?](#question-16-what-defines-palpable-content)                                                                                      |
| 17.   | [What is transparent content model?](#question-17-what-is-transparent-content-model)                                                                              |
| 18.   | [What is metadata content category?](#question-18-what-is-metadata-content-category)                                                                              |
| 19.   | [What are embedded content categories?](#question-19-what-are-embedded-content-categories)                                                                        |
| 20.   | [What are form-associated elements?](#question-20-what-are-form-associated-elements)                                                                              |

## Question 1. What happens if you place `<html>` tag inside `<body>`?

# Short answer

Placing an `<html>` tag inside the `<body>` is **invalid HTML**. Browsers will invoke HTML error-recovery (the parser's error-handling algorithm) and typically **ignore or reparent the misplaced `<html>` element** rather than creating a second document root. The page may still render, but the DOM will not match the source code exactly, and behavior is not something you should rely on.

---

# Explanation

The `<html>` element is the **document root** and must be the top-level element of an HTML document. A valid document structure is:

```html
<!DOCTYPE html>
<html>
  <head>
    ...
  </head>
  <body>
    ...
  </body>
</html>
```

If you write:

```html
<body>
  <p>Hello</p>
  <html>
    <p>Invalid</p>
  </html>
</body>
```

the HTML parser treats this as a parse error.

### What browsers do

Modern browsers follow the HTML parsing algorithm, which is designed to recover from malformed markup.

Typical behavior:

- The second `<html>` tag **does not create another document root**.
- The parser ignores the misplaced root element or merges its attributes with the existing root where appropriate.
- Its children are usually parsed as though they appeared directly in the body.
- The rendered page often appears "correct," even though the markup is invalid.

For example, the DOM may effectively become:

```html
<html>
  <head></head>
  <body>
    <p>Hello</p>
    <p>Invalid</p>
  </body>
</html>
```

rather than containing a nested `<html>` element.

### Why this happens

HTML is intentionally **fault-tolerant**. Unlike XML, browsers don't stop parsing when they encounter invalid markup. Instead, they follow standardized error-recovery rules so users can still view webpages.

---

# Example

**Invalid HTML**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Example</title>
  </head>
  <body>
    <h1>Main Page</h1>

    <html>
      <p>This is invalid HTML.</p>
    </html>
  </body>
</html>
```

**What the browser effectively interprets**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Example</title>
  </head>
  <body>
    <h1>Main Page</h1>
    <p>This is invalid HTML.</p>
  </body>
</html>
```

---

# Accessibility & SEO

### Accessibility

- Screen readers rely on the browser's parsed DOM, not the original source.
- Since browsers repair the markup, assistive technologies usually receive a valid document tree.
- However, malformed HTML can cause unexpected accessibility issues if parser recovery differs across browsers.
- No ARIA role can compensate for an invalid document structure.

### SEO

- Search engines also parse malformed HTML using browser-like parsers.
- They usually recover successfully, but invalid markup may:
  - confuse automated tools,
  - affect structured data extraction,
  - reduce maintainability.

- Always keep a single `<html>` root element.

---

# Integration & Trade-offs

### CSS

- CSS selectors like:

```css
html {
  font-size: 16px;
}
```

always target the document's single root element. A nested `<html>` element won't behave as another root.

### JavaScript

```javascript
document.documentElement;
```

always references the actual document root.

Code like:

```javascript
document.querySelector("html");
```

returns the root `<html>` element—not an invalid nested one that the parser discarded or reparented.

### Frameworks (React/Vue/Angular)

- Components should **never** render `<html>`, `<head>`, or `<body>` inside application components.
- Frameworks expose dedicated APIs for managing the document root and metadata (for example, React frameworks often provide document or head management mechanisms).
- Server-side rendering depends on a valid document structure; malformed root elements can lead to hydration mismatches or unexpected parsing before JavaScript runs.

### Progressive Enhancement

Progressive enhancement assumes valid HTML. Invalid document structure may work today because browsers recover gracefully, but it is not guaranteed behavior and should never be relied upon.

---

# Testing & Validation

- Validate markup using the WHATWG/W3C HTML validator.
- Inspect the DOM in browser DevTools—you'll notice the nested `<html>` element is not preserved as written.
- Run accessibility audits with tools like axe DevTools or Lighthouse to catch structural issues.
- Include HTML validation in CI/CD for server-rendered pages or generated templates.

---

# Pitfalls

- **Assuming a second `<html>` element creates another document**—it does not.
- **Relying on browser error recovery** instead of writing valid HTML.
- **Rendering `<html>` from reusable components or templates**, resulting in invalid markup and possible SSR/hydration issues.

## Question 2. Can an HTML document have multiple `<head>` tags?

## Question 3. Can an HTML document have multiple `<body>` tags?

## Question 4. What happens if `<title>` is missing?

## Question 5. What happens if `<meta charset>` is placed at the bottom of the head?

## Question 6. What is the parsing behavior of self-closing tags in HTML vs XHTML?

## Question 7. Why does `<script />` not self-close in HTML?

## Question 8. What is the adoption agency algorithm in HTML parsing?

## Question 9. What is foster parenting in HTML parsing?

## Question 10. What happens if you nest interactive elements (e.g., button inside anchor)?

## Question 11. What are interactive content categories?

## Question 12. What is phrasing content?

## Question 13. What is flow content?

## Question 14. What is sectioning content?

## Question 15. What is heading content?

## Question 16. What defines palpable content?

## Question 17. What is transparent content model?

## Question 18. What is metadata content category?

## Question 19. What are embedded content categories?

## Question 20. What are form-associated elements?
