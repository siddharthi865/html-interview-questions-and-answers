# Set 14

| S.No. | Question                                                                                                                                                    |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [How does screen reader interpret semantic elements?](#question-1-how-does-screen-reader-interpret-semantic-elements)                                       |
| 2.    | [What is landmark role in accessibility?](#question-2-what-is-landmark-role-in-accessibility)                                                               |
| 3.    | [What is the difference between `aria-describedby` and `aria-labelledby`?](#question-3-what-is-the-difference-between-aria-describedby-and-aria-labelledby) |
| 4.    | [How do you create accessible navigation?](#question-4-how-do-you-create-accessible-navigation)                                                             |
| 5.    | [What are skip links?](#question-5-what-are-skip-links)                                                                                                     |
| 6.    | [How do you improve keyboard navigation?](#question-6-how-do-you-improve-keyboard-navigation)                                                               |
| 7.    | [What is focus management in HTML?](#question-7-what-is-focus-management-in-html)                                                                           |
| 8.    | [How do you hide content visually but keep it accessible?](#question-8-how-do-you-hide-content-visually-but-keep-it-accessible)                             |
| 9.    | [What is live region in ARIA?](#question-9-what-is-live-region-in-aria)                                                                                     |
| 10.   | [What is `aria-live`?](#question-10-what-is-aria-live)                                                                                                      |
| 11.   | [How do custom elements lifecycle methods work?](#question-11-how-do-custom-elements-lifecycle-methods-work)                                                |
| 12.   | [What is the difference between open and closed Shadow DOM?](#question-12-what-is-the-difference-between-open-and-closed-shadow-dom)                        |
| 13.   | [How does template cloning work?](#question-13-how-does-template-cloning-work)                                                                              |
| 14.   | [What is slot fallback content?](#question-14-what-is-slot-fallback-content)                                                                                |
| 15.   | [How does HTML module scripts work?](#question-15-how-does-html-module-scripts-work)                                                                        |
| 16.   | [What is import maps in HTML?](#question-16-what-is-import-maps-in-html)                                                                                    |
| 17.   | [What is declarative shadow DOM?](#question-17-what-is-declarative-shadow-dom)                                                                              |
| 18.   | [What is the popover API?](#question-18-what-is-the-popover-api)                                                                                            |
| 19.   | [What is the inert attribute?](#question-19-what-is-the-inert-attribute)                                                                                    |
| 20.   | [What is view transitions API?](#question-20-what-is-view-transitions-api)                                                                                  |

## Question 1. How does screen reader interpret semantic elements?

# How does screen reader interpret semantic elements?

## Short answer

Screen readers use semantic HTML elements to understand the structure and meaning of a webpage. Instead of simply reading content in order, they expose elements like `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, and headings as landmarks and structural regions, allowing users to navigate quickly and understand the page hierarchy.

---

## Explanation

Semantic HTML provides **meaning**, not just presentation. Browsers build an **Accessibility Tree** from the DOM, mapping semantic elements to accessibility APIs (such as UI Automation on Windows, AX API on macOS, and ATK on Linux). Screen readers consume this accessibility tree—not the raw HTML.

For example:

- `<header>` → Banner landmark (when it's the page header)
- `<nav>` → Navigation landmark
- `<main>` → Main content landmark
- `<footer>` → Contentinfo landmark (when it's the page footer)
- `<article>` → Article/document region
- `<section>` → Region (only when it has an accessible name, such as a heading)
- `<aside>` → Complementary landmark
- `<h1>`–`<h6>` → Heading levels for document outline
- `<button>` → Button control with built-in keyboard behavior
- `<form>` → Form landmark (typically when it has an accessible name)

This enables screen reader users to:

- Jump directly between landmarks.
- Navigate by heading levels.
- Skip repetitive navigation.
- Understand the relationship between different content areas.
- Interact with controls using expected keyboard shortcuts.

Using semantic HTML also reduces the need for custom ARIA because browsers already expose the correct roles.

### Example interpretation

Given this HTML:

```html
<header>
  <h1>Tech Blog</h1>
</header>

<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/articles">Articles</a></li>
  </ul>
</nav>

<main>
  <article>
    <h2>Understanding Semantic HTML</h2>
    <p>Semantic HTML improves accessibility.</p>
  </article>
</main>

<footer>
  <p>&copy; 2026</p>
</footer>
```

A screen reader may expose something conceptually like:

- Banner
- Heading level 1: "Tech Blog"
- Navigation
- Main
- Article
- Heading level 2: "Understanding Semantic HTML"
- Contentinfo

Users can jump directly to any of these landmarks instead of reading everything sequentially.

---

## Example

```html
<header>
  <h1>Company Portal</h1>
</header>

<nav aria-label="Primary">
  <ul>
    <li><a href="/">Dashboard</a></li>
    <li><a href="/reports">Reports</a></li>
  </ul>
</nav>

<main>
  <article>
    <h2>Monthly Report</h2>
    <p>Revenue increased by 12%.</p>
  </article>
</main>

<footer>
  <p>© 2026 Company</p>
</footer>
```

This markup is fully semantic and requires no additional ARIA roles because the HTML elements already communicate their purpose.

---

## Accessibility & SEO

### Accessibility

- Prefer semantic elements over generic `<div>` containers.
- Use a single `<main>` landmark per page.
- Maintain a logical heading hierarchy (`<h1>` → `<h2>` → `<h3>`).
- Give multiple navigation areas distinct accessible names using `aria-label`, e.g., `aria-label="Primary"` and `aria-label="Footer"`.
- Avoid replacing native elements (e.g., `<button>`, `<a>`) with `<div>` or `<span>` plus ARIA unless absolutely necessary.

### SEO

Semantic HTML helps search engines better understand page structure:

- `<article>` identifies standalone content.
- `<nav>` indicates navigation menus.
- Headings establish content hierarchy.
- `<header>` and `<footer>` define page sections.

While semantic HTML is not a direct ranking factor, it improves crawlability and content understanding.

---

## Integration & Trade-offs

- **CSS:** Semantic elements behave like normal HTML elements and can be styled identically to `<div>` elements.
- **JavaScript:** Semantic elements provide meaning independent of JS, supporting progressive enhancement. JS should enhance interactions rather than recreate semantics.
- **React/Vue/Angular:** Use semantic elements in JSX/templates (`<main>`, `<nav>`, `<section>`) instead of wrapping everything in `<div>`. Component abstraction should preserve meaningful HTML.
- **SSR vs. SPA:** Server-side rendering exposes semantic markup immediately, benefiting assistive technologies and SEO. SPAs should ensure dynamic updates preserve landmarks, headings, focus management, and announce significant changes when appropriate.

---

## Testing & Validation

- Validate HTML to ensure semantic elements are used correctly and nested properly.
- Test keyboard navigation to verify users can reach landmarks and controls logically.
- Use browser accessibility inspectors to view the accessibility tree and confirm roles and names.
- Run automated audits with tools like **axe DevTools** and **Lighthouse**, then verify behavior with real screen readers such as **NVDA**, **JAWS**, or **VoiceOver**, since automated tools cannot fully assess the user experience.

---

## Pitfalls

- Using numerous `<div>` elements instead of semantic elements, forcing assistive technologies to infer structure.
- Skipping heading levels or using headings solely for visual styling.
- Adding unnecessary ARIA roles (e.g., `role="button"` on an actual `<button>` or `role="navigation"` on `<nav>`), which is redundant and can introduce maintenance issues.

## Question 2. What is landmark role in accessibility?

## Question 3. What is the difference between `aria-describedby` and `aria-labelledby`?

## Question 4. How do you create accessible navigation?

## Question 5. What are skip links?

## Question 6. How do you improve keyboard navigation?

## Question 7. What is focus management in HTML?

## Question 8. How do you hide content visually but keep it accessible?

## Question 9. What is live region in ARIA?

## Question 10. What is `aria-live`?

## Question 11. How do custom elements lifecycle methods work?

## Question 12. What is the difference between open and closed Shadow DOM?

## Question 13. How does template cloning work?

## Question 14. What is slot fallback content?

## Question 15. How does HTML module scripts work?

## Question 16. What is import maps in HTML?

## Question 17. What is declarative shadow DOM?

## Question 18. What is the popover API?

## Question 19. What is the inert attribute?

## Question 20. What is view transitions API?
