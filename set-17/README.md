# Set 17

| S.No. | Question                                                                                                                                                  |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is the difference between content attributes and IDL attributes?](#question-1-what-is-the-difference-between-content-attributes-and-idl-attributes) |
| 2.    | [How does the browser handle unknown attributes?](#question-2-how-does-the-browser-handle-unknown-attributes)                                             |
| 3.    | [How does the browser handle unknown elements?](#question-3-how-does-the-browser-handle-unknown-elements)                                                 |
| 4.    | [What are reflected attributes?](#question-4-what-are-reflected-attributes)                                                                               |
| 5.    | [What is the default value of the `type` attribute in `<input>`?](#question-5-what-is-the-default-value-of-the-type-attribute-in-input)                   |
| 6.    | [What is the default value of method in `<form>`?](#question-6-what-is-the-default-value-of-method-in-form)                                               |
| 7.    | [What is the default character encoding if not specified?](#question-7-what-is-the-default-character-encoding-if-not-specified)                           |
| 8.    | [What is the purpose of `rel="alternate"`?](#question-8-what-is-the-purpose-of-relalternate)                                                              |
| 9.    | [What is `rel="author"`?](#question-9-what-is-relauthor)                                                                                                  |
| 10.   | [What is the purpose of the `manifest` attribute (legacy)?](#question-10-what-is-the-purpose-of-the-manifest-attribute-legacy)                            |
| 11.   | [What is the purpose of `http-equiv` in meta tags?](#question-11-what-is-the-purpose-of-http-equiv-in-meta-tags)                                          |
| 12.   | [What is `meta refresh`?](#question-12-what-is-meta-refresh)                                                                                              |
| 13.   | [What is the `content` attribute in meta tags?](#question-13-what-is-the-content-attribute-in-meta-tags)                                                  |
| 14.   | [What is the difference between `rel="stylesheet"` and `rel="preload"`?](#question-14-what-is-the-difference-between-relstylesheet-and-relpreload)        |
| 15.   | [What is a favicon and how is it added?](#question-15-what-is-a-favicon-and-how-is-it-added)                                                              |
| 16.   | [What are multiple icon sizes used for?](#question-16-what-are-multiple-icon-sizes-used-for)                                                              |
| 17.   | [What is Apple touch icon?](#question-17-what-is-apple-touch-icon)                                                                                        |
| 18.   | [What is theme-color meta tag?](#question-18-what-is-theme-color-meta-tag)                                                                                |
| 19.   | [What is application-name meta tag?](#question-19-what-is-application-name-meta-tag)                                                                      |
| 20.   | [What is viewport-fit?](#question-20-what-is-viewport-fit)                                                                                                |

## Question 1. What is the difference between content attributes and IDL attributes?

# Difference Between Content Attributes and IDL Attributes

## Short answer

**Content attributes** are the attributes written in the HTML markup (e.g., `value`, `checked`, `disabled`), while **IDL attributes** (Interface Definition Language attributes) are the corresponding JavaScript properties exposed by the DOM API. They often reflect each other, but **they are not always identical**, and changes to one do not always update the other.

---

# Explanation

The HTML specification distinguishes between:

- **Content attributes** → The values defined in the HTML document.
- **IDL attributes** → JavaScript properties on DOM objects (such as `HTMLElement`, `HTMLInputElement`, etc.).

Example:

```html
<input id="username" value="John" />
```

The HTML contains a **content attribute**:

```html
value="John"
```

When the browser parses the page, it creates a DOM object:

```javascript
const input = document.getElementById("username");
```

This object exposes an **IDL attribute**:

```javascript
input.value;
```

Although they may initially contain the same value, they can behave differently after the page loads.

---

## Reflection

Many HTML attributes are **reflected attributes**, meaning the HTML attribute and the DOM property stay synchronized.

Example:

```html
<input disabled />
```

```javascript
input.disabled; // true
```

```javascript
input.disabled = false;
```

Result:

```html
<input />
```

The `disabled` content attribute is removed because the IDL property reflects it.

Common reflected attributes:

- `id`
- `title`
- `hidden`
- `disabled`
- `checked` (with special behavior)
- `readonly`
- `required`
- `lang`
- `dir`

---

## Cases where they differ

### 1. `value`

This is the most common interview example.

```html
<input value="Hello" />
```

Initially:

```javascript
input.getAttribute("value"); // "Hello"
input.value; // "Hello"
```

User types:

```
World
```

Now:

```javascript
input.getAttribute("value"); // "Hello"
input.value; // "World"
```

The HTML attribute represents the **default value**, while the IDL property represents the **current value**.

---

### 2. `checked`

```html
<input type="checkbox" checked />
```

Initially:

```javascript
checkbox.checked; // true
checkbox.defaultChecked; // true
```

User unchecks it:

```javascript
checkbox.checked; // false
checkbox.defaultChecked; // true
```

The content attribute corresponds to the **default checked state**, while the IDL property reflects the current interactive state.

---

### 3. Boolean attributes

HTML:

```html
<button disabled></button>
```

or

```html
<button disabled=""></button>
```

or

```html
<button disabled="disabled"></button>
```

All mean the same thing.

In JavaScript:

```javascript
button.disabled; // true
```

Setting:

```javascript
button.disabled = false;
```

removes the attribute.

---

### 4. Attribute names vs property names

Some names differ between HTML and JavaScript.

| HTML Attribute | IDL Property                  |
| -------------- | ----------------------------- |
| `class`        | `className` (and `classList`) |
| `for`          | `htmlFor`                     |
| `readonly`     | `readOnly`                    |
| `tabindex`     | `tabIndex`                    |

These naming differences avoid conflicts with JavaScript reserved words or follow JavaScript naming conventions.

---

## Example

```html
<label for="email">Email</label>
<input id="email" value="alice@example.com" />

<script>
  const input = document.getElementById("email");

  console.log(input.getAttribute("value")); // "alice@example.com"
  console.log(input.value); // "alice@example.com"

  input.value = "bob@example.com";

  console.log(input.getAttribute("value")); // "alice@example.com"
  console.log(input.value); // "bob@example.com"

  input.setAttribute("value", "charlie@example.com");

  console.log(input.getAttribute("value")); // "charlie@example.com"
  console.log(input.value); // "bob@example.com"
</script>
```

> **Note:** The `value` property represents the live value, while the `value` content attribute stores the default value unless the element is reset or recreated.

---

# Accessibility & SEO

### Accessibility

- Content vs. IDL attributes generally do **not** change accessibility semantics directly, but using the correct DOM properties matters for interactive controls.
- For form controls, update the appropriate property (e.g., `checked`, `value`, `disabled`) so assistive technologies receive the current state.
- Use semantic HTML first; avoid relying solely on JavaScript state when native attributes are available.

### SEO

- Search engines primarily process the HTML document (content attributes) during crawling, though modern crawlers may execute JavaScript.
- Critical metadata (e.g., `lang`, `title`, `meta`, canonical links, structured data) should be present in the server-rendered HTML when possible.
- Client-side property changes alone may not benefit SEO if they are not reflected in the rendered HTML or server output.

---

# Integration & Trade-offs

- **CSS:** CSS selectors such as `[disabled]` match content attributes, while pseudo-classes like `:disabled` reflect the element's current state. Because reflected boolean attributes stay synchronized, both often work similarly for native controls.
- **JavaScript:** Use DOM properties (`element.value`, `element.checked`, `element.disabled`) for reading and updating live UI state. Use `getAttribute()`/`setAttribute()` when working with the actual HTML attributes or custom `data-*` attributes.
- **Frameworks (React/Vue/Angular):** These frameworks typically bind to DOM **properties** for interactive elements (`value`, `checked`) while synchronizing attributes where appropriate. Controlled components in React, for example, update the `value` property rather than manipulating the attribute directly.
- **SSR vs. SPA:** Server-side rendering should emit correct initial content attributes. After hydration, frameworks generally manipulate IDL properties to keep the UI responsive without constantly rewriting HTML attributes.
- **Progressive enhancement:** Ensure the initial HTML contains meaningful default attributes so the page works before JavaScript enhances behavior.

---

# Testing & Validation

- Validate markup using the WHATWG HTML checker or the W3C Nu Validator.
- Use browser DevTools to compare:
  - `element.getAttribute(name)` (content attribute)
  - `element.propertyName` (IDL attribute/property)

- Run accessibility audits with tools like axe DevTools and Lighthouse to verify that dynamic property updates (e.g., `checked`, `disabled`) are correctly exposed to assistive technologies.
- Write end-to-end tests (e.g., Playwright or Cypress) that assert both the DOM property and, where relevant, the underlying attribute.

---

# Pitfalls

- **Don't confuse `getAttribute("value")` with `element.value`;** the former returns the initial/default attribute, while the latter represents the current value for form controls.
- **Use DOM properties for interactive state** (`checked`, `selected`, `disabled`) instead of manually editing attributes.
- **Remember that not every content attribute has a one-to-one IDL property,** and some properties (such as `className`, `htmlFor`, and `readOnly`) intentionally use different names.

## Question 2. How does the browser handle unknown attributes?

## Question 3. How does the browser handle unknown elements?

## Question 4. What are reflected attributes?

## Question 5. What is the default value of the `type` attribute in `<input>`?

## Question 6. What is the default value of method in `<form>`?

## Question 7. What is the default character encoding if not specified?

## Question 8. What is the purpose of `rel="alternate"`?

## Question 9. What is `rel="author"`?

## Question 10. What is the purpose of the `manifest` attribute (legacy)?

## Question 11. What is the purpose of `http-equiv` in meta tags?

## Question 12. What is `meta refresh`?

## Question 13. What is the `content` attribute in meta tags?

## Question 14. What is the difference between `rel="stylesheet"` and `rel="preload"`?

## Question 15. What is a favicon and how is it added?

## Question 16. What are multiple icon sizes used for?

## Question 17. What is Apple touch icon?

## Question 18. What is theme-color meta tag?

## Question 19. What is application-name meta tag?

## Question 20. What is viewport-fit?
