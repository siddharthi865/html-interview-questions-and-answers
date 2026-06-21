# Set 4

| S.No. | Question                                                                                                                                             |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is the difference between `<article>` and `<section>`?](#question-1-what-is-the-difference-between-article-and-section)                        |
| 2.    | [What is the purpose of `<aside>`?](#question-2-what-is-the-purpose-of-aside)                                                                        |
| 3.    | [What is the `<nav>` tag used for?](#question-3-what-is-the-nav-tag-used-for)                                                                        |
| 4.    | [What is the `<main>` tag?](#question-4-what-is-the-main-tag)                                                                                        |
| 5.    | [What is the difference between `<figure>` and `<img>`?](#question-5-what-is-the-difference-between-figure-and-img)                                  |
| 6.    | [What is `<figcaption>`?](#question-6-what-is-figcaption)                                                                                            |
| 7.    | [What is the purpose of meta tags?](#question-7-what-is-the-purpose-of-meta-tags)                                                                    |
| 8.    | [What is the viewport meta tag?](#question-8-what-is-the-viewport-meta-tag)                                                                          |
| 9.    | [What is charset in HTML?](#question-9-what-is-charset-in-html)                                                                                      |
| 10.   | [What is the difference between `id` and `class`?](#question-10-what-is-the-difference-between-id-and-class)                                         |
| 11.   | [Can multiple elements have the same id?](#question-11-can-multiple-elements-have-the-same-id)                                                       |
| 12.   | [What is the difference between inline, internal, and external CSS?](#question-12-what-is-the-difference-between-inline-internal-and-external-css)   |
| 13.   | [How do you link CSS to HTML?](#question-13-how-do-you-link-css-to-html)                                                                             |
| 14.   | [How do you add JavaScript to HTML?](#question-14-how-do-you-add-javascript-to-html)                                                                 |
| 15.   | [Where should you place the `<script>` tag and why?](#question-15-where-should-you-place-the-script-tag-and-why)                                     |
| 16.   | [What is the difference between HTML and DOM?](#question-16-what-is-the-difference-between-html-and-dom)                                             |
| 17.   | [What is the difference between HTML attributes and DOM properties?](#question-17-what-is-the-difference-between-html-attributes-and-dom-properties) |
| 18.   | [What are data attributes?](#question-18-what-are-data-attributes)                                                                                   |
| 19.   | [What is the purpose of `data-*` attributes?](#question-19-what-is-the-purpose-of-data--attributes)                                                  |
| 20.   | [What is the difference between `defer` and `async` in script tags?](#question-20-what-is-the-difference-between-defer-and-async-in-script-tags)     |

## Question 1. What is the difference between `<article>` and `<section>`?

# Short answer

`<article>` represents a **self-contained, independent piece of content** that could stand on its own and potentially be reused or syndicated elsewhere.

`<section>` represents a **thematic grouping of related content** within a document, usually organized under a heading.

A good rule of thumb:

- Use **`<article>`** when the content makes sense independently.
- Use **`<section>`** when the content is part of a larger page and groups related information.

---

# Explanation

Both elements are semantic HTML5 elements, but they serve different purposes.

### `<article>`

An `<article>` is intended for content that could be distributed or reused independently, such as:

- Blog posts
- News articles
- Forum posts
- User comments
- Product reviews

The content should still make sense if extracted from the page.

Example:

```html
<article>
  <h2>How to Improve Web Performance</h2>
  <p>Performance optimization techniques...</p>
</article>
```

### `<section>`

A `<section>` groups related content under a common theme. It is typically part of a larger page structure.

Examples:

- Features section on a homepage
- FAQ section
- Contact section
- Chapters in a document

Example:

```html
<section>
  <h2>Features</h2>
  <p>Fast, secure, and scalable.</p>
</section>
```

### Relationship Between Them

An `<article>` can contain multiple `<section>` elements.

```html
<article>
  <h1>HTML Semantic Elements</h1>

  <section>
    <h2>Introduction</h2>
    <p>...</p>
  </section>

  <section>
    <h2>Examples</h2>
    <p>...</p>
  </section>
</article>
```

Similarly, a `<section>` may contain multiple articles.

---

# Example

```html
<main>
  <section>
    <h1>Latest Blog Posts</h1>

    <article>
      <h2>Understanding HTML Semantics</h2>
      <p>Learn how semantic HTML improves accessibility and SEO.</p>
    </article>

    <article>
      <h2>Modern CSS Layouts</h2>
      <p>An introduction to Grid and Flexbox.</p>
    </article>
  </section>
</main>
```

In this example:

- The **section** groups blog posts together.
- Each **article** is an independent piece of content.

---

# Accessibility & SEO

### Accessibility

- Both elements create meaningful document structure for assistive technologies.
- A `<section>` should generally have a heading (`<h1>`–`<h6>`) to identify its purpose.
- Screen readers can use landmarks and headings to navigate content more efficiently.

Example:

```html
<section aria-labelledby="faq-heading">
  <h2 id="faq-heading">Frequently Asked Questions</h2>
</section>
```

### SEO

Search engines use semantic structure to better understand page content.

- Use `<article>` for blog posts, news items, reviews, and other standalone content.
- Use `<section>` to organize page content logically.
- Proper heading hierarchy inside sections improves content discoverability.

---

# Integration & Trade-offs

### CSS

Both elements behave like block-level elements by default and can be styled identically:

```css
article,
section {
  padding: 1rem;
}
```

Choose them for **meaning**, not appearance.

### JavaScript

JavaScript can target either element:

```js
document.querySelectorAll("article");
```

Semantics remain valuable even when JS enhances behavior.

### Frameworks (React/Vue/Angular)

Use semantic tags in components rather than generic `<div>` elements.

React example:

```jsx
<ArticleCard>
  <article>...</article>
</ArticleCard>
```

### SSR vs SPA

- Server-side rendered content inside `<article>` is immediately available to crawlers and assistive technologies.
- In SPAs, semantic HTML still improves accessibility and maintainability, though content may be rendered client-side.

### Progressive Enhancement

Semantic HTML provides value even when CSS or JavaScript fails to load. The document structure remains understandable.

---

# Testing & Validation

- Validate markup using the WHATWG/W3C HTML validator.
- Use browser accessibility trees to verify document structure.
- Run:
  - axe DevTools
  - Lighthouse
  - Accessibility Insights

Checks:

1. Does each `<section>` have a meaningful heading?
2. Could each `<article>` stand on its own?
3. Is the heading hierarchy logical?

---

# Pitfalls

- Using `<section>` as a generic replacement for `<div>`.
- Creating sections without headings, making them less meaningful.
- Using `<article>` for content that cannot stand independently.

## Question 2. What is the purpose of `<aside>`?

## Question 3. What is the `<nav>` tag used for?

## Question 4. What is the `<main>` tag?

## Question 5. What is the difference between `<figure>` and `<img>`?

## Question 6. What is `<figcaption>`?

## Question 7. What is the purpose of meta tags?

## Question 8. What is the viewport meta tag?

## Question 9. What is charset in HTML?

## Question 10. What is the difference between `id` and `class`?

## Question 11. Can multiple elements have the same id?

## Question 12. What is the difference between inline, internal, and external CSS?

## Question 13. How do you link CSS to HTML?

## Question 14. How do you add JavaScript to HTML?

## Question 15. Where should you place the `<script>` tag and why?

## Question 16. What is the difference between HTML and DOM?

## Question 17. What is the difference between HTML attributes and DOM properties?

## Question 18. What are data attributes?

## Question 19. What is the purpose of `data-*` attributes?

## Question 20. What is the difference between `defer` and `async` in script tags?
