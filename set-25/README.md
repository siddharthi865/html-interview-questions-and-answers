# Set 25

| S.No. | Question                                                                                                                     |
| ----- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is credentialless iframe?](#question-1-what-is-credentialless-iframe)                                                  |
| 2.    | [What is fenced frames?](#question-2-what-is-fenced-frames)                                                                  |
| 3.    | [What is portal element?](#question-3-what-is-portal-element)                                                                |
| 4.    | [What is navigation API integration?](#question-4-what-is-navigation-api-integration)                                        |
| 5.    | [What is same-origin-domain relaxation?](#question-5-what-is-same-origin-domain-relaxation)                                  |
| 6.    | [What is document.domain risk?](#question-6-what-is-documentdomain-risk)                                                     |
| 7.    | [What is HTML parsing reentrancy?](#question-7-what-is-html-parsing-reentrancy)                                              |
| 8.    | [What is synchronous section in parser?](#question-8-what-is-synchronous-section-in-parser)                                  |
| 9.    | [What is origin trial in HTML features?](#question-9-what-is-origin-trial-in-html-features)                                  |
| 10.   | [What is feature policy vs permission policy?](#question-10-what-is-feature-policy-vs-permission-policy)                     |
| 11.   | [What is HTML fragment parsing?](#question-11-what-is-html-fragment-parsing)                                                 |
| 12.   | [What is template instantiation proposal?](#question-12-what-is-template-instantiation-proposal)                             |
| 13.   | [What is structured cloning algorithm relation to HTML?](#question-13-what-is-structured-cloning-algorithm-relation-to-html) |
| 14.   | [What is HTML event loop integration?](#question-14-what-is-html-event-loop-integration)                                     |
| 15.   | [What is task vs microtask in HTML spec?](#question-15-what-is-task-vs-microtask-in-html-spec)                               |
| 16.   | [What is browsing context?](#question-16-what-is-browsing-context)                                                           |
| 17.   | [What is nested browsing context?](#question-17-what-is-nested-browsing-context)                                             |
| 18.   | [What is top-level browsing context?](#question-18-what-is-top-level-browsing-context)                                       |
| 19.   | [What is session history entry?](#question-19-what-is-session-history-entry)                                                 |
| 20.   | [What is navigation timing integration with HTML?](#question-20-what-is-navigation-timing-integration-with-html)             |

## Question 1. What is credentialless iframe?

# Short answer

A **credentialless iframe** is an `<iframe>` loaded **without cookies, HTTP authentication, or other user credentials**. It allows embedding third-party content in a more privacy-preserving way while still enabling pages using **Cross-Origin-Embedder-Policy (COEP)** to embed resources that otherwise couldn't be loaded due to missing cross-origin isolation headers.

---

# Explanation

Normally, when a browser loads a cross-origin `<iframe>`, it sends credentials such as:

- Cookies
- HTTP authentication headers
- TLS client certificates (if applicable)

These credentials allow the embedded site to recognize the user.

A **credentialless iframe** creates a **new, temporary, anonymous context** for the embedded document:

- No cookies are sent.
- Existing login sessions are unavailable.
- Storage (cookies, localStorage, IndexedDB, etc.) is isolated from the user's normal browsing session.
- The embedded page behaves as if it's being opened by a brand-new anonymous visitor.

The primary motivation is enabling **cross-origin isolation**.

Normally, if a page uses:

```http
Cross-Origin-Embedder-Policy: require-corp
```

it cannot embed arbitrary third-party iframes unless those sites explicitly opt in using CORP or CORS headers.

Using:

```html
<iframe credentialless></iframe>
```

allows certain third-party content to be embedded without exposing user credentials, making it compatible with COEP in many cases.

This is useful for applications that need APIs requiring cross-origin isolation, such as:

- `SharedArrayBuffer`
- High-resolution timers
- WebAssembly threading

without requiring every embedded third-party site to change its headers.

---

# Example

```html
<iframe
  src="https://example-third-party.com/widget"
  credentialless
  width="600"
  height="400"
  title="Weather widget"
>
</iframe>
```

The browser loads:

- the iframe without cookies,
- without authentication,
- in an isolated storage environment.

If JavaScript inside the iframe checks:

```javascript
document.cookie;
```

it will appear empty (unless cookies are set within that temporary credentialless context).

---

# Accessibility & SEO

### Accessibility

- Always provide a descriptive `title` attribute on `<iframe>` so assistive technologies can identify its purpose.
- The `credentialless` attribute has **no impact on accessibility** or keyboard navigation.
- If the iframe is decorative or non-essential, consider whether it should be omitted entirely or replaced with semantic HTML.

### SEO

- Search engines generally do **not** index iframe content as part of the embedding page.
- `credentialless` does not affect SEO directly.
- Critical content should not rely solely on an iframe if you want it indexed with the host page.

---

# Integration & Trade-offs

### Benefits

- Improves user privacy by omitting credentials.
- Enables embedding some third-party resources in pages using COEP.
- Helps applications that require cross-origin isolation.
- Reduces cross-site tracking through embedded content.

### Limitations

- Logged-in experiences won't work because cookies and authentication are unavailable.
- Third-party widgets that depend on user sessions (chat, payment, account dashboards, personalized feeds) may not function correctly.
- Browser support is more limited than established iframe features, so progressive enhancement or fallbacks may be necessary.

### Framework integration

- In React:

```jsx
<iframe src="https://example.com" credentialless title="Example" />
```

- Frameworks such as React, Vue, and Angular simply render the HTML attribute; the browser enforces the behavior.
- Server-side rendering does not change how `credentialless` works, since enforcement happens in the browser after the page is loaded.

---

# Testing & Validation

- Verify in browser DevTools that requests from the iframe are sent without cookies or other credentials.
- Test both authenticated and anonymous scenarios to ensure embedded functionality still works as expected.
- Use browser compatibility resources before relying on `credentialless` in production, and provide a fallback for unsupported browsers if necessary.
- Run accessibility audits (for example, with axe DevTools or Lighthouse) to ensure the iframe has an appropriate `title` and remains usable.

---

# Pitfalls

- Using `credentialless` for widgets that require user authentication (login, payments, account dashboards).
- Assuming all browsers support the attribute equally; feature detection or graceful degradation may be needed.
- Forgetting that the iframe uses an isolated storage context, so cookies and web storage are not shared with the user's regular session.

## Question 2. What is fenced frames?

## Question 3. What is portal element?

## Question 4. What is navigation API integration?

## Question 5. What is same-origin-domain relaxation?

## Question 6. What is document.domain risk?

## Question 7. What is HTML parsing reentrancy?

## Question 8. What is synchronous section in parser?

## Question 9. What is origin trial in HTML features?

## Question 10. What is feature policy vs permission policy?

## Question 11. What is HTML fragment parsing?

## Question 12. What is template instantiation proposal?

## Question 13. What is structured cloning algorithm relation to HTML?

## Question 14. What is HTML event loop integration?

## Question 15. What is task vs microtask in HTML spec?

## Question 16. What is browsing context?

## Question 17. What is nested browsing context?

## Question 18. What is top-level browsing context?

## Question 19. What is session history entry?

## Question 20. What is navigation timing integration with HTML?
