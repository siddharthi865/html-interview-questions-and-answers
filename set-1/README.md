# Set 1

| S.No. | Question                                                                                                          |
| ----- | ----------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is HTML?](#question-1-what-is-html)                                                                         |
| 2.    | [What does HTML stand for?](#question-2-what-does-html-stand-for)                                                 |
| 3.    | [What is the difference between HTML and HTML5?](#question-3-what-is-the-difference-between-html-and-html5)       |
| 4.    | [What is the basic structure of an HTML document?](#question-4-what-is-the-basic-structure-of-an-html-document)   |
| 5.    | [What is the purpose of `<!DOCTYPE html>`?](#question-5-what-is-the-purpose-of-doctype-html)                      |
| 6.    | [What is the difference between `<head>` and `<body>`?](#question-6-what-is-the-difference-between-head-and-body) |
| 7.    | [What are HTML elements?](#question-7-what-are-html-elements)                                                     |
| 8.    | [What are HTML tags?](#question-8-what-are-html-tags)                                                             |
| 9.    | [What is the difference between tags and elements?](#question-9-what-is-the-difference-between-tags-and-elements) |
| 10.   | [What are attributes in HTML?](#question-10-what-are-attributes-in-html)                                          |

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

## Question 7. What are HTML elements?

> HTML elements are the **building blocks of a web page**, defined by a start tag, content, and an end tag (or self-closing syntax). Each element represents a specific meaning or function in the document structure, such as headings, paragraphs, links, or images.

**Production Implementation:**

1. **HTML5.3 Standard**
   Reference: [https://html.spec.whatwg.org/multipage/dom.html#elements](https://html.spec.whatwg.org/multipage/dom.html#elements)
   In the HTML living standard, an element is a structured node in the DOM tree consisting of a tag name, attributes, and content that defines document semantics.

2. **Semantic Approach**

   **Anatomy of an HTML element:**

   ```html
   <p class="intro">Hello world</p>
   ```

   - `<p>` → opening tag (defines element type)
   - `class="intro"` → attributes (metadata about the element)
   - `Hello world` → content (what is displayed)
   - `</p>` → closing tag

   **Types of elements:**
   - **Block-level elements** (structure the page):
     - `<div>`, `<section>`, `<article>`, `<header>`, `<main>`
   - **Inline elements** (flow within text):
     - `<span>`, `<a>`, `<strong>`, `<em>`
   - **Void (self-closing) elements**:
     - `<img>`, `<input>`, `<br>`, `<meta>`

   > Modern HTML prioritizes **semantic elements** over generic containers.

3. **Performance**

   HTML elements directly impact rendering performance:
   - Deeply nested elements → slower layout calculations
   - Semantic elements → better browser optimization of accessibility tree
   - Fewer DOM nodes → faster rendering and repaint
   - Void elements (like `<img>`) load independently and can be lazy-loaded:

   ```html
   <img src="photo.jpg" loading="lazy" alt="Description" />
   ```

   - Efficient structure improves:
   - Time to First Render (TTFR)
   - Layout stability (CLS reduction)

4. **Accessibility**

   HTML elements are the foundation of accessibility:
   - Screen readers interpret elements as semantic roles:
     - `<button>` → interactive control
     - `<h1>` → page heading landmark
     - `<nav>` → navigation region

   - Proper element choice reduces need for ARIA:
     - Prefer `<button>` over `<div role="button">`
     - Use `<label>` for form inputs
     - Use heading hierarchy for navigation

**Code Example:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>HTML Elements Example</title>
  </head>

  <body>
    <!-- Structural (block-level elements) -->
    <header>
      <h1>HTML Elements</h1>
    </header>

    <main>
      <section>
        <h2>What is an Element?</h2>

        <!-- Paragraph element -->
        <p>An HTML element consists of a start tag, content, and an end tag.</p>

        <!-- Inline element inside paragraph -->
        <p>
          Visit the
          <a href="https://html.spec.whatwg.org/">HTML specification</a>
          for details.
        </p>

        <!-- Void element -->
        <img src="example.png" alt="Example diagram" loading="lazy" />

        <!-- Form element -->
        <form>
          <label for="email">Email</label>
          <input id="email" type="email" required />
        </form>
      </section>
    </main>

    <footer>
      <small>&copy; 2026</small>
    </footer>
  </body>
</html>
```

**Browser Support:**

- All HTML elements are interpreted by browsers via the HTML parser (not version-dependent in modern HTML)
- Newer semantic elements (like `<main>`, `<section>`) are supported in all evergreen browsers
- Unknown elements are treated as inline by default (custom elements supported via Web Components)

**Common Pitfalls:**

1. **Using `<div>` for everything** → loses semantic meaning and harms accessibility
2. **Incorrect nesting of elements** → invalid DOM structure (e.g., block inside inline without care)
3. **Ignoring semantic intent** → using elements purely for styling instead of meaning

## Question 8. What are HTML tags?

> HTML tags are the **syntactic markers** used to define the start and end of HTML elements. They are written inside angle brackets (e.g., `<p>`, `</p>`) and tell the browser how to interpret and structure content, but they are not the elements themselves.

**Production Implementation:**

1. **HTML5.3 Standard**
   Reference: [https://html.spec.whatwg.org/multipage/syntax.html#syntax-elements](https://html.spec.whatwg.org/multipage/syntax.html#syntax-elements)
   In the HTML living standard, tags are part of the syntax used to construct **elements**, which then form the DOM tree.

2. **Semantic Approach**

   **Tags vs Elements (important distinction)**

   | Concept        | Meaning                            | Example                       |
   | -------------- | ---------------------------------- | ----------------------------- |
   | **Tag**        | Syntax marker                      | `<p>` or `</p>`               |
   | **Element**    | Complete structure (tag + content) | `<p>Hello</p>`                |
   | **Node (DOM)** | Runtime representation in browser  | Parsed element in memory tree |

   ### Types of HTML tags

   #### 1. Opening tag

   Defines the start of an element:

   ```html
   <p></p>
   ```

   #### 2. Closing tag

   Defines the end of an element:

   ```html
   </p>
   ```

   #### 3. Self-closing (void) tags

   Do not require a closing tag:

   ```html
   <img />
   <input />
   <br />
   <meta />
   ```

   > Key point: **Tags are syntax; elements are meaning.**

3. **Performance**

   While tags themselves don’t affect performance directly, they influence how efficiently the browser parses HTML:
   - Well-formed tags → faster parsing and DOM construction
   - Incorrect or missing closing tags → browser auto-correction adds parsing overhead
   - Void tags reduce DOM complexity (no children nodes)
   - Proper structure improves:
     - DOM tree stability
     - Render tree construction speed

4. **Accessibility**

   Tags indirectly impact accessibility by defining correct elements:
   - `<button>` tag → creates an interactive control in accessibility tree
   - `<h1>`–`<h6>` tags → build document outline for screen readers
   - `<label>` tags → associate form inputs for assistive tech

   Incorrect or missing tags can:
   - Break semantic mapping
   - Force reliance on ARIA (less ideal than native semantics)

**Code Example:**

```html id="html-tags-example"
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>HTML Tags Example</title>
  </head>

  <body>
    <!-- Opening and closing tags form an element -->
    <p>This is a paragraph element.</p>

    <!-- Self-closing (void) tag -->
    <img src="image.jpg" alt="Example image" />

    <!-- Nested tags forming structured elements -->
    <a href="https://example.com"> Click here </a>

    <!-- Form example -->
    <form>
      <label for="name">Name</label>
      <input id="name" type="text" />
    </form>
  </body>
</html>
```

**Browser Support:**

- All HTML tags are universally supported as part of the HTML parsing algorithm
- Unknown tags are treated as generic inline elements (useful for Web Components)
- Void tags must not have closing tags in strict parsing mode, though browsers are forgiving

**Common Pitfalls:**

1. **Confusing tags with elements** → tags are syntax, elements are DOM structures
2. **Missing closing tags in non-void elements** → causes unpredictable DOM correction
3. **Using invalid nesting** → browser silently fixes structure, leading to layout bugs

## Question 9. What is the difference between tags and elements?

> HTML tags are the **syntax markers** (like `<p>` and `</p>`), while an HTML element is the **complete structure** that includes the tags plus the content between them. In short: tags are the brackets; elements are the actual DOM structure the browser creates.

**Production Implementation:**

1. **HTML5.3 Standard**
   Reference: [https://html.spec.whatwg.org/multipage/dom.html#elements](https://html.spec.whatwg.org/multipage/dom.html#elements)
   The HTML specification defines an **element** as a node in the DOM tree created from parsed tags, attributes, and content. Tags are just part of the parsing syntax.

2. **Semantic Approach**

   ### Clear distinction

   | Concept     | Definition                    | Example         |
   | ----------- | ----------------------------- | --------------- |
   | **Tag**     | Syntax used in HTML source    | `<p>` or `</p>` |
   | **Element** | Full structured object in DOM | `<p>Hello</p>`  |

   ### Breakdown

   **Tags (source code level)**
   - Opening tag: `<h1>`
   - Closing tag: `</h1>`
   - Self-closing tag: `<img />`

   > Tags exist only in the HTML markup text.

   **Elements (browser / DOM level)**

   An element includes:
   - Opening tag
   - Content
   - Closing tag (if applicable)
   - Attributes
   - DOM representation in memory

     Example:

     ```html id="element-example"
     <p class="intro">Hello world</p>
     ```

     This becomes a **DOM element node** like:
     - Type: paragraph element
     - Attributes: class="intro"
     - Content: "Hello world"

3. **Performance**

   Understanding this difference matters for rendering:
   - Browser parses **tags → builds DOM elements**
   - More invalid tags → more corrective parsing overhead
   - Clean tag structure → faster DOM construction
   - Void tags (`<img>`, `<input>`) reduce tree depth

   Efficient markup improves:
   - Time to DOMContentLoaded
   - Layout stability
   - Memory usage of DOM tree

4. **Accessibility**
   - Accessibility APIs do not see “tags”
   - They interact with **elements in the accessibility tree**

   Examples:
   - `<button>` tag → becomes a **button element role**
   - `<h1>` tag → becomes a **heading landmark**
   - `<a>` tag → becomes a **link element**

   If tags are misused (e.g., `<div>` instead of `<button>`), accessibility must be manually patched with ARIA, which is less reliable than native elements.

**Code Example:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Tags vs Elements</title>
  </head>

  <body>
    <!-- Tags -->
    <!-- <p> and </p> are tags -->

    <!-- Element -->
    <p class="message">Hello world</p>

    <!-- Another element -->
    <a href="https://example.com">Visit site</a>

    <!-- Void element (only one tag, still an element) -->
    <img src="photo.jpg" alt="Example image" />
  </body>
</html>
```

**Browser Support:**

- All browsers interpret tags during parsing to create DOM elements
- Invalid or missing tags are auto-corrected by HTML parser (forgiving syntax model)
- Modern DOM APIs operate on **elements, not tags**

**Common Pitfalls:**

1. **Thinking tags exist at runtime** → they don’t; only elements exist in the DOM
2. **Confusing element with inner text** → element includes structure + content
3. **Ignoring void elements** → they are elements but have no closing tags

## Question 10. What are attributes in HTML?

> HTML attributes are **key-value pairs added to tags** that provide additional information about an element, such as behavior, identity, accessibility, or configuration (e.g., `class`, `id`, `href`, `alt`). They modify how an element behaves or is interpreted, but are not part of its visible content.

**Production Implementation:**

1. **HTML5.3 Standard**
   Reference: [https://html.spec.whatwg.org/multipage/dom.html#attributes](https://html.spec.whatwg.org/multipage/dom.html#attributes)
   In the HTML living standard, attributes are defined as **name-value pairs associated with elements in the DOM**, influencing rendering, behavior, and accessibility.

2. **Semantic Approach**

   ### Anatomy of attributes

   ```html id="attr-example"
   <a href="https://example.com" target="_blank" rel="noopener"> Visit site </a>
   ```

   - `href` → defines destination (behavior)
   - `target` → controls navigation behavior
   - `rel` → security + relationship metadata

   ### Common attribute categories

   **1. Global attributes (usable on most elements)**
   - `id` → unique identifier
   - `class` → styling/hooks
   - `data-*` → custom data storage
   - `title` → tooltip/accessibility hint
   - `lang` → language declaration

   **2. Element-specific attributes**
   - `<img src="..." alt="...">`
   - `<input type="email" required>`
   - `<a href="...">`

   #### 3. Boolean attributes

   Presence = true:

   ```html id="bool-attr"
   <input type="checkbox" checked />
   ```

   No value needed (or value equals name in legacy HTML).

3. **Performance**

   Attributes can directly impact performance:
   - `loading="lazy"` → defers image loading, improves LCP
   - `defer` / `async` (script attributes) → prevent render blocking
   - `fetchpriority="high"` → optimizes critical resource loading
   - Excessive DOM attributes → slightly increase memory footprint

   Efficient attribute usage improves:
   - First Contentful Paint (FCP)
   - Largest Contentful Paint (LCP)
   - Network prioritization

4. **Accessibility**

   Attributes are critical for accessibility:
   - `alt` → describes images for screen readers
   - `aria-*` → enhances or modifies accessibility semantics
   - `for` (in `<label>`) → associates label with input
   - `tabindex` → controls keyboard navigation
   - `role` → defines element purpose when semantics are insufficient

   Example:

   ```html id="accessibility-attr"
   <img src="chart.png" alt="Sales growth chart for 2026" />

   <label for="email">Email</label>
   <input id="email" type="email" required aria-describedby="email-help" />
   ```

**Code Example:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>HTML Attributes</title>
  </head>

  <body>
    <!-- Global attributes -->
    <h1 id="main-title" class="title">HTML Attributes</h1>

    <!-- Link attributes -->
    <a href="https://example.com" target="_blank" rel="noopener noreferrer">
      External Link
    </a>

    <!-- Image attributes (accessibility-critical) -->
    <img src="hero.jpg" alt="Developer working on laptop" loading="lazy" />

    <!-- Form attributes -->
    <form>
      <label for="email">Email</label>
      <input id="email" type="email" required placeholder="Enter your email" />
    </form>

    <!-- Custom data attributes -->
    <button data-action="submit-form">Submit</button>
  </body>
</html>
```

**Browser Support:**

- All standard HTML attributes are universally supported
- `data-*` attributes are fully supported in all modern browsers
- ARIA attributes supported in all major assistive technology ecosystems

**Common Pitfalls:**

1. **Using non-standard attributes without `data-*`** → invalid HTML, unpredictable behavior
2. **Missing `alt` on images** → accessibility failure (WCAG violation)
3. **Overusing ARIA instead of native attributes** → reduces accessibility quality
4. **Misusing boolean attributes (`checked="false"`)** → still evaluates as true
