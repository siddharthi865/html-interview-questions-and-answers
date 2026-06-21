# Set 9

| S.No. | Question                                                                                                                                                              |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is canonical link in HTML?](#question-1-what-is-canonical-link-in-html)                                                                                         |
| 2.    | [What is prefetching in HTML?](#question-2-what-is-prefetching-in-html)                                                                                               |
| 3.    | [What is preloading in HTML?](#question-3-what-is-preloading-in-html)                                                                                                 |
| 4.    | [What is DNS prefetch?](#question-4-what-is-dns-prefetch)                                                                                                             |
| 5.    | [What is the difference between `<script defer>` and placing script at bottom?](#question-5-what-is-the-difference-between-script-defer-and-placing-script-at-bottom) |
| 6.    | [What is the `<noscript>` tag?](#question-6-what-is-the-noscript-tag)                                                                                                 |
| 7.    | [What is structured data in HTML?](#question-7-what-is-structured-data-in-html)                                                                                       |
| 8.    | [What are Open Graph meta tags?](#question-8-what-are-open-graph-meta-tags)                                                                                           |
| 9.    | [What is the purpose of `rel="noopener"`?](#question-9-what-is-the-purpose-of-relnoopener)                                                                            |
| 10.   | [What is `rel="noreferrer"`?](#question-10-what-is-relnoreferrer)                                                                                                     |
| 11.   | [How does the HTML parser work?](#question-11-how-does-the-html-parser-work)                                                                                          |
| 12.   | [What is DOM tree construction?](#question-12-what-is-dom-tree-construction)                                                                                          |
| 13.   | [What happens during HTML reflow and repaint?](#question-13-what-happens-during-html-reflow-and-repaint)                                                              |
| 14.   | [What causes layout thrashing?](#question-14-what-causes-layout-thrashing)                                                                                            |
| 15.   | [What are custom elements?](#question-15-what-are-custom-elements)                                                                                                    |
| 16.   | [What is Shadow DOM?](#question-16-what-is-shadow-dom)                                                                                                                |
| 17.   | [What is the template tag?](#question-17-what-is-the-template-tag)                                                                                                    |
| 18.   | [What is slot in Web Components?](#question-18-what-is-slot-in-web-components)                                                                                        |
| 19.   | [What is hydration in frontend frameworks?](#question-19-what-is-hydration-in-frontend-frameworks)                                                                    |
| 20.   | [What is server-side rendering (SSR)?](#question-20-what-is-server-side-rendering-ssr)                                                                                |

## Question 1. What is canonical link in HTML?

# Short answer

A **canonical link** is an HTML `<link>` element placed inside the `<head>` that tells search engines which URL is the **preferred (canonical) version** of a page when multiple URLs contain the same or very similar content. It helps consolidate SEO signals and reduces duplicate content issues.

```html
<link rel="canonical" href="https://example.com/products/laptop" />
```

---

# Explanation

A canonical link uses the `rel="canonical"` relationship to indicate the authoritative URL for a page.

For example, all of these URLs may display the same content:

- `https://example.com/product/123`
- `https://example.com/product/123?ref=homepage`
- `https://example.com/product/123?utm_source=newsletter`
- `https://www.example.com/product/123`

Without a canonical URL, search engines may treat them as separate pages, splitting ranking signals such as backlinks and indexing. By specifying a canonical URL, you tell search engines to attribute SEO value to the preferred version.

### How it works

1. Browser loads the HTML document.
2. Search engine crawlers read the `<head>`.
3. They find:

```html
<link rel="canonical" href="https://example.com/product/123" />
```

4. The search engine understands that this URL is the preferred version and generally consolidates indexing and ranking signals toward it.

**Important:** The canonical tag is a **hint**, not a strict directive. Search engines may ignore it if it conflicts with the page content, redirects, or other signals.

---

# Example

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Wireless Headphones</title>

    <link
      rel="canonical"
      href="https://example.com/products/wireless-headphones"
    />
  </head>
  <body>
    <main>
      <h1>Wireless Headphones</h1>
      <p>High-quality wireless headphones with noise cancellation.</p>
    </main>
  </body>
</html>
```

If users visit:

```
https://example.com/products/wireless-headphones?utm_source=email
```

the canonical tag points search engines to:

```
https://example.com/products/wireless-headphones
```

---

# Accessibility & SEO

### Accessibility

- The canonical tag has **no direct accessibility impact**.
- It is not exposed to screen readers or assistive technologies.
- No ARIA attributes or roles are required.

### SEO

Canonical tags are important because they:

- Prevent duplicate content issues.
- Consolidate ranking signals (backlinks, authority).
- Improve crawl efficiency.
- Ensure the preferred URL appears in search results.
- Help when the same content is available through filtering, sorting, tracking parameters, or multiple routes.

**Best practices**

- Place the tag inside the `<head>`.
- Use an **absolute URL**.
- Only specify **one canonical tag** per page.
- Ensure the canonical URL returns **HTTP 200 OK**.
- The canonical page should not be blocked by `robots.txt` or marked with `noindex`.
- Canonical URLs should match redirects. For example, don't canonicalize to a URL that immediately redirects elsewhere.

---

# Integration & Trade-offs

### CSS

- CSS is unaffected by canonical links.

### JavaScript

- Client-side JavaScript cannot rely on canonical tags for navigation or routing.
- If a SPA injects canonical tags dynamically, ensure they are present in the server-rendered HTML or rendered early enough for crawlers that may not execute JavaScript fully.

### Server-Side Rendering (SSR)

- SSR frameworks (e.g., React with Next.js, Vue with Nuxt, Angular Universal) should generate canonical tags on the server for each route.
- Dynamic pages should compute the canonical URL based on the resource, excluding tracking parameters.

### Progressive Enhancement vs. SPA

- Traditional server-rendered pages naturally include canonical tags in the initial HTML.
- SPAs should update the canonical tag during route changes, but SSR or prerendering remains the most reliable approach for SEO.

---

# Testing & Validation

Verify the implementation by:

- Viewing the page source and confirming the `<link rel="canonical">` is inside `<head>`.
- Checking that the canonical URL is correct and accessible (HTTP 200).
- Using browser DevTools to inspect the rendered `<head>`.
- Running Lighthouse for general SEO checks.
- Using accessibility tools like axe for overall page quality (though they do not specifically validate canonical tags).
- Using search engine webmaster tools (e.g., URL inspection) to verify the selected canonical URL.

---

# Pitfalls

- **Using multiple canonical tags** on the same page, which can create ambiguity.
- **Canonicalizing to the wrong page**, causing search engines to ignore or misinterpret the preferred URL.
- **Pointing to redirected, broken (404), or `noindex` pages**, which weakens the canonical signal.

## Question 2. What is prefetching in HTML?

## Question 3. What is preloading in HTML?

## Question 4. What is DNS prefetch?

## Question 5. What is the difference between `<script defer>` and placing script at bottom?

## Question 6. What is the `<noscript>` tag?

## Question 7. What is structured data in HTML?

## Question 8. What are Open Graph meta tags?

## Question 9. What is the purpose of `rel="noopener"`?

## Question 10. What is `rel="noreferrer"`?

## Question 11. How does the HTML parser work?

## Question 12. What is DOM tree construction?

## Question 13. What happens during HTML reflow and repaint?

## Question 14. What causes layout thrashing?

## Question 15. What are custom elements?

## Question 16. What is Shadow DOM?

## Question 17. What is the template tag?

## Question 18. What is slot in Web Components?

## Question 19. What is hydration in frontend frameworks?

## Question 20. What is server-side rendering (SSR)?
