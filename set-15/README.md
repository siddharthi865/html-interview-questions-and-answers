# Set 15

| S.No. | Question                                                                                                                    |
| ----- | --------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is same-origin policy?](#question-1-what-is-same-origin-policy)                                                       |
| 2.    | [What is sandbox token behavior?](#question-2-what-is-sandbox-token-behavior)                                               |
| 3.    | [What is form action hijacking?](#question-3-what-is-form-action-hijacking)                                                 |
| 4.    | [What is HTML injection?](#question-4-what-is-html-injection)                                                               |
| 5.    | [How can improper HTML structure cause vulnerabilities?](#question-5-how-can-improper-html-structure-cause-vulnerabilities) |
| 6.    | [What is mixed content?](#question-6-what-is-mixed-content)                                                                 |
| 7.    | [What is subresource integrity (SRI)?](#question-7-what-is-subresource-integrity-sri)                                       |
| 8.    | [What is CORS behavior in HTML tags?](#question-8-what-is-cors-behavior-in-html-tags)                                       |
| 9.    | [How does the browser sanitize HTML?](#question-9-how-does-the-browser-sanitize-html)                                       |
| 10.   | [What is DOM clobbering?](#question-10-what-is-dom-clobbering)                                                              |
| 11.   | [What is critical CSS and how does HTML support it?](#question-11-what-is-critical-css-and-how-does-html-support-it)        |
| 12.   | [What is streaming HTML?](#question-12-what-is-streaming-html)                                                              |
| 13.   | [What is incremental rendering?](#question-13-what-is-incremental-rendering)                                                |
| 14.   | [How does SSR differ from static HTML?](#question-14-how-does-ssr-differ-from-static-html)                                  |
| 15.   | [What is hydration mismatch?](#question-15-what-is-hydration-mismatch)                                                      |
| 16.   | [What is prerendering?](#question-16-what-is-prerendering)                                                                  |
| 17.   | [What is edge rendering?](#question-17-what-is-edge-rendering)                                                              |
| 18.   | [What is micro-frontend architecture in HTML?](#question-18-what-is-micro-frontend-architecture-in-html)                    |
| 19.   | [How does HTML interact with service workers?](#question-19-how-does-html-interact-with-service-workers)                    |
| 20.   | [What is HTML's role in progressive web apps (PWA)?](#question-20-what-is-htmls-role-in-progressive-web-apps-pwa)           |

## Question 1. What is same-origin policy?

# What is the Same-Origin Policy?

## Short answer

The **Same-Origin Policy (SOP)** is a browser security mechanism that prevents a web page from accessing data or resources from a different **origin** (scheme/protocol + host + port) unless the target explicitly allows it. It protects users from attacks such as data theft, session hijacking, and unauthorized access between websites.

---

## Explanation

The **origin** of a URL is defined by three components:

- **Protocol (scheme):** `http` vs `https`
- **Host (domain):** `example.com`
- **Port:** `80`, `443`, `3000`, etc.

Two URLs are considered **same-origin** only if **all three** match.

| URL                         | Same Origin as `https://example.com`? | Reason                                |
| --------------------------- | ------------------------------------- | ------------------------------------- |
| `https://example.com/about` | ✅ Yes                                | Same protocol, host, and default port |
| `https://blog.example.com`  | ❌ No                                 | Different subdomain                   |
| `http://example.com`        | ❌ No                                 | Different protocol                    |
| `https://example.com:8080`  | ❌ No                                 | Different port                        |

### Why SOP exists

Without SOP, a malicious website could:

- Read your online banking information
- Access emails from another tab
- Steal authentication cookies or sensitive data
- Perform actions on behalf of authenticated users

SOP isolates websites from each other, making browsers much safer.

### What SOP restricts

SOP primarily prevents JavaScript from:

- Reading another site's DOM
- Accessing cookies or localStorage from another origin
- Reading responses from cross-origin AJAX/Fetch requests
- Accessing IndexedDB from another origin

Example:

```javascript
// Running on https://siteA.com

fetch("https://siteB.com/api/user").then((res) => res.json()); // ❌ Blocked unless siteB enables CORS
```

### What is still allowed

SOP does **not** block loading many cross-origin resources.

Examples include:

- Images (`<img>`)
- CSS (`<link>`)
- JavaScript (`<script>`)
- Fonts (subject to CORS in many cases)
- Videos
- Iframes (loading is allowed, but reading their contents is restricted)

For example:

```html
<img src="https://cdn.example.com/logo.png" alt="Logo" />
```

The image can load, but JavaScript cannot inspect pixels from a cross-origin image drawn to a canvas unless appropriate CORS headers are present.

### How websites allow cross-origin access

The standard mechanism is **Cross-Origin Resource Sharing (CORS)**.

Server example:

```
Access-Control-Allow-Origin: https://example.com
```

This tells the browser that the specified origin is allowed to read the response.

---

## Example

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Same-Origin Policy Example</title>
  </head>
  <body>
    <button id="load">Load Data</button>

    <script>
      document.getElementById("load").addEventListener("click", async () => {
        try {
          const response = await fetch("https://api.example.com/data");
          const data = await response.json();
          console.log(data);
        } catch (err) {
          console.error("Blocked unless the server allows CORS.");
        }
      });
    </script>
  </body>
</html>
```

> This example requires JavaScript. The request succeeds only if the server responds with appropriate CORS headers.

---

## Accessibility & SEO

### Accessibility

- Same-Origin Policy has **no direct accessibility impact**.
- If cross-origin content fails to load, ensure users receive accessible error messages (e.g., via an ARIA live region) rather than silent failures.
- Use semantic HTML so the page remains usable even if external resources are unavailable.

### SEO

- SOP itself does not affect indexing.
- Search engines can crawl linked resources independently.
- Cross-origin APIs used for client-side rendering should not be relied upon as the only source of indexable content; prefer server-side rendering or prerendering for important SEO content.

---

## Integration & Trade-offs

### CSS

- External stylesheets can be loaded across origins.
- CSS cannot bypass SOP to read protected cross-origin data.

### JavaScript

- `fetch()` and `XMLHttpRequest` are restricted by SOP unless the server enables CORS.
- `window.postMessage()` provides a secure way for documents from different origins (such as iframes) to communicate.

### Client-side frameworks

- **React/Vue/Angular** applications commonly consume APIs on different origins.
- During development, proxy servers (e.g., Vite or webpack dev server proxies) are often used to avoid CORS issues.
- In production, configure the API to return the correct CORS headers.

### Server-side rendering (SSR)

- SSR fetches data on the server, where browser SOP does not apply.
- Browser-based API requests after hydration are still subject to SOP and CORS.

### Progressive enhancement

- Design pages so core functionality works without relying entirely on cross-origin JavaScript.
- Gracefully handle failed API requests and provide fallback content when possible.

---

## Testing & Validation

- Verify cross-origin requests in browser DevTools (Network and Console).
- Use browser security messages to identify blocked requests due to missing or incorrect CORS headers.
- Validate HTML with the WHATWG HTML checker or W3C validator.
- Run accessibility audits with tools such as axe DevTools and Lighthouse to ensure error states remain accessible.
- Test across different origins (localhost, staging, production) because protocol, host, and port differences can affect behavior.

---

## Pitfalls

- **Assuming subdomains are the same origin.** `app.example.com` and `example.com` are different origins.
- **Confusing SOP with CORS.** SOP blocks access by default; CORS is the mechanism servers use to selectively allow cross-origin access.
- **Thinking SOP blocks all cross-origin requests.** Browsers often allow sending requests or loading resources, but restrict JavaScript from reading the response unless permitted.

## Question 2. What is sandbox token behavior?

## Question 3. What is form action hijacking?

## Question 4. What is HTML injection?

## Question 5. How can improper HTML structure cause vulnerabilities?

## Question 6. What is mixed content?

## Question 7. What is subresource integrity (SRI)?

## Question 8. What is CORS behavior in HTML tags?

## Question 9. How does the browser sanitize HTML?

## Question 10. What is DOM clobbering?

## Question 11. What is critical CSS and how does HTML support it?

## Question 12. What is streaming HTML?

## Question 13. What is incremental rendering?

## Question 14. How does SSR differ from static HTML?

## Question 15. What is hydration mismatch?

## Question 16. What is prerendering?

## Question 17. What is edge rendering?

## Question 18. What is micro-frontend architecture in HTML?

## Question 19. How does HTML interact with service workers?

## Question 20. What is HTML’s role in progressive web apps (PWA)?
