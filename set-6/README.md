# Set 6

| S.No. | Question                                                                                                                                                                          |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is the purpose of the `<html>` tag?](#question-1-what-is-the-purpose-of-the-html-tag)                                                                                       |
| 2.    | [What is the `lang` attribute in the `<html>` tag used for?](#question-2-what-is-the-lang-attribute-in-the-html-tag-used-for)                                                     |
| 3.    | [What happens if we don't include `<!DOCTYPE html>`?](#question-3-what-happens-if-we-dont-include-doctype-html)                                                                   |
| 4.    | [What is the difference between HTML and XHTML?](#question-4-what-is-the-difference-between-html-and-xhtml)                                                                       |
| 5.    | [What are empty (void) elements in HTML?](#question-5-what-are-empty-void-elements-in-html)                                                                                       |
| 6.    | [Can HTML tags be case sensitive?](#question-6-can-html-tags-be-case-sensitive)                                                                                                   |
| 7.    | [What is the difference between `<meta>` and `<link>`?](#question-7-what-is-the-difference-between-meta-and-link)                                                                 |
| 8.    | [What is the purpose of the `<title>` tag?](#question-8-what-is-the-purpose-of-the-title-tag)                                                                                     |
| 9.    | [What is the difference between `<meta name="description">` and `<meta name="keywords">`?](#question-9-what-is-the-difference-between-meta-namedescription-and-meta-namekeywords) |
| 10.   | [How do comments work in HTML?](#question-10-how-do-comments-work-in-html)                                                                                                        |
| 11.   | [What is the `<mark>` tag used for?](#question-11-what-is-the-mark-tag-used-for)                                                                                                  |
| 12.   | [What is the `<small>` tag used for?](#question-12-what-is-the-small-tag-used-for)                                                                                                |
| 13.   | [What is the difference between `<sub>` and `<sup>`?](#question-13-what-is-the-difference-between-sub-and-sup)                                                                    |
| 14.   | [What is the `<abbr>` tag?](#question-14-what-is-the-abbr-tag)                                                                                                                    |
| 15.   | [What is the `<cite>` tag?](#question-15-what-is-the-cite-tag)                                                                                                                    |
| 16.   | [What is the `<blockquote>` tag?](#question-16-what-is-the-blockquote-tag)                                                                                                        |
| 17.   | [What is the `<q>` tag?](#question-17-what-is-the-q-tag)                                                                                                                          |
| 18.   | [What is the `<code>` tag?](#question-18-what-is-the-code-tag)                                                                                                                    |
| 19.   | [What is the `<kbd>` tag?](#question-19-what-is-the-kbd-tag)                                                                                                                      |
| 20.   | [What is the `<s>` tag?](#question-20-what-is-the-s-tag)                                                                                                                          |

## Question 1. What is the purpose of the `<html>` tag?

# Short answer

The `<html>` tag is the **root element** of every HTML document. It wraps the entire page (except the `<!DOCTYPE html>` declaration), identifies the document as HTML, and provides document-wide metadata such as the page language through the `lang` attribute.

---

# Explanation

The `<html>` element is the top-level container for all HTML content. Every valid HTML document has exactly one `<html>` element containing two primary children:

- `<head>` – Metadata, stylesheets, scripts, title, character encoding, viewport settings, etc.
- `<body>` – All visible page content.

Example structure:

```text
<!DOCTYPE html>
<html>
  <head>...</head>
  <body>...</body>
</html>
```

### Why it matters

### 1. Defines the document root

The browser builds the DOM starting from the `<html>` element. Every visible and non-visible HTML element is a descendant of this root node.

```text
Document
└── html
    ├── head
    └── body
```

### 2. Specifies the document language

The `lang` attribute is one of the most important attributes on `<html>`.

```html
<html lang="en"></html>
```

Benefits:

- Helps screen readers pronounce content correctly.
- Assists browsers with spell checking.
- Improves translation accuracy.
- Provides language information for search engines.

For multilingual pages, use `lang` on individual elements when content changes language:

```html
<p>
  Welcome!
  <span lang="fr">Bonjour</span>
</p>
```

### 3. Serves as the root for CSS and JavaScript

CSS can target the root element:

```css
html {
  scroll-behavior: smooth;
  font-size: 16px;
}
```

JavaScript can access it using:

```javascript
document.documentElement;
```

This is commonly used for:

- Dark mode toggling
- CSS custom properties
- Reading viewport information
- Manipulating global classes

Example:

```javascript
document.documentElement.classList.add("dark");
```

### 4. Supports accessibility

The `lang` attribute on `<html>` enables assistive technologies to:

- Use the correct pronunciation rules.
- Choose the correct speech synthesis voice.
- Interpret abbreviations correctly.

Without it, many screen readers default to an incorrect language.

### 5. Helps SEO

Search engines use the page language to:

- Index pages appropriately.
- Serve the correct language version.
- Understand multilingual websites.

For international sites, `lang` works together with:

- `<meta charset>`
- `<title>`
- `hreflang` links (for alternate language versions)
- Canonical URLs

---

# Example

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Example Page</title>
  </head>
  <body>
    <header>
      <h1>Welcome</h1>
    </header>

    <main>
      <p>This is a valid HTML document.</p>
    </main>
  </body>
</html>
```

This example demonstrates:

- Proper document structure
- Root `<html>` element
- Language declaration
- Semantic HTML5 elements

---

# Accessibility & SEO

### Accessibility

- Always set the `lang` attribute on the `<html>` element.
- Use additional `lang` attributes only for portions of content in another language.
- No ARIA role is required or recommended for `<html>`; it already has well-defined semantics.
- The `<html>` element is not a landmark—landmarks come from elements like `<header>`, `<main>`, `<nav>`, and `<footer>`.

### SEO

- Specify the correct language:

  ```html
  <html lang="en"></html>
  ```

- Combine it with:
  - `<title>`
  - `<meta charset="UTF-8">`
  - `<meta name="viewport">`
  - Descriptive metadata and structured semantic HTML.

- For multilingual sites, pair `lang` with appropriate `hreflang` links to help search engines serve the correct localized version.

---

# Integration & Trade-offs

### CSS

The `<html>` element is frequently used for global styles:

```css
html {
  font-size: 100%;
  scroll-behavior: smooth;
}
```

CSS custom properties are often defined here:

```css
html {
  --primary-color: #0d6efd;
}
```

### JavaScript

Global application state is commonly reflected by classes or data attributes on the root element:

```html
<html lang="en" data-theme="dark"></html>
```

or

```javascript
document.documentElement.dataset.theme = "dark";
```

### Client-side frameworks

Frameworks like React, Vue, and Angular typically mount inside the `<body>` (for example, a `<div id="root">`). The `<html>` element is generally managed by the server-rendered document template or framework-specific document file (such as Next.js's custom document). Frameworks may update attributes like `lang` or `class` for themes or localization, but they do not replace the `<html>` element itself.

### Server-side rendering & Progressive Enhancement

- SSR sends a complete HTML document beginning with the `<html>` element, enabling browsers and search engines to parse content immediately.
- Progressive enhancement relies on a valid HTML document first; JavaScript can then enhance behavior without changing the fundamental role of the `<html>` element.

---

# Testing & Validation

- Validate markup using the HTML Living Standard validator to ensure there is a single `<html>` element and a correct document structure.
- Run accessibility audits with tools like axe or Lighthouse to verify that the document language (`lang`) is specified.
- Test with a screen reader to confirm the correct language is announced and pronunciation is appropriate.
- Inspect `document.documentElement` in browser DevTools to verify global attributes (such as `lang`, `class`, or `data-theme`) are applied as expected.

---

# Pitfalls

- **Omitting the `lang` attribute**, reducing accessibility and potentially affecting language detection.
- **Using multiple `<html>` elements**, which creates an invalid HTML document.
- **Trying to replace or manipulate the `<html>` element itself** instead of updating its attributes (such as `class`, `lang`, or `data-*`) for themes or localization.

## Question 2. What is the `lang` attribute in the `<html>` tag used for?

## Question 3. What happens if we don’t include `<!DOCTYPE html>`?

## Question 4. What is the difference between HTML and XHTML?

## Question 5. What are empty (void) elements in HTML?

## Question 6. Can HTML tags be case sensitive?

## Question 7. What is the difference between `<meta>` and `<link>`?

## Question 8. What is the purpose of the `<title>` tag?

## Question 9. What is the difference between `<meta name="description">` and `<meta name="keywords">`?

## Question 10. How do comments work in HTML?

## Question 11. What is the `<mark>` tag used for?

## Question 12. What is the `<small>` tag used for?

## Question 13. What is the difference between `<sub>` and `<sup>`?

## Question 14. What is the `<abbr>` tag?

## Question 15. What is the `<cite>` tag?

## Question 16. What is the `<blockquote>` tag?

## Question 17. What is the `<q>` tag?

## Question 18. What is the `<code>` tag?

## Question 19. What is the `<kbd>` tag?

## Question 20. What is the `<s>` tag?
