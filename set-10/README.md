# Set 10

| S.No. | Question                                                                                                                                            |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is XSS (Cross-Site Scripting)?](#question-1-what-is-xss-cross-site-scripting)                                                                 |
| 2.    | [How can HTML help prevent XSS?](#question-2-how-can-html-help-prevent-xss)                                                                         |
| 3.    | [What is Content Security Policy (CSP)?](#question-3-what-is-content-security-policy-csp)                                                           |
| 4.    | [What is the purpose of `integrity` attribute?](#question-4-what-is-the-purpose-of-integrity-attribute)                                             |
| 5.    | [What is `crossorigin` attribute?](#question-5-what-is-crossorigin-attribute)                                                                       |
| 6.    | [What is clickjacking?](#question-6-what-is-clickjacking)                                                                                           |
| 7.    | [How does iframe sandboxing improve security?](#question-7-how-does-iframe-sandboxing-improve-security)                                             |
| 8.    | [What is referrer policy?](#question-8-what-is-referrer-policy)                                                                                     |
| 9.    | [What is the difference between HTTP-only cookies and localStorage?](#question-9-what-is-the-difference-between-http-only-cookies-and-localstorage) |
| 10.   | [How can form inputs be exploited?](#question-10-how-can-form-inputs-be-exploited)                                                                  |
| 11.   | [What is microdata in HTML?](#question-11-what-is-microdata-in-html)                                                                                |
| 12.   | [What is RDFa?](#question-12-what-is-rdfa)                                                                                                          |
| 13.   | [What is the manifest attribute?](#question-13-what-is-the-manifest-attribute)                                                                      |
| 14.   | [What is the `ping` attribute in anchor tags?](#question-14-what-is-the-ping-attribute-in-anchor-tags)                                              |
| 15.   | [What are access keys?](#question-15-what-are-access-keys)                                                                                          |
| 16.   | [What is the `download` attribute?](#question-16-what-is-the-download-attribute)                                                                    |
| 17.   | [What is the difference between `<bdi>` and `<bdo>`?](#question-17-what-is-the-difference-between-bdi-and-bdo)                                      |
| 18.   | [What is bidirectional text in HTML?](#question-18-what-is-bidirectional-text-in-html)                                                              |
| 19.   | [What are obsolete HTML tags?](#question-19-what-are-obsolete-html-tags)                                                                            |
| 20.   | [How does HTML handle internationalization (i18n)?](#question-20-how-does-html-handle-internationalization-i18n)                                    |

## Question 1. What is XSS (Cross-Site Scripting)?

# Short answer

**Cross-Site Scripting (XSS)** is a web security vulnerability where an attacker injects malicious JavaScript into a web page that executes in another user's browser. While HTML itself does not execute JavaScript, insecure handling of HTML content (e.g., rendering untrusted input) can enable XSS. Preventing XSS primarily involves **escaping output, sanitizing HTML, validating input, using Content Security Policy (CSP), and avoiding unsafe DOM APIs.**

---

# Explanation

XSS occurs when an application includes **untrusted user input** in HTML without proper escaping or sanitization, allowing the browser to interpret it as executable code.

The injected JavaScript runs **with the permissions of the vulnerable website's origin**, allowing attackers to:

- Steal session cookies (if not protected with `HttpOnly`)
- Perform actions on behalf of the user
- Read sensitive page data
- Modify page content
- Redirect users to malicious websites
- Capture keystrokes or credentials

### Types of XSS

### 1. Stored (Persistent) XSS

The malicious script is stored on the server (database, comments, forum posts, profiles).

Example flow:

1. Attacker posts:

   ```html
   <script>
     alert("Hacked");
   </script>
   ```

2. Server stores it.
3. Every visitor loads the page.
4. Browser executes the script.

Example:

```html
<p>User comment:</p>
<div>
  <!-- Dangerous -->
  <script>
    alert("XSS");
  </script>
</div>
```

---

### 2. Reflected XSS

The payload comes from the URL or request and is immediately reflected into the response.

Example:

```
https://example.com/search?q=<script>alert(1)</script>
```

If the server renders:

```html
<h2>
  Results for:
  <script>
    alert(1);
  </script>
</h2>
```

the browser executes it.

---

### 3. DOM-based XSS

The vulnerability exists entirely in client-side JavaScript.

Unsafe code:

```javascript
element.innerHTML = location.hash.substring(1);
```

URL:

```
https://site.com/#<img src=x onerror=alert(1)>
```

Because `innerHTML` parses HTML, the attack executes.

Safer approach:

```javascript
element.textContent = location.hash.substring(1);
```

---

## Why HTML matters

HTML is the document the browser parses.

If user input becomes part of HTML like:

```html
<div>User input here</div>
```

without escaping, an attacker can inject HTML elements such as:

```html
<script>
  ...
</script>
```

or

```html
<img src="x" onerror="alert(1)" />
```

The browser treats them as markup rather than plain text.

---

# Example

A safe example that displays user input as text instead of HTML:

```html
<label for="comment">Comment</label>
<textarea id="comment"></textarea>

<p>Preview:</p>
<div id="preview"></div>

<script>
  const textarea = document.getElementById("comment");
  const preview = document.getElementById("preview");

  textarea.addEventListener("input", () => {
    // Safe: renders text, not HTML
    preview.textContent = textarea.value;
  });
</script>
```

> **Note:** If your application intentionally supports user-authored HTML (e.g., rich-text editors), sanitize it with a trusted HTML sanitizer before inserting it into the DOM. Never insert untrusted content directly with `innerHTML`.

---

# Accessibility & SEO

### Accessibility

- XSS has no direct accessibility benefit or impact, but malicious scripts can:
  - Break keyboard navigation
  - Alter focus unexpectedly
  - Replace accessible content
  - Interfere with assistive technologies

- Use semantic HTML regardless of security.
- Avoid unnecessary ARIA attributes that could complicate dynamic content updates.

### SEO

- Search engines may flag compromised pages.
- Injected spam content can damage search rankings.
- XSS can lead to defacement or hidden links that harm site reputation.
- Keep HTML clean and escape all user-generated content before rendering.

---

# Integration & Trade-offs

### HTML + JavaScript

Avoid:

```javascript
element.innerHTML = userInput;
```

Prefer:

```javascript
element.textContent = userInput;
```

---

### React

React automatically escapes values:

```jsx
<div>{userInput}</div>
```

Unsafe:

```jsx
<div dangerouslySetInnerHTML={{ __html: userInput }} />
```

Only use `dangerouslySetInnerHTML` with sanitized HTML.

---

### Vue

Safe:

```vue
{{ userInput }}
```

Unsafe:

```vue
<div v-html="userInput"></div>
```

Sanitize content before using `v-html`.

---

### Angular

Angular escapes template interpolations by default and sanitizes many HTML bindings. Bypassing these protections (e.g., with `DomSanitizer.bypassSecurityTrustHtml`) should only be done after careful review of trusted content.

---

### Server-side Rendering (SSR)

- Escape all dynamic HTML output on the server.
- Use context-aware encoding (HTML, attribute, JavaScript, URL).
- Never trust client-side validation alone.

---

### Progressive Enhancement

- Security should not depend on JavaScript.
- Validate and escape data on the server, even if the client sanitizes it.

---

# Testing & Validation

Use a combination of:

- HTML validation to ensure valid markup.
- Accessibility testing with **axe DevTools**, **Lighthouse**, and screen readers.
- Security testing using common XSS payloads (in a safe testing environment).
- Static analysis and secure code reviews to identify unsafe APIs such as `innerHTML`, `outerHTML`, `document.write()`, and `insertAdjacentHTML()`.
- Enable a strong **Content Security Policy (CSP)** to reduce the impact of XSS if a vulnerability slips through.

---

# Pitfalls

- **Never trust user input**, even if it comes from your own users.
- **Do not use `innerHTML`** with untrusted data; prefer `textContent` or safe templating.
- **Do not rely solely on client-side validation**—always validate, encode, and sanitize on the server where appropriate.

## Question 2. How can HTML help prevent XSS?

## Question 3. What is Content Security Policy (CSP)?

## Question 4. What is the purpose of `integrity` attribute?

## Question 5. What is `crossorigin` attribute?

## Question 6. What is clickjacking?

## Question 7. How does iframe sandboxing improve security?

## Question 8. What is referrer policy?

## Question 9. What is the difference between HTTP-only cookies and localStorage?

## Question 10. How can form inputs be exploited?

## Question 11. What is microdata in HTML?

## Question 12. What is RDFa?

## Question 13. What is the manifest attribute?

## Question 14. What is the `ping` attribute in anchor tags?

## Question 15. What are access keys?

## Question 16. What is the `download` attribute?

## Question 17. What is the difference between `<bdi>` and `<bdo>`?

## Question 18. What is bidirectional text in HTML?

## Question 19. What are obsolete HTML tags?

## Question 20. How does HTML handle internationalization (i18n)?
