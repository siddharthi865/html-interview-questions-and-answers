# Set 11

| S.No. | Question                                                                                                                                                         |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What happens if you nest block elements inside inline elements?](#question-1-what-happens-if-you-nest-block-elements-inside-inline-elements)                    |
| 2.    | [What happens if HTML tags are not properly closed?](#question-2-what-happens-if-html-tags-are-not-properly-closed)                                              |
| 3.    | [How do browsers handle invalid HTML?](#question-3-how-do-browsers-handle-invalid-html)                                                                          |
| 4.    | [What is quirks mode?](#question-4-what-is-quirks-mode)                                                                                                          |
| 5.    | [What triggers standards mode?](#question-5-what-triggers-standards-mode)                                                                                        |
| 6.    | [What is the difference between strict mode and quirks mode rendering?](#question-6-what-is-the-difference-between-strict-mode-and-quirks-mode-rendering)        |
| 7.    | [Can multiple classes be assigned to a single element?](#question-7-can-multiple-classes-be-assigned-to-a-single-element)                                        |
| 8.    | [Can you nest forms in HTML?](#question-8-can-you-nest-forms-in-html)                                                                                            |
| 9.    | [What is the default display behavior of `<div>`?](#question-9-what-is-the-default-display-behavior-of-div)                                                      |
| 10.   | [What is the default display behavior of `<span>`?](#question-10-what-is-the-default-display-behavior-of-span)                                                   |
| 11.   | [What happens if duplicate attributes are added to an element?](#question-11-what-happens-if-duplicate-attributes-are-added-to-an-element)                       |
| 12.   | [What is the difference between boolean attributes and normal attributes?](#question-12-what-is-the-difference-between-boolean-attributes-and-normal-attributes) |
| 13.   | [What are common boolean attributes in HTML?](#question-13-what-are-common-boolean-attributes-in-html)                                                           |
| 14.   | [What happens if an attribute value is omitted?](#question-14-what-happens-if-an-attribute-value-is-omitted)                                                     |
| 15.   | [What is the difference between property reflection and attributes?](#question-15-what-is-the-difference-between-property-reflection-and-attributes)             |
| 16.   | [What are enumerated attributes?](#question-16-what-are-enumerated-attributes)                                                                                   |
| 17.   | [What are global event attributes?](#question-17-what-are-global-event-attributes)                                                                               |
| 18.   | [What is the `dir` attribute?](#question-18-what-is-the-dir-attribute)                                                                                           |
| 19.   | [What happens if id values are duplicated?](#question-19-what-happens-if-id-values-are-duplicated)                                                               |
| 20.   | [What are custom attributes vs data attributes?](#question-20-what-are-custom-attributes-vs-data-attributes)                                                     |

## Question 1. What happens if you nest block elements inside inline elements?

# Short answer

Nesting **block-level elements inside inline elements** is generally **invalid in older HTML models** and can lead browsers to automatically correct the markup in unexpected ways. In modern HTML5, the rule is more nuanced because elements are categorized by **content models** (flow content, phrasing content, etc.) rather than simply "block" and "inline." Most inline elements (such as `<span>`) only allow **phrasing content**, so placing a block element like `<div>` inside them is invalid.

---

# Explanation

Historically, HTML elements were classified as either:

- **Block elements** (`<div>`, `<p>`, `<section>`, `<article>`)
- **Inline elements** (`<span>`, `<a>`, `<strong>`, `<em>`)

The old rule was:

- ✅ Block elements can contain inline elements.
- ❌ Inline elements cannot contain block elements.

HTML5 replaced this with **content models**.

For example:

- `<span>` accepts **phrasing content only**.
- `<div>` is **flow content**, not phrasing content.

Therefore:

```html
<span>
  <div>Content</div>
</span>
```

is **invalid HTML**.

### What browsers do

Browsers use the HTML parsing algorithm to recover from invalid markup.

They may:

- Automatically close the inline element
- Move the block element outside
- Create a different DOM than you expected

This means:

- CSS selectors may not behave as expected.
- JavaScript DOM traversal can become confusing.
- Different browsers generally follow the HTML5 parser, but relying on parser correction is poor practice.

---

# Example

❌ Invalid

```html
<span class="highlight">
  <div>Important message</div>
</span>
```

✅ Correct

```html
<div class="highlight">
  <p>Important message</p>
</div>
```

Or, if only inline styling is needed:

```html
<p>
  This is
  <span class="highlight">important</span>
  text.
</p>
```

---

# Accessibility & SEO

### Accessibility

- Invalid nesting can confuse assistive technologies if the resulting DOM differs from the source.
- Use semantic containers:
  - `<section>`
  - `<article>`
  - `<main>`
  - `<nav>`
  - `<aside>`

- Avoid using `<div>` merely for styling when an inline `<span>` is appropriate.

### SEO

Search engines use the parsed DOM, so invalid nesting is usually corrected before indexing. However:

- Poor semantics reduce content clarity.
- Semantic HTML improves document structure and machine understanding.

---

# Integration & Trade-offs

### CSS

Developers sometimes attempt this:

```html
<span>
  <div class="tooltip"></div>
</span>
```

Instead, use:

```html
<span class="wrapper">
  <span class="tooltip">...</span>
</span>
```

or change the outer element to a `<div>` if block layout is required.

### JavaScript

Frameworks like React, Vue, and Angular generally preserve HTML semantics. Invalid nesting can trigger warnings (for example, React's `validateDOMNesting`) because the browser may create a DOM different from what the framework expects during hydration.

### Server-side Rendering (SSR)

Invalid HTML can cause hydration mismatches because the browser repairs the HTML before the client-side framework attaches to it.

### Progressive Enhancement

Using valid semantic markup ensures consistent behavior regardless of whether JavaScript is enabled.

---

# Testing & Validation

- Validate markup using the WHATWG HTML checker or the W3C Nu Validator.
- Run accessibility audits with **axe DevTools** or **Lighthouse**.
- Inspect the browser's DOM in DevTools to verify that the parsed DOM matches the authored HTML.

---

# Pitfalls

- **Putting `<div>` inside `<span>`** because of CSS layout needs instead of choosing the correct container.
- **Assuming the browser preserves invalid nesting** exactly as written.
- **Ignoring framework warnings** (e.g., React DOM nesting warnings), which can lead to hydration issues.

## Question 2. What happens if HTML tags are not properly closed?

## Question 3. How do browsers handle invalid HTML?

## Question 4. What is quirks mode?

## Question 5. What triggers standards mode?

## Question 6. What is the difference between strict mode and quirks mode rendering?

## Question 7. Can multiple classes be assigned to a single element?

## Question 8. Can you nest forms in HTML?

## Question 9. What is the default display behavior of `<div>`?

## Question 10. What is the default display behavior of `<span>`?

## Question 11. What happens if duplicate attributes are added to an element?

## Question 12. What is the difference between boolean attributes and normal attributes?

## Question 13. What are common boolean attributes in HTML?

## Question 14. What happens if an attribute value is omitted?

## Question 15. What is the difference between property reflection and attributes?

## Question 16. What are enumerated attributes?

## Question 17. What are global event attributes?

## Question 18. What is the `dir` attribute?

## Question 19. What happens if id values are duplicated?

## Question 20. What are custom attributes vs data attributes?
