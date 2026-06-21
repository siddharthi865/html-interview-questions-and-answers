# Set 18

| S.No. | Question                                                                                                                                                                                         |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1.    | [What is the difference between vector and raster images?](#question-1-what-is-the-difference-between-vector-and-raster-images)                                                                  |
| 2.    | [When should you prefer SVG over PNG?](#question-2-when-should-you-prefer-svg-over-png)                                                                                                          |
| 3.    | [What are fallback mechanisms in `<video>`?](#question-3-what-are-fallback-mechanisms-in-video)                                                                                                  |
| 4.    | [How does multiple `<source>` selection work?](#question-4-how-does-multiple-source-selection-work)                                                                                              |
| 5.    | [What is media fragment URI?](#question-5-what-is-media-fragment-uri)                                                                                                                            |
| 6.    | [What is the difference between autoplay policy on desktop vs mobile?](#question-6-what-is-the-difference-between-autoplay-policy-on-desktop-vs-mobile)                                          |
| 7.    | [How does browser choose image from `srcset`?](#question-7-how-does-browser-choose-image-from-srcset)                                                                                            |
| 8.    | [What is DPR (Device Pixel Ratio)?](#question-8-what-is-dpr-device-pixel-ratio)                                                                                                                  |
| 9.    | [What is responsive images problem?](#question-9-what-is-responsive-images-problem)                                                                                                              |
| 10.   | [What is art direction in HTML images?](#question-10-what-is-art-direction-in-html-images)                                                                                                       |
| 11.   | [What is form-associated custom elements?](#question-11-what-is-form-associated-custom-elements)                                                                                                 |
| 12.   | [What is `formmethod` attribute?](#question-12-what-is-formmethod-attribute)                                                                                                                     |
| 13.   | [What is `formtarget` attribute?](#question-13-what-is-formtarget-attribute)                                                                                                                     |
| 14.   | [What is `formenctype` attribute?](#question-14-what-is-formenctype-attribute)                                                                                                                   |
| 15.   | [How does browser serialize form data?](#question-15-how-does-browser-serialize-form-data)                                                                                                       |
| 16.   | [What is URL encoding in forms?](#question-16-what-is-url-encoding-in-forms)                                                                                                                     |
| 17.   | [What is the difference between application/x-www-form-urlencoded and multipart/form-data?](#question-17-what-is-the-difference-between-applicationx-www-form-urlencoded-and-multipartform-data) |
| 18.   | [How do disabled fields behave during submission?](#question-18-how-do-disabled-fields-behave-during-submission)                                                                                 |
| 19.   | [How do readonly fields behave during submission?](#question-19-how-do-readonly-fields-behave-during-submission)                                                                                 |
| 20.   | [How can you trigger form submission programmatically without JS?](#question-20-how-can-you-trigger-form-submission-programmatically-without-js)                                                 |

## Question 1. What is the difference between vector and raster images?

# Short answer

**Vector images** are made from mathematical paths (points, lines, curves), so they can be scaled infinitely without losing quality. **Raster images** are made from pixels, so enlarging them beyond their original resolution causes pixelation and loss of detail.

---

# Explanation

The main difference lies in **how the image is represented**.

### Vector images

- Built using **mathematical equations** describing shapes, lines, and curves.
- **Resolution-independent**—they remain sharp at any size.
- Usually have **smaller file sizes** for simple graphics.
- Best for:
  - Logos
  - Icons
  - Illustrations
  - Diagrams
  - SVG graphics

Common formats:

- **SVG** (web standard)
- AI
- EPS
- PDF (can contain vector graphics)

### Raster images

- Made of a **grid of pixels**.
- **Resolution-dependent**—quality depends on the number of pixels.
- Enlarging beyond the original dimensions causes **blurriness or pixelation**.
- Better for:
  - Photographs
  - Digital artwork
  - Complex textures
  - Images with millions of colors

Common formats:

- JPEG/JPG
- PNG
- GIF
- WebP
- AVIF
- BMP

### Comparison

| Feature             | Vector                      | Raster                   |
| ------------------- | --------------------------- | ------------------------ |
| Representation      | Mathematical paths          | Pixels                   |
| Scalability         | Infinite                    | Limited                  |
| Quality when zoomed | Always sharp                | Becomes pixelated        |
| Best for            | Logos, icons, illustrations | Photos, realistic images |
| File size           | Small for simple graphics   | Depends on resolution    |
| Editing             | Easy to resize/edit shapes  | Pixel-level editing      |

---

# Example

```html
<!-- Vector image -->
<img src="logo.svg" alt="Company logo" width="150" height="150" />

<!-- Raster image -->
<img src="hero-photo.webp" alt="Mountain landscape" width="800" height="500" />
```

---

# Accessibility & SEO

- Always provide meaningful `alt` text for informative images.
- Decorative images should use `alt=""`.
- SVGs can include `<title>` and `<desc>` for additional accessibility when embedded inline.
- Use modern formats like **WebP** or **AVIF** for raster images to improve performance.
- Specify `width` and `height` attributes to reduce layout shifts (CLS).
- Use responsive images (`srcset`, `sizes`) for raster images serving multiple resolutions.

---

# Integration & Trade-offs

### CSS

- SVGs scale perfectly with CSS (`width`, `height`, `transform`).
- Raster images require higher-resolution assets for large displays (e.g., Retina).

### JavaScript

- Inline SVGs expose DOM elements that can be animated or manipulated with JavaScript.
- Raster images can only be manipulated as a whole unless processed using `<canvas>` or image-processing libraries.

### Frameworks (React/Vue/Angular)

- SVGs can often be imported as components, making them easy to style and animate.
- Raster images are typically imported as static assets and optimized during the build process.

### SSR & Progressive Enhancement

- SVGs render crisply immediately and integrate well with server-side rendering.
- Raster images benefit from lazy loading (`loading="lazy"`), responsive image techniques, and CDN optimization.

---

# Testing & Validation

- Use browser DevTools to verify image dimensions and file sizes.
- Run **Lighthouse** to check image optimization opportunities.
- Validate SVG markup if embedding inline.
- Test raster images on high-DPI displays to ensure sufficient resolution.
- Verify that all informative images have appropriate `alt` text using accessibility tools like axe.

---

# Pitfalls

- **Using raster images for logos or icons**, resulting in blurry scaling.
- **Using SVG for detailed photographs**, which can create unnecessarily large and complex files.
- **Serving oversized raster images** instead of responsive image variants, increasing page load time.

## Question 2. When should you prefer SVG over PNG?

## Question 3. What are fallback mechanisms in `<video>`?

## Question 4. How does multiple `<source>` selection work?

## Question 5. What is media fragment URI?

## Question 6. What is the difference between autoplay policy on desktop vs mobile?

## Question 7. How does browser choose image from `srcset`?

## Question 8. What is DPR (Device Pixel Ratio)?

## Question 9. What is responsive images problem?

## Question 10. What is art direction in HTML images?

## Question 11. What is form-associated custom elements?

## Question 12. What is `formmethod` attribute?

## Question 13. What is `formtarget` attribute?

## Question 14. What is `formenctype` attribute?

## Question 15. How does browser serialize form data?

## Question 16. What is URL encoding in forms?

## Question 17. What is the difference between application/x-www-form-urlencoded and multipart/form-data?

## Question 18. How do disabled fields behave during submission?

## Question 19. How do readonly fields behave during submission?

## Question 20. How can you trigger form submission programmatically without JS?
