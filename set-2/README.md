# Set 2

| S.No. | Question                                                                                                                            |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [How do you create a hyperlink in HTML?](#question-1-how-do-you-create-a-hyperlink-in-html)                                         |
| 2.    | [What is the difference between absolute and relative URLs?](#question-2-what-is-the-difference-between-absolute-and-relative-urls) |
| 3.    | [What is the `target` attribute in anchor tags?](#question-3-what-is-the-target-attribute-in-anchor-tags)                           |
| 4.    | [How do you add an image in HTML?](#question-4-how-do-you-add-an-image-in-html)                                                     |
| 5.    | [What is the `alt` attribute?](#question-5-what-is-the-alt-attribute)                                                               |
| 6.    | [Why is the `alt` attribute important?](#question-6-why-is-the-alt-attribute-important)                                             |
| 7.    | [How do you add audio in HTML5?](#question-7-how-do-you-add-audio-in-html5)                                                         |
| 8.    | [How do you add video in HTML5?](#question-8-how-do-you-add-video-in-html5)                                                         |
| 9.    | [What is the purpose of the `controls` attribute?](#question-9-what-is-the-purpose-of-the-controls-attribute)                       |
| 10.   | [What is the `<source>` tag used for?](#question-10-what-is-the-source-tag-used-for)                                                |
| 11.   | [What are the types of lists in HTML?](#question-11-what-are-the-types-of-lists-in-html)                                            |
| 12.   | [What is the difference between `<ul>` and `<ol>`?](#question-12-what-is-the-difference-between-ul-and-ol)                          |
| 13.   | [What is the `<dl>` tag?](#question-13-what-is-the-dl-tag)                                                                          |
| 14.   | [How do you create nested lists?](#question-14-how-do-you-create-nested-lists)                                                      |
| 15.   | [What is the `type` attribute in ordered lists?](#question-15-what-is-the-type-attribute-in-ordered-lists)                          |
| 16.   | [What is the purpose of the `<form>` tag?](#question-16-what-is-the-purpose-of-the-form-tag)                                        |
| 17.   | [What are common input types in HTML5?](#question-17-what-are-common-input-types-in-html5)                                          |
| 18.   | [What is the difference between GET and POST?](#question-18-what-is-the-difference-between-get-and-post)                            |
| 19.   | [What is the `action` attribute in forms?](#question-19-what-is-the-action-attribute-in-forms)                                      |
| 20.   | [What is the `method` attribute?](#question-20-what-is-the-method-attribute)                                                        |

## Question 1. How do you create a hyperlink in HTML?

# Short answer

A hyperlink is created using the `<a>` (anchor) element with the `href` attribute:

```html
<a href="https://example.com">Visit Example</a>
```

When users click the link, the browser navigates to the URL specified in `href`.

---

# Explanation

The `<a>` element is the semantic HTML element for creating links between resources. Hyperlinks are fundamental to the web because they connect pages, documents, sections of a page, files, email addresses, and other protocols.

Key concepts:

- **`href` (Hypertext Reference)** specifies the destination.
- The link text should clearly describe the destination rather than using generic text like "Click here."
- Links are keyboard accessible by default and can be activated using the **Enter** key.
- Search engines use hyperlinks to discover and understand relationships between pages.
- CSS is commonly used to style links, while JavaScript can enhance behavior without replacing native link functionality.
- For navigation, use real links (`<a>`) instead of buttons. Buttons (`<button>`) should perform actions, not navigation.

Common link types:

- External page: `https://example.com`
- Internal page: `/about`
- Page section: `#contact`
- Email: `mailto:user@example.com`
- Phone: `tel:+1234567890`

---

# Example

```html
<nav aria-label="Main navigation">
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About Us</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<section id="contact">
  <h2>Contact</h2>
  <p>Email us anytime.</p>
</section>
```

For opening an external link in a new tab:

```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
  External Website
</a>
```

---

# Accessibility & SEO

### Accessibility

- Use meaningful link text:
  - ✅ "View pricing plans"
  - ❌ "Click here"

- Links are focusable and keyboard accessible by default.
- Avoid placing non-descriptive content inside links without accessible text.
- If a link opens a new tab/window, consider informing users in the visible text or accessible name.

Example:

```html
<a href="report.pdf"> Download Annual Report (PDF) </a>
```

### SEO

- Search engines use anchor text to understand the destination page.
- Descriptive anchor text improves SEO and usability.
- Use crawlable URLs in `href`.
- Internal linking helps search engines discover and rank content.

Good:

```html
<a href="/html-guide">Complete HTML Guide</a>
```

Poor:

```html
<a href="/html-guide">Read more</a>
```

---

# Integration & Trade-offs

### CSS Integration

Links can be styled using pseudo-classes:

```css
a:hover {
  text-decoration: underline;
}
a:focus {
  outline: 2px solid;
}
```

Always preserve visible focus indicators for keyboard users.

### JavaScript Integration

JavaScript can enhance links:

```html
<a href="/products" id="products-link">Products</a>
```

However, navigation should still work if JavaScript is disabled (progressive enhancement).

### Frameworks

- **React:** Often uses routing components (e.g., `<Link>` from React Router), which ultimately render anchor elements.
- **Vue:** Uses `<router-link>`.
- **Angular:** Uses `[routerLink]`.

Example (React):

```jsx
<Link to="/about">About</Link>
```

These components preserve SPA navigation while maintaining link semantics.

### SSR vs SPA

- **SSR (Server-Side Rendering):** Links work immediately and are easily crawled.
- **SPA (Single-Page Applications):** Client-side routing improves navigation speed but should still render semantic links for accessibility and SEO.

---

# Testing & Validation

- Validate markup using the WHATWG/W3C HTML validator.
- Run accessibility audits with:
  - axe DevTools
  - Lighthouse
  - WAVE

- Test keyboard navigation:
  - Tab to the link.
  - Ensure focus is visible.
  - Press Enter and verify navigation.

- Verify screen readers announce meaningful link text.

---

# Pitfalls

- Using `<button>` for page navigation instead of `<a>`.
- Using vague anchor text such as "Click here" or "Read more."
- Opening links with `target="_blank"` without `rel="noopener noreferrer"`.

## Question 2. What is the difference between absolute and relative URLs?

## Question 3. What is the `target` attribute in anchor tags?

## Question 4. How do you add an image in HTML?

## Question 5. What is the `alt` attribute?

## Question 6. Why is the `alt` attribute important?

## Question 7. How do you add audio in HTML5?

## Question 8. How do you add video in HTML5?

## Question 9. What is the purpose of the `controls` attribute?

## Question 10. What is the `<source>` tag used for?

## Question 11. What are the types of lists in HTML?

## Question 12. What is the difference between `<ul>` and `<ol>`?

## Question 13. What is the `<dl>` tag?

## Question 14. How do you create nested lists?

## Question 15. What is the `type` attribute in ordered lists?

## Question 16. What is the purpose of the `<form>` tag?

## Question 17. What are common input types in HTML5?

## Question 18. What is the difference between GET and POST?

## Question 19. What is the `action` attribute in forms?

## Question 20. What is the `method` attribute?
