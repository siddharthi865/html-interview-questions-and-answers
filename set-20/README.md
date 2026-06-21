# Set 20

| S.No. | Question                                                                                               |
| ----- | ------------------------------------------------------------------------------------------------------ |
| 1.    | [What is HTML sanitization?](#question-1-what-is-html-sanitization)                                    |
| 2.    | [What is DOM-based XSS?](#question-2-what-is-dom-based-xss)                                            |
| 3.    | [What is attribute-based XSS?](#question-3-what-is-attribute-based-xss)                                |
| 4.    | [What is CSP nonce?](#question-4-what-is-csp-nonce)                                                    |
| 5.    | [What is CSP hash?](#question-5-what-is-csp-hash)                                                      |
| 6.    | [What is Trusted Types?](#question-6-what-is-trusted-types)                                            |
| 7.    | [What is iframe credentialless?](#question-7-what-is-iframe-credentialless)                            |
| 8.    | [What is same-site cookie behavior?](#question-8-what-is-same-site-cookie-behavior)                    |
| 9.    | [What is referrer leakage?](#question-9-what-is-referrer-leakage)                                      |
| 10.   | [What is HTML escaping?](#question-10-what-is-html-escaping)                                           |
| 11.   | [What is Web App Manifest file?](#question-11-what-is-web-app-manifest-file)                           |
| 12.   | [What is display mode in PWA?](#question-12-what-is-display-mode-in-pwa)                               |
| 13.   | [What is scope in web app manifest?](#question-13-what-is-scope-in-web-app-manifest)                   |
| 14.   | [What is installability criteria?](#question-14-what-is-installability-criteria)                       |
| 15.   | [What is splash screen configuration?](#question-15-what-is-splash-screen-configuration)               |
| 16.   | [What is maskable icon?](#question-16-what-is-maskable-icon)                                           |
| 17.   | [What is web share API integration in HTML?](#question-17-what-is-web-share-api-integration-in-html)   |
| 18.   | [What is file system access API interaction?](#question-18-what-is-file-system-access-api-interaction) |
| 19.   | [What is permission policy?](#question-19-what-is-permission-policy)                                   |
| 20.   | [What is federated credential management?](#question-20-what-is-federated-credential-management)       |

## Question 1. What is HTML sanitization?

# Short answer

**HTML sanitization** is the process of cleaning untrusted HTML by removing or modifying unsafe elements, attributes, and URLs while preserving allowed markup. Its primary purpose is to prevent **Cross-Site Scripting (XSS)** and other injection attacks when rendering user-generated content.

---

# Explanation

Sanitization is different from **escaping**:

- **Escaping** converts HTML into plain text so the browser does not interpret it.

  ```html
  &lt;script&gt;alert('XSS')&lt;/script&gt;
  ```

- **Sanitization** allows safe HTML (such as `<p>`, `<strong>`, `<a>`) but removes dangerous content like `<script>` or event handlers.

For example, given:

```html
<p>Hello</p>
<script>
  alert("XSS");
</script>
<img src="x" onerror="alert('XSS')" />
<a href="javascript:alert('XSS')">Click</a>
```

A sanitizer might produce:

```html
<p>Hello</p>
<img src="x" />
<a>Click</a>
```

or

```html
<p>Hello</p>
<a href="#">Click</a>
```

depending on its configuration.

### Why sanitization is needed

Whenever HTML comes from an **untrusted source**, such as:

- User comments
- Blog posts
- Rich text editors
- Markdown converted to HTML
- CMS content
- Third-party integrations

rendering it directly can execute malicious JavaScript.

Common threats include:

```html
<script>
  ...
</script>
```

```html
<img onerror="stealCookies()" />
```

```html
<a href="javascript:alert(1)"></a>
```

```html
<iframe src="https://malicious-site.com"></iframe>
```

A sanitizer removes or rewrites these before the browser parses them.

### How sanitization works

Most sanitizers use an **allowlist (whitelist)** approach:

- Allow safe elements
  - `p`
  - `ul`
  - `li`
  - `strong`
  - `em`
  - `a`

- Allow only safe attributes
  - `href`
  - `title`
  - `alt`

- Remove dangerous attributes
  - `onclick`
  - `onload`
  - `style` (often configurable)

- Validate URL schemes
  - Allow:
    - `https:`
    - `mailto:`

  - Reject:
    - `javascript:`
    - `data:` (depending on policy)

This is much safer than trying to block only known "bad" patterns.

---

# Example

```html
<!-- User input -->
<div>
  <strong>Welcome!</strong>
  <img src="avatar.jpg" onerror="alert('XSS')" />
  <a href="javascript:alert('XSS')">Profile</a>
</div>

<!-- Sanitized output -->
<div>
  <strong>Welcome!</strong>
  <img src="avatar.jpg" alt="" />
  <a>Profile</a>
</div>
```

> In practice, sanitization is performed by server-side code or a trusted client-side library before inserting HTML into the DOM. Simply writing HTML alone does **not** sanitize content.

---

# Accessibility & SEO

### Accessibility

- Sanitization should preserve semantic HTML like:
  - `<h1>`–`<h6>`
  - `<p>`
  - `<ul>`
  - `<table>`

- Avoid stripping useful accessibility attributes unnecessarily.
- Be careful when removing attributes:
  - Some ARIA attributes may be needed.
  - Some sanitizers allow only safe ARIA attributes.

- Preserve meaningful `alt` text on images when possible.

### SEO

- Sanitization helps prevent malicious or spammy injected content.
- Preserve semantic headings and links.
- Validate links before allowing them.
- If user-generated links open in a new tab (`target="_blank"`), add:

  ```html
  rel="noopener noreferrer"
  ```

- Sanitization does not directly improve SEO rankings, but it protects page integrity and prevents harmful injected markup.

---

# Integration & Trade-offs

### CSS

- Sanitizers often remove inline `style` attributes because CSS can sometimes be abused (e.g., older browser quirks or unwanted visual manipulation).
- Prefer predefined CSS classes over user-supplied inline styles.

### JavaScript

Never insert untrusted HTML like this:

```javascript
element.innerHTML = userInput;
```

Instead:

- Sanitize first, then insert.
- Or use `textContent` if HTML formatting is not needed.

### React

React escapes text by default:

```jsx
<div>{userInput}</div>
```

This is safe.

However:

```jsx
<div dangerouslySetInnerHTML={{ __html: userInput }} />
```

requires prior sanitization because React performs **no** sanitization here.

### Angular

Angular automatically sanitizes many HTML bindings, but bypass mechanisms (such as trusted HTML APIs) should only be used with fully trusted content.

### Vue

Using `v-html` inserts raw HTML and requires sanitization beforehand.

### Server-side rendering (SSR)

Sanitize content before storing it or before rendering on the server so every client receives safe HTML. Even with SSR, validate and sanitize any new untrusted input.

### Progressive enhancement

Sanitization is independent of JavaScript enhancements. HTML should be safe before client-side scripts execute.

---

# Testing & Validation

- Verify that malicious payloads like `<script>`, `onerror`, and `javascript:` URLs are removed.
- Test with common XSS payload collections (such as those from the OWASP XSS Filter Evasion Cheat Sheet) to validate your sanitization policy.
- Use browser developer tools to inspect the resulting DOM rather than only the source HTML.
- Run automated security and accessibility checks:
  - axe for accessibility
  - Lighthouse for best practices

- Remember that HTML validation checks markup correctness, **not** security.

---

# Pitfalls

- **Do not use regular expressions to sanitize HTML.** HTML is not a regular language, and regex-based approaches are easy to bypass.
- **Do not rely solely on client-side sanitization.** Always validate and sanitize on the server as well.
- **Prefer allowlists over blocklists.** Removing only "known bad" tags or attributes is error-prone and often misses new attack vectors.

## Question 2. What is DOM-based XSS?

## Question 3. What is attribute-based XSS?

## Question 4. What is CSP nonce?

## Question 5. What is CSP hash?

## Question 6. What is Trusted Types?

## Question 7. What is iframe credentialless?

## Question 8. What is same-site cookie behavior?

## Question 9. What is referrer leakage?

## Question 10. What is HTML escaping?

## Question 11. What is Web App Manifest file?

## Question 12. What is display mode in PWA?

## Question 13. What is scope in web app manifest?

## Question 14. What is installability criteria?

## Question 15. What is splash screen configuration?

## Question 16. What is maskable icon?

## Question 17. What is web share API integration in HTML?

## Question 18. What is file system access API interaction?

## Question 19. What is permission policy?

## Question 20. What is federated credential management?
