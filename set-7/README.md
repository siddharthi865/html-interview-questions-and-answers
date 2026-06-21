# Set 7

| S.No. | Question                                                                                                                       |
| ----- | ------------------------------------------------------------------------------------------------------------------------------ |
| 1.    | [What is the `loading="lazy"` attribute?](#question-1-what-is-the-loadinglazy-attribute)                                       |
| 2.    | [What is the `srcset` attribute in images?](#question-2-what-is-the-srcset-attribute-in-images)                                |
| 3.    | [What is the `sizes` attribute in `<img>`?](#question-3-what-is-the-sizes-attribute-in-img)                                    |
| 4.    | [What is the `<picture>` element?](#question-4-what-is-the-picture-element)                                                    |
| 5.    | [What is the difference between `<embed>` and `<object>`?](#question-5-what-is-the-difference-between-embed-and-object)        |
| 6.    | [What is the `<track>` tag used for?](#question-6-what-is-the-track-tag-used-for)                                              |
| 7.    | [What are subtitles in video elements?](#question-7-what-are-subtitles-in-video-elements)                                      |
| 8.    | [What is autoplay in audio/video?](#question-8-what-is-autoplay-in-audiovideo)                                                 |
| 9.    | [What is the `muted` attribute?](#question-9-what-is-the-muted-attribute)                                                      |
| 10.   | [What is the `poster` attribute in `<video>`?](#question-10-what-is-the-poster-attribute-in-video)                             |
| 11.   | [What is the `autocomplete` attribute?](#question-11-what-is-the-autocomplete-attribute)                                       |
| 12.   | [What is the `novalidate` attribute?](#question-12-what-is-the-novalidate-attribute)                                           |
| 13.   | [What is the `form` attribute on input elements?](#question-13-what-is-the-form-attribute-on-input-elements)                   |
| 14.   | [What is the `formaction` attribute?](#question-14-what-is-the-formaction-attribute)                                           |
| 15.   | [What is the difference between `placeholder` and `value`?](#question-15-what-is-the-difference-between-placeholder-and-value) |
| 16.   | [What is the `step` attribute?](#question-16-what-is-the-step-attribute)                                                       |
| 17.   | [What is the difference between `radio` and `checkbox`?](#question-17-what-is-the-difference-between-radio-and-checkbox)       |
| 18.   | [What is the `<datalist>` element?](#question-18-what-is-the-datalist-element)                                                 |
| 19.   | [What is the `multiple` attribute?](#question-19-what-is-the-multiple-attribute)                                               |
| 20.   | [What is the `accept` attribute in file input?](#question-20-what-is-the-accept-attribute-in-file-input)                       |

## Question 1. What is the `loading="lazy"` attribute?

# Short answer

`loading="lazy"` is a native HTML attribute for elements like `<img>` and `<iframe>` that tells the browser to **defer loading offscreen resources until they are close to entering the viewport**. This reduces the initial page load time, saves bandwidth, and can improve performance metrics such as Largest Contentful Paint (LCP) when used appropriately.

---

# Explanation

Lazy loading is a browser optimization that delays fetching non-critical resources until they are likely to be needed.

Without lazy loading:

- The browser starts downloading all images and iframes during page load.
- Large pages with many images consume more bandwidth and delay rendering.

With `loading="lazy"`:

- Images and iframes below the fold are downloaded only when the user scrolls near them.
- Above-the-fold content loads faster.
- Browsers decide exactly when to fetch based on viewport distance and network conditions.

Example behavior:

```
Page loads
│
├── Hero image → loads immediately
├── Logo → loads immediately
├── Image 25 screens below → delayed
└── Footer iframe → delayed
```

Supported values:

| Value   | Meaning                                                    |
| ------- | ---------------------------------------------------------- |
| `lazy`  | Delay loading until near the viewport                      |
| `eager` | Load immediately (default behavior for critical resources) |

Modern browsers implement native lazy loading without requiring JavaScript libraries.

### When should you use it?

Use `loading="lazy"` for:

- Images below the fold
- Blog images
- Product gallery images
- User-generated content
- Embedded maps/videos
- Long image-heavy pages

Avoid using it for:

- Hero images
- Logo (if critical)
- Above-the-fold content
- LCP images

Those should load eagerly.

---

# Example

```html
<main>
  <h1>Travel Gallery</h1>

  <img
    src="hero.jpg"
    alt="Mountain landscape"
    width="1200"
    height="600"
    fetchpriority="high"
  />

  <section>
    <h2>More Photos</h2>

    <img
      src="beach.jpg"
      alt="Sunny beach"
      width="800"
      height="600"
      loading="lazy"
    />

    <img
      src="forest.jpg"
      alt="Forest trail"
      width="800"
      height="600"
      loading="lazy"
    />
  </section>
</main>
```

**Notes:**

- The hero image loads immediately.
- Gallery images load lazily.
- Including `width` and `height` helps browsers reserve layout space and prevents layout shifts.

---

# Accessibility & SEO

### Accessibility

- `loading="lazy"` **does not affect accessibility**.
- Always provide meaningful `alt` text for informative images.
- Decorative images should use `alt=""`.
- Native lazy loading does not change keyboard navigation or screen reader behavior.

### SEO

- Search engines can index lazy-loaded images when implemented correctly, especially with native `loading="lazy"`.
- Avoid lazy loading critical content that should be visible immediately.
- Always specify:
  - `src`
  - `alt`
  - `width`
  - `height`

These improve crawlability, accessibility, and visual stability.

---

# Integration & Trade-offs

### CSS

- Works independently of CSS.
- Setting explicit dimensions (`width`/`height` or `aspect-ratio` in CSS) helps avoid cumulative layout shift (CLS).

### JavaScript

- Native lazy loading replaces many older JavaScript solutions based on the Intersection Observer API for common use cases.
- JavaScript is still useful for advanced scenarios (custom thresholds, animations, placeholders, or analytics).

### Frameworks

- **React:** `<img loading="lazy" />`
- **Vue:** `<img loading="lazy">`
- **Angular:** `<img loading="lazy">`

The attribute is passed through to the browser like standard HTML.

### Server-side Rendering (SSR)

- Works well with SSR because the browser decides when to fetch resources after receiving the HTML.
- No extra JavaScript is required for basic lazy loading.

### Progressive Enhancement

- Browsers that support `loading="lazy"` benefit automatically.
- Older browsers simply ignore the attribute and load images eagerly, so functionality is preserved.

---

# Testing & Validation

- Validate HTML using the HTML Living Standard validator to ensure valid markup.
- Use browser DevTools (Network panel) to confirm that offscreen images are fetched only when scrolling.
- Run Lighthouse to verify performance improvements and identify if the LCP image is incorrectly lazy-loaded.
- Use axe DevTools or similar accessibility tools to ensure images still have appropriate `alt` text and accessible markup.

---

# Pitfalls

- **Don't lazy-load above-the-fold images**, especially the LCP (hero) image, as it can delay rendering and hurt Core Web Vitals.
- **Always specify `width` and `height`** (or reserve space with CSS) to prevent layout shifts.
- **Don't rely on lazy loading alone**—optimize image formats (e.g., WebP or AVIF), compress images, and use responsive images (`srcset`/`sizes`) where appropriate.

## Question 2. What is the `srcset` attribute in images?

## Question 3. What is the `sizes` attribute in `<img>`?

## Question 4. What is the `<picture>` element?

## Question 5. What is the difference between `<embed>` and `<object>`?

## Question 6. What is the `<track>` tag used for?

## Question 7. What are subtitles in video elements?

## Question 8. What is autoplay in audio/video?

## Question 9. What is the `muted` attribute?

## Question 10. What is the `poster` attribute in `<video>`?

## Question 11. What is the `autocomplete` attribute?

## Question 12. What is the `novalidate` attribute?

## Question 13. What is the `form` attribute on input elements?

## Question 14. What is the `formaction` attribute?

## Question 15. What is the difference between `placeholder` and `value`?

## Question 16. What is the `step` attribute?

## Question 17. What is the difference between `radio` and `checkbox`?

## Question 18. What is the `<datalist>` element?

## Question 19. What is the `multiple` attribute?

## Question 20. What is the `accept` attribute in file input?
