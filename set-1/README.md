# Set 1

| S.No. | Question                                                                                                          |
| ----- | ----------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is HTML?](#question-1-what-is-html)                                                                         |
| 2.    | [What does HTML stand for?](#question-2-what-does-html-stand-for)                                                 |
| 3.    | [What is the difference between HTML and HTML5?](#question-3-what-is-the-difference-between-html-and-html5)       |
| 4.    | [What is the basic structure of an HTML document?](#question-4-what-is-the-basic-structure-of-an-html-document)   |
| 5.    | [What is the purpose of `<!DOCTYPE html>`?](#question-5-what-is-the-purpose-of-doctype-html)                      |
| 6.    | [What is the difference between `<head>` and `<body>`?](#question-6-what-is-the-difference-between-head-and-body) |

## Question 1. What is HTML?

> HTML (HyperText Markup Language) is the standard semantic markup language used to structure content on the web. It defines the meaning and hierarchy of elements like headings, paragraphs, images, and interactive components so browsers can render accessible, machine-readable documents.

**Production Implementation:**

1. **HTML5.3 Standard**
   Reference: [https://html.spec.whatwg.org/multipage/](https://html.spec.whatwg.org/multipage/)
   HTML is defined as a living standard by WHATWG, continuously evolving with modern web needs (not versioned like HTML4/5 in practice).

2. **Semantic Approach**
   Modern HTML emphasizes meaning, not presentation:
   - `<header>`, `<main>`, `<article>`, `<section>`, `<footer>` define structure
   - `<h1>`–`<h6>` define document outline
   - `<nav>` for navigation landmarks
   - ARIA roles only when semantics are insufficient (e.g., `role="dialog"` fallback)

3. **Performance**
   - Browser parses HTML incrementally (critical rendering path)
   - Use `<link rel="preload">` for critical assets
   - Use `loading="lazy"` for images/iframes
   - Minimize DOM depth for faster layout & paint
   - Defer non-critical scripts (`defer`, `async`)

4. **Accessibility**
   - Semantic tags create built-in accessibility tree
   - Proper heading hierarchy supports screen readers
   - Landmarks (`<main>`, `<nav>`) improve navigation
   - Use `alt` for images, `label` for form controls
   - Ensure keyboard navigation support (focusable elements)

**Code Example:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>What is HTML?</title>

    <!-- Performance: preload critical font -->
    <link
      rel="preload"
      href="/fonts/inter.woff2"
      as="font"
      type="font/woff2"
      crossorigin
    />
  </head>

  <body>
    <header>
      <h1>Understanding HTML</h1>
      <nav aria-label="Main navigation">
        <a href="#definition">Definition</a>
        <a href="#usage">Usage</a>
      </nav>
    </header>

    <main id="definition">
      <article>
        <h2>What is HTML?</h2>
        <p>
          HTML is the standard markup language used to structure content on the
          web.
        </p>

        <figure>
          <img
            src="html-structure.png"
            alt="Diagram showing HTML document structure"
            loading="lazy"
          />
          <figcaption>Basic structure of an HTML document</figcaption>
        </figure>
      </article>

      <section id="usage">
        <h2>Why it matters</h2>
        <p>HTML provides semantic meaning, enabling accessibility and SEO.</p>
      </section>
    </main>

    <footer>
      <small>&copy; 2026 Web Standards</small>
    </footer>
  </body>
</html>
```

**Browser Support:**

- Universal support across all modern browsers
- Semantic elements fully supported in all evergreen browsers
- Progressive enhancement recommended for older environments (IE legacy ignored in modern specs)

**Common Pitfalls:**

1. **Using divs everywhere instead of semantic tags** → hurts accessibility & SEO
2. **Missing alt attributes on images** → breaks screen reader experience
3. **Incorrect heading hierarchy (skipping h2/h3 levels)** → confuses document outline and assistive tech

## Question 2. What does HTML stand for?

> HTML stands for **HyperText Markup Language**, where “HyperText” refers to linked documents on the web and “Markup Language” means it uses tags to structure and describe content rather than execute logic.

**Production Implementation:**

1. **HTML5.3 Standard**
   Reference: [https://html.spec.whatwg.org/multipage/](https://html.spec.whatwg.org/multipage/)
   The WHATWG HTML Living Standard defines HTML as a structured language for representing documents in browsers using elements and attributes.

2. **Semantic Approach**
   Breaking down the term:
   - **HyperText** → text connected via hyperlinks (`<a href="">`)
   - **Markup** → tags like `<p>`, `<section>`, `<article>` that define meaning
   - **Language** → a standardized system understood by browsers

3. **Performance**
   While the acronym itself isn’t performance-related, HTML impacts performance through:
   - Efficient document parsing (streaming HTML parsing)
   - Reduced layout complexity via semantic structure
   - Faster rendering when minimal DOM nesting is used

4. **Accessibility**
   The “Markup Language” part is key:
   - Tags create the accessibility tree automatically
   - HyperText enables navigable content for assistive tech
   - Proper semantics reduce need for excessive ARIA overrides

**Code Example:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>HTML Meaning Example</title>
  </head>

  <body>
    <main>
      <h1>HyperText Markup Language</h1>

      <p>
        HTML stands for HyperText Markup Language. It structures content using
        semantic elements.
      </p>

      <p>
        Learn more via
        <a href="https://html.spec.whatwg.org/multipage/">
          official HTML specification </a
        >.
      </p>
    </main>
  </body>
</html>
```

**Browser Support:**

- Supported in all browsers (core concept of the web)
- No compatibility concerns—HTML is foundational to the web platform

**Common Pitfalls:**

1. **Thinking HTML is a programming language** → it is not; it does not contain logic
2. **Confusing “HyperText” with styling or design** → it refers to linking documents
3. **Ignoring semantics and only using `<div>`** → reduces accessibility and SEO effectiveness

## Question 3. What is the difference between HTML and HTML5?

> HTML is the broad markup language used for structuring web pages, while HTML5 is its modern evolution that introduced richer semantics, native multimedia support, improved form controls, and APIs like canvas and storage—making the web more application-like without plugins.

**Production Implementation:**

1. **HTML5.3 Standard**
   Reference: [https://html.spec.whatwg.org/multipage/](https://html.spec.whatwg.org/multipage/)
   Today, “HTML5” is effectively part of the **HTML Living Standard (WHATWG)**, meaning HTML is no longer versioned in practice—it continuously evolves.

2. **Semantic Approach**
   Key differences in structure and meaning:
   - **HTML (older HTML4/XHTML era)**
     - Heavy reliance on `<div>` and `<span>`
     - Limited semantic elements
     - External plugins for media (Flash, etc.)

   - **HTML5 (modern HTML)**
     - Semantic elements: `<header>`, `<main>`, `<article>`, `<section>`, `<footer>`
     - Native media: `<audio>`, `<video>`
     - Graphics: `<canvas>` and SVG integration
     - Better form semantics: `type="email"`, `required`, `pattern`
     - Built-in APIs (storage, geolocation, etc.)

3. **Performance**
   HTML5 improves performance by design:
   - Native media removes plugin overhead (no Flash)
   - Reduced JavaScript dependency for basic UI features
   - Better parsing rules (error-tolerant HTML parsing)
   - Efficient resource hints support (`preload`, `prefetch`)
   - Faster interaction with native APIs (no external bridges)

4. **Accessibility**
   HTML5 significantly improves accessibility:
   - Semantic landmarks (`<nav>`, `<main>`, `<aside>`) improve screen reader navigation
   - Built-in form validation reduces custom ARIA misuse
   - Native controls are keyboard-accessible by default
   - Better document outline structure via headings + sections

**Code Example:**

```html
<!-- HTML4-style (older approach) -->
<div id="header">
  <h1>My Website</h1>
</div>

<div id="content">
  <div class="article">
    <h2>Welcome</h2>
    <p>This is content.</p>
  </div>
</div>
```

```html
<!-- HTML5 modern semantic approach -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>HTML5 Example</title>
  </head>

  <body>
    <header>
      <h1>My Website</h1>
    </header>

    <main>
      <article>
        <h2>Welcome</h2>
        <p>This is content.</p>
      </article>

      <!-- Native video support -->
      <video controls preload="metadata">
        <source src="intro.mp4" type="video/mp4" />
        Your browser does not support video.
      </video>
    </main>

    <footer>
      <small>&copy; 2026</small>
    </footer>
  </body>
</html>
```

**Browser Support:**

- HTML (legacy elements): universally supported
- HTML5 features: fully supported in modern browsers (Chrome, Edge, Firefox, Safari)
- Some APIs (e.g., geolocation, storage) require HTTPS and permissions

**Common Pitfalls:**

1. **Thinking HTML5 is a “new version you install”** → it’s a living standard, not a fixed release
2. **Overusing `<div>` instead of semantic elements** → reduces accessibility and SEO quality
3. **Misusing HTML5 APIs without fallbacks** → older browsers or restricted environments may not support all features

## Question 4. What is the basic structure of an HTML document?

> An HTML document follows a standard hierarchical structure starting with `<!DOCTYPE html>`, followed by `<html>`, and split into `<head>` (metadata) and `<body>` (visible content). This structure ensures proper parsing, accessibility, and consistent rendering across browsers.

**Production Implementation:**

1. **HTML5.3 Standard**
   Reference: [https://html.spec.whatwg.org/multipage/](https://html.spec.whatwg.org/multipage/)
   The HTML living standard defines a required document tree: doctype declaration → html root → head + body sections, forming the foundation of all web pages.

2. **Semantic Approach**
   Modern structure emphasizes meaning and accessibility:
   - `<!DOCTYPE html>` → Enables standards mode (avoids quirks mode)
   - `<html lang="en">` → Root element + language for assistive tech
   - `<head>` → Metadata (SEO, encoding, performance hints)
   - `<body>` → Rendered content (semantic layout using `<header>`, `<main>`, `<footer>`)

   Semantic layout inside `<body>`:
   - `<header>`: site/page intro
   - `<main>`: primary content (one per page)
   - `<section>` / `<article>`: grouped content
   - `<footer>`: closing info

3. **Performance**
   - `<head>` controls critical rendering path (CSS, fonts, scripts)
   - Place CSS in `<head>` to avoid FOUC (flash of unstyled content)
   - Use `defer` for non-blocking JavaScript
   - Preload critical assets:
     - fonts (`<link rel="preload">`)
     - hero images

   - Minimal head size improves Time to First Paint (TTFP)

4. **Accessibility**
   - `<html lang>` improves screen reader pronunciation
   - `<title>` defines document context in assistive tools
   - Proper heading hierarchy inside `<body>` supports navigation
   - `<main>` landmark allows skip-to-content functionality

**Code Example:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- Metadata -->
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>Basic HTML Structure</title>

    <!-- Performance optimization -->
    <link
      rel="preload"
      href="/fonts/inter.woff2"
      as="font"
      type="font/woff2"
      crossorigin
    />

    <!-- Styles -->
    <link rel="stylesheet" href="styles.css" />
  </head>

  <body>
    <!-- Accessibility landmark -->
    <header>
      <h1>Website Title</h1>
    </header>

    <!-- Main content (only one per page) -->
    <main>
      <article>
        <h2>Page Content</h2>
        <p>This is the main content of the page.</p>
      </article>
    </main>

    <!-- Footer -->
    <footer>
      <p>&copy; 2026 Company Name</p>
    </footer>

    <!-- Non-blocking script -->
    <script src="app.js" defer></script>
  </body>
</html>
```

**Browser Support:**

- Fully supported in all modern browsers
- `<!DOCTYPE html>` ensures standards mode across all engines
- Semantic elements (`header`, `main`, `footer`) supported everywhere in evergreen browsers

**Common Pitfalls:**

1. **Missing `<!DOCTYPE html>`** → triggers quirks mode and inconsistent rendering
2. **Multiple `<main>` elements** → breaks accessibility rules (only one allowed per page)
3. **Putting scripts in `<head>` without `defer`** → blocks rendering and hurts performance

## Question 5. What is the purpose of `<!DOCTYPE html>`?

> `<!DOCTYPE html>` tells the browser to use **standards mode (HTML5 rendering mode)** instead of quirks mode, ensuring the page is parsed and rendered according to modern HTML and CSS specifications for consistent cross-browser behavior.

**Production Implementation:**

1. **HTML5.3 Standard**
   Reference: [https://html.spec.whatwg.org/multipage/syntax.html#the-doctype](https://html.spec.whatwg.org/multipage/syntax.html#the-doctype)
   In the HTML living standard, `<!DOCTYPE html>` is a required preamble that triggers **standards-compliant parsing mode** in all modern browsers.

2. **Semantic Approach**
   Although not a visible element, it has a critical semantic role in rendering behavior:
   - `<!DOCTYPE html>` → activates **standards mode**
   - Without it → browser may enter **quirks mode**
   - Quirks mode → legacy behavior for old websites (pre-HTML5 era)

   Key impact areas:
   - Box model interpretation (CSS width/height differences)
   - Font sizing behavior
   - Layout rendering consistency
   - Form and table layout rules

3. **Performance**
   - Ensures predictable rendering pipeline (DOM → CSSOM → Render Tree)
   - Avoids extra compatibility heuristics used in quirks mode
   - Improves rendering stability across engines (Blink, WebKit, Gecko)
   - Reduces layout recalculations caused by legacy assumptions

4. **Accessibility**
   - Standards mode ensures consistent accessibility tree generation
   - Screen readers rely on predictable DOM structure behavior
   - Prevents inconsistencies in landmark and layout interpretation

**Code Example:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Doctype Example</title>
  </head>

  <body>
    <h1>Standards Mode Page</h1>
    <p>This page uses <!DOCTYPE html> to ensure modern rendering behavior.</p>
  </body>
</html>
```

**Browser Support:**

- Universal across all modern browsers
- Required for HTML5+ standards mode
- If omitted, browsers may fall back to quirks mode (especially for legacy compatibility)

**Common Pitfalls:**

1. **Omitting `<!DOCTYPE html>`** → triggers quirks mode and inconsistent layout behavior
2. **Using old doctypes (HTML4/XHTML)** → unnecessary and outdated
3. **Assuming it affects page content** → it does not render visually; it only affects parsing mode

## Question 6. What is the difference between `<head>` and `<body>`?

> The `<head>` contains **metadata and resource instructions for the browser** (not directly visible content), while the `<body>` contains **all visible and interactive page content** rendered to the user. In short: _head = instructions_, _body = UI_.

**Production Implementation:**

1. **HTML5.3 Standard**
   Reference: [https://html.spec.whatwg.org/multipage/semantics.html#the-head-element](https://html.spec.whatwg.org/multipage/semantics.html#the-head-element)
   The HTML specification defines `<head>` as a container for metadata, and `<body>` as the document’s content section that is rendered.

2. **Semantic Approach**

   **`<head>` (Non-visual metadata layer)**

   Used for:
   - Document metadata: `<meta charset>`, `<meta name="viewport">`
   - SEO: `<title>`, meta description
   - Resource loading:
     - `<link rel="stylesheet">`
     - `<link rel="preload">`

   - Script configuration:
     - `<script defer>`

   - Social sharing metadata (Open Graph, Twitter cards)

   > Think: **“How the page behaves and is discovered”**

   **`<body>` (Visible content layer)**

   Used for:
   - Layout structure:
   - `<header>`, `<main>`, `<footer>`

   - Content:
     - headings, paragraphs, images, forms

   - Interactions:
     - buttons, inputs, dialogs

   - Dynamic UI controlled by JS

   > Think: **“What the user sees and interacts with”**

3. **Performance**

   **`<head>` optimizations:**
   - Critical CSS loaded early → avoids FOUC
   - Preload fonts/images for faster LCP
   - Scripts marked `defer` to avoid render blocking

   **`<body>` optimizations:**
   - Lazy-load images (`loading="lazy"`)
   - Defer non-critical DOM rendering
   - Minimize layout thrashing by structuring semantic regions

4. **Accessibility**
   - `<head>` improves **contextual understanding**:
     - `<title>` defines page name for screen readers & tabs

   - `<body>` defines **navigable accessibility tree**:
     - Landmarks (`<main>`, `<nav>`) enable skip navigation
     - Proper structure improves screen reader flow

**Code Example:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- Metadata (not visible on page) -->
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>Head vs Body Example</title>

    <!-- SEO -->
    <meta name="description" content="Explaining head vs body in HTML" />

    <!-- Performance: preload critical asset -->
    <link
      rel="preload"
      href="/fonts/inter.woff2"
      as="font"
      type="font/woff2"
      crossorigin
    />

    <!-- Styles -->
    <link rel="stylesheet" href="styles.css" />

    <!-- Script (non-blocking) -->
    <script src="app.js" defer></script>
  </head>

  <body>
    <!-- Visible content starts here -->
    <header>
      <h1>Website Title</h1>
    </header>

    <main>
      <article>
        <h2>Main Content</h2>
        <p>This content is rendered for the user.</p>
      </article>

      <button type="button">Click Me</button>
    </main>

    <footer>
      <small>&copy; 2026</small>
    </footer>
  </body>
</html>
```

**Browser Support:**

- Universally supported across all browsers
- Strict structural rules enforced by HTML parser (invalid nesting is auto-corrected by browser)

**Common Pitfalls:**

1. **Putting visible content in `<head>`** → ignored or moved by browser parser
2. **Loading blocking scripts in `<head>` without `defer`/`async`** → delays rendering
3. **Misusing `<body>` for metadata (SEO tags, title, links)** → breaks document semantics and discoverability
