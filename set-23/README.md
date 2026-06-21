# Set 23

| S.No. | Question                                                                                                                    |
| ----- | --------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is fetchpriority attribute?](#question-1-what-is-fetchpriority-attribute)                                             |
| 2.    | [What is priority hints?](#question-2-what-is-priority-hints)                                                               |
| 3.    | [What is speculative preloading?](#question-3-what-is-speculative-preloading)                                               |
| 4.    | [What is lazy rendering vs lazy loading?](#question-4-what-is-lazy-rendering-vs-lazy-loading)                               |
| 5.    | [What is intersection of HTML and IntersectionObserver?](#question-5-what-is-intersection-of-html-and-intersectionobserver) |
| 6.    | [What is back-forward cache (bfcache)?](#question-6-what-is-back-forward-cache-bfcache)                                     |
| 7.    | [What HTML patterns break bfcache?](#question-7-what-html-patterns-break-bfcache)                                           |
| 8.    | [What is prerender speculation rules?](#question-8-what-is-prerender-speculation-rules)                                     |
| 9.    | [What is importance of minimal DOM depth?](#question-9-what-is-importance-of-minimal-dom-depth)                             |
| 10.   | [How does excessive nesting affect performance?](#question-10-how-does-excessive-nesting-affect-performance)                |
| 11.   | [What is name computation algorithm in accessibility?](#question-11-what-is-name-computation-algorithm-in-accessibility)    |
| 12.   | [What is accessible name vs accessible description?](#question-12-what-is-accessible-name-vs-accessible-description)        |
| 13.   | [How does implicit ARIA role mapping work?](#question-13-how-does-implicit-aria-role-mapping-work)                          |
| 14.   | [What is role conflict?](#question-14-what-is-role-conflict)                                                                |
| 15.   | [What is presentational role conflict resolution?](#question-15-what-is-presentational-role-conflict-resolution)            |
| 16.   | [What is accessible focus order?](#question-16-what-is-accessible-focus-order)                                              |
| 17.   | [What is roving tabindex pattern?](#question-17-what-is-roving-tabindex-pattern)                                            |
| 18.   | [What is modal accessibility requirement?](#question-18-what-is-modal-accessibility-requirement)                            |
| 19.   | [What is inert subtree behavior?](#question-19-what-is-inert-subtree-behavior)                                              |
| 20.   | [What is aria-modal?](#question-20-what-is-aria-modal)                                                                      |

## Question 1. What is fetchpriority attribute?

# Short answer

The `fetchpriority` attribute is a **resource priority hint** that tells the browser how important a resource is relative to other resources during loading. It helps the browser decide **which resources to fetch sooner or later**, improving page performance—especially for critical images like the Largest Contentful Paint (LCP) image.

Supported values are:

- `high` – Prioritize fetching earlier.
- `low` – Deprioritize fetching.
- `auto` (default) – Let the browser decide.

---

# Explanation

Modern browsers already assign priorities to resources based on their type and location in the document. For example:

- CSS in `<head>` → very high priority
- JavaScript → high or medium
- Images → often lower initially
- Lazy-loaded images → very low

`fetchpriority` lets developers provide an additional hint when the browser's default heuristics are not optimal.

It is **not a command**—the browser may ignore it if it determines another strategy is better.

Common use cases:

- Prioritize the hero image (LCP)
- Deprioritize decorative images
- Fine-tune network scheduling on image-heavy pages

Unlike `loading="lazy"`, which controls **when** a resource begins loading, `fetchpriority` influences **how urgently** it is fetched once discovered.

---

# Example

```html
<!-- Critical hero image -->
<img
  src="/images/hero.webp"
  alt="Product showcase"
  width="1200"
  height="600"
  fetchpriority="high"
/>

<!-- Decorative image -->
<img src="/images/background-pattern.svg" alt="" fetchpriority="low" />
```

A common optimization for the LCP image is:

```html
<link rel="preload" as="image" href="/images/hero.webp" fetchpriority="high" />

<img
  src="/images/hero.webp"
  alt="Hero banner"
  width="1200"
  height="600"
  fetchpriority="high"
/>
```

> `preload` helps the browser discover the image early, while `fetchpriority="high"` tells it to treat the fetch as important.

---

# Accessibility & SEO

### Accessibility

- `fetchpriority` has **no accessibility impact**.
- Continue providing meaningful `alt` text for informative images.
- Decorative images should use `alt=""`.

### SEO

- It has **no direct SEO effect**.
- It can improve **Core Web Vitals**, particularly:
  - Largest Contentful Paint (LCP)
  - Sometimes First Contentful Paint (FCP)

- Better Core Web Vitals can contribute to a better user experience, which is considered in search ranking signals.

---

# Integration & Trade-offs

### CSS

Background images cannot use the HTML `fetchpriority` attribute because they are loaded from CSS. Instead, consider preloading critical background images:

```html
<link rel="preload" as="image" href="/hero-bg.webp" />
```

### JavaScript

The JavaScript `Image` object also exposes a `fetchPriority` property:

```javascript
const img = new Image();
img.fetchPriority = "high";
img.src = "/hero.webp";
```

### React/Vue/Angular

Most modern frameworks pass the attribute through:

```jsx
<img src="/hero.webp" fetchPriority="high" alt="Hero" />
```

In React, the JSX prop is `fetchPriority` (camelCase), which renders as the HTML `fetchpriority` attribute.

### SSR & Progressive Enhancement

- Works well with server-side rendered pages because the browser sees the hint immediately.
- Browsers that don't support it simply ignore it, making it a safe progressive enhancement.

### Performance considerations

Use `high` sparingly. Marking many resources as high priority can reduce its effectiveness and compete with truly critical resources like CSS or fonts.

---

# Testing & Validation

- Inspect the **Network** panel in browser DevTools to verify resource priorities.
- Use **Lighthouse** to measure LCP improvements.
- Use browser performance profiling to confirm the hero image loads earlier.
- Validate HTML with the WHATWG-compliant validator and ensure the attribute is used only where supported.

---

# Pitfalls

- **Don't mark every image as `fetchpriority="high"`**—only the most critical resources.
- **Don't confuse it with `loading="lazy"`**—they solve different problems (`when` vs. `priority`).
- **Don't expect guaranteed behavior**—it's a browser hint, not a strict instruction.

## Question 2. What is priority hints?

## Question 3. What is speculative preloading?

## Question 4. What is lazy rendering vs lazy loading?

## Question 5. What is intersection of HTML and IntersectionObserver?

## Question 6. What is back-forward cache (bfcache)?

## Question 7. What HTML patterns break bfcache?

## Question 8. What is prerender speculation rules?

## Question 9. What is importance of minimal DOM depth?

## Question 10. How does excessive nesting affect performance?

## Question 11. What is name computation algorithm in accessibility?

## Question 12. What is accessible name vs accessible description?

## Question 13. How does implicit ARIA role mapping work?

## Question 14. What is role conflict?

## Question 15. What is presentational role conflict resolution?

## Question 16. What is accessible focus order?

## Question 17. What is roving tabindex pattern?

## Question 18. What is modal accessibility requirement?

## Question 19. What is inert subtree behavior?

## Question 20. What is aria-modal?
