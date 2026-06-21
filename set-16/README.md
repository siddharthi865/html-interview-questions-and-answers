# Set 16

| S.No. | Question                                                                                                                                            |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is the difference between HTML Living Standard and HTML5?](#question-1-what-is-the-difference-between-html-living-standard-and-html5)         |
| 2.    | [Who maintains the HTML specification?](#question-2-who-maintains-the-html-specification)                                                           |
| 3.    | [What is the purpose of the WHATWG?](#question-3-what-is-the-purpose-of-the-whatwg)                                                                 |
| 4.    | [What is W3C's role in HTML standardization?](#question-4-what-is-w3cs-role-in-html-standardization)                                                |
| 5.    | [What are deprecated attributes?](#question-5-what-are-deprecated-attributes)                                                                       |
| 6.    | [What are obsolete but conforming features?](#question-6-what-are-obsolete-but-conforming-features)                                                 |
| 7.    | [What are obsolete and non-conforming features?](#question-7-what-are-obsolete-and-non-conforming-features)                                         |
| 8.    | [What is the difference between presentational and semantic markup?](#question-8-what-is-the-difference-between-presentational-and-semantic-markup) |
| 9.    | [Why should we avoid inline styles in HTML?](#question-9-why-should-we-avoid-inline-styles-in-html)                                                 |
| 10.   | [What is character encoding and why is UTF-8 commonly used?](#question-10-what-is-character-encoding-and-why-is-utf-8-commonly-used)                |
| 11.   | [What is tokenization in HTML parsing?](#question-11-what-is-tokenization-in-html-parsing)                                                          |
| 12.   | [What is tree construction stage in parsing?](#question-12-what-is-tree-construction-stage-in-parsing)                                              |
| 13.   | [What is insertion mode in HTML parsing?](#question-13-what-is-insertion-mode-in-html-parsing)                                                      |
| 14.   | [What happens when the parser encounters malformed nesting?](#question-14-what-happens-when-the-parser-encounters-malformed-nesting)                |
| 15.   | [What are optional closing tags?](#question-15-what-are-optional-closing-tags)                                                                      |
| 16.   | [Which HTML tags can omit closing tags?](#question-16-which-html-tags-can-omit-closing-tags)                                                        |
| 17.   | [What are raw text elements?](#question-17-what-are-raw-text-elements)                                                                              |
| 18.   | [What are escapable raw text elements?](#question-18-what-are-escapable-raw-text-elements)                                                          |
| 19.   | [What happens if you put block elements inside `<p>`?](#question-19-what-happens-if-you-put-block-elements-inside-p)                                |
| 20.   | [Why does HTML auto-correct certain structures?](#question-20-why-does-html-auto-correct-certain-structures)                                        |

## Question 1. What is the difference between HTML Living Standard and HTML5?

# Short answer

**HTML5** refers to the major version of HTML that was standardized as a snapshot (primarily the W3C Recommendation published in 2014). **HTML Living Standard** is the continuously updated specification maintained by WHATWG, where new HTML features, APIs, and clarifications are added incrementally instead of waiting for versioned releases.

In modern web development, when people say "HTML5," they usually mean the modern HTML platform, but technically browsers implement the **HTML Living Standard**.

---

# Explanation

Historically, HTML evolved through versioned specifications (HTML 2.0, HTML 4.01, XHTML, HTML5).

### HTML5

- A **versioned specification**.
- Published as a stable recommendation by W3C (2014).
- Represents a snapshot of the language at a specific point in time.
- Introduced major features such as:
  - Semantic elements (`<header>`, `<main>`, `<article>`, `<section>`)
  - Native multimedia (`<audio>`, `<video>`)
  - Canvas
  - Improved forms
  - New APIs

### HTML Living Standard

- Maintained by **WHATWG**.
- Continuously updated instead of creating HTML6 or HTML7.
- Browser vendors collaborate on changes as the web evolves.
- Reflects what browsers actually implement.
- Includes ongoing improvements, bug fixes, clarifications, and integration with modern web APIs.

Today, Chrome, Firefox, Safari, and Edge track the **Living Standard**, making it the authoritative specification for modern HTML.

---

# Example

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Modern HTML</title>
  </head>
  <body>
    <main>
      <article>
        <h1>HTML Living Standard Example</h1>
        <p>This document uses semantic HTML supported by modern browsers.</p>
      </article>
    </main>
  </body>
</html>
```

This markup is valid under both HTML5 and the HTML Living Standard. The Living Standard mainly differs in how the specification evolves over time rather than requiring different syntax.

---

# Accessibility & SEO

### Accessibility

- Semantic elements introduced with HTML5 remain fundamental in the Living Standard.
- Use landmarks like:
  - `<header>`
  - `<nav>`
  - `<main>`
  - `<aside>`
  - `<footer>`

- Prefer native HTML controls over ARIA where possible ("No ARIA is better than bad ARIA").
- Keyboard behavior is defined by native HTML semantics and enhanced by browser implementations that follow the Living Standard.

### SEO

- Search engines benefit from semantic HTML regardless of whether you call it HTML5 or the Living Standard.
- Continue to use:
  - `<title>`
  - `<meta name="description">`
  - Proper heading hierarchy
  - Canonical URLs
  - Semantic content structure

- The Living Standard may clarify parsing and metadata behavior, but SEO best practices remain largely unchanged.

---

# Integration & Trade-offs

### CSS

- CSS selectors target semantic elements identically in HTML5 and the Living Standard.
- New semantic elements improve maintainability and readability.

### JavaScript

- Modern DOM APIs are specified alongside the Living Standard.
- Features are added incrementally without waiting for a new HTML version.

### Frameworks (React/Vue/Angular)

- JSX templates ultimately render standard HTML.
- Frameworks rely on browser implementations of the Living Standard.
- Continue using semantic HTML instead of generic `<div>` wrappers for better accessibility and SEO.

### Server-Side Rendering vs SPA

- SSR benefits from semantic HTML because content is immediately available to users and search engines.
- SPAs should still render semantic HTML and progressively enhance with JavaScript.
- The Living Standard supports progressive enhancement by ensuring HTML remains functional without JavaScript where feasible.

---

# Testing & Validation

- Validate markup using the WHATWG-compatible HTML validator (Nu Validator).
- Run accessibility audits with:
  - axe DevTools
  - Lighthouse

- Test with keyboard-only navigation and screen readers.
- Verify that semantic landmarks and headings are correctly exposed in the accessibility tree.
- Check browser compatibility for newer features before relying on them in production.

---

# Pitfalls

- **Assuming HTML5 is the latest specification.** Browsers now follow the continuously updated Living Standard.
- **Using "HTML5" to refer to JavaScript APIs.** Many APIs commonly labeled "HTML5" (such as Geolocation or Web Storage) evolve independently of the core HTML specification.
- **Ignoring browser support.** Even if a feature appears in the Living Standard, verify implementation across target browsers before using it.

## Question 2. Who maintains the HTML specification?

## Question 3. What is the purpose of the WHATWG?

## Question 4. What is W3C’s role in HTML standardization?

## Question 5. What are deprecated attributes?

## Question 6. What are obsolete but conforming features?

## Question 7. What are obsolete and non-conforming features?

## Question 8. What is the difference between presentational and semantic markup?

## Question 9. Why should we avoid inline styles in HTML?

## Question 10. What is character encoding and why is UTF-8 commonly used?

## Question 11. What is tokenization in HTML parsing?

## Question 12. What is tree construction stage in parsing?

## Question 13. What is insertion mode in HTML parsing?

## Question 14. What happens when the parser encounters malformed nesting?

## Question 15. What are optional closing tags?

## Question 16. Which HTML tags can omit closing tags?

## Question 17. What are raw text elements?

## Question 18. What are escapable raw text elements?

## Question 19. What happens if you put block elements inside `<p>`?

## Question 20. Why does HTML auto-correct certain structures?
