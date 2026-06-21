# Set 19

| S.No. | Question                                                                                                                                    |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is language negotiation in browsers?](#question-1-what-is-language-negotiation-in-browsers)                                           |
| 2.    | [How does `lang` attribute improve accessibility?](#question-2-how-does-lang-attribute-improve-accessibility)                               |
| 3.    | [What is hreflang?](#question-3-what-is-hreflang)                                                                                           |
| 4.    | [What is bidirectional isolation?](#question-4-what-is-bidirectional-isolation)                                                             |
| 5.    | [What is the purpose of `<bdi>`?](#question-5-what-is-the-purpose-of-bdi)                                                                   |
| 6.    | [What is text direction inheritance?](#question-6-what-is-text-direction-inheritance)                                                       |
| 7.    | [What is Unicode bidi algorithm?](#question-7-what-is-unicode-bidi-algorithm)                                                               |
| 8.    | [How does HTML support RTL layouts?](#question-8-how-does-html-support-rtl-layouts)                                                         |
| 9.    | [What is the difference between logical and physical direction?](#question-9-what-is-the-difference-between-logical-and-physical-direction) |
| 10.   | [What is locale-sensitive content in HTML?](#question-10-what-is-locale-sensitive-content-in-html)                                          |
| 11.   | [What is the preload scanner?](#question-11-what-is-the-preload-scanner)                                                                    |
| 12.   | [What is speculative parsing?](#question-12-what-is-speculative-parsing)                                                                    |
| 13.   | [What is DOMContentLoaded event?](#question-13-what-is-domcontentloaded-event)                                                              |
| 14.   | [What is the load event?](#question-14-what-is-the-load-event)                                                                              |
| 15.   | [What is document.readyState?](#question-15-what-is-documentreadystate)                                                                     |
| 16.   | [What is mutation of DOM during parsing?](#question-16-what-is-mutation-of-dom-during-parsing)                                              |
| 17.   | [What is parser-inserted script?](#question-17-what-is-parser-inserted-script)                                                              |
| 18.   | [What is dynamically inserted script?](#question-18-what-is-dynamically-inserted-script)                                                    |
| 19.   | [How does document.write() affect parsing?](#question-19-how-does-documentwrite-affect-parsing)                                             |
| 20.   | [Why is document.write discouraged?](#question-20-why-is-documentwrite-discouraged)                                                         |

## Question 1. What is language negotiation in browsers?

# Language Negotiation in Browsers

## Short answer

**Language negotiation** is the process by which a browser and a server determine the most appropriate language to serve to a user. The browser communicates the user's language preferences through the **`Accept-Language` HTTP request header**, and the server selects the best matching localized version of the content (if available).

---

## Explanation

Language negotiation is part of **HTTP content negotiation**. When a user visits a website, the browser automatically sends language preferences configured in the operating system or browser settings.

Example request header:

```http
Accept-Language: en-US,en;q=0.9,fr;q=0.7,hi;q=0.6
```

Meaning:

- `en-US` → highest preference
- `en` → fallback English
- `fr` → French with quality (`q`) value of `0.7`
- `hi` → Hindi with quality value of `0.6`

The `q` value (quality factor) ranges from **0 to 1**, where higher values indicate higher preference.

### How negotiation works

1. Browser sends `Accept-Language`.
2. Server compares it against supported languages.
3. Server chooses the closest match.
4. Server returns localized content.
5. Server may include:

```http
Content-Language: en-US
```

and often

```http
Vary: Accept-Language
```

so caches store different language versions correctly.

### Example

Browser:

```http
Accept-Language: fr-CA,fr;q=0.9,en;q=0.8
```

Server supports:

- English
- French

Server responds with the French version because it is the closest available match.

---

## Example

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Welcome</title>
  </head>
  <body>
    <h1>Welcome</h1>
  </body>
</html>
```

Server-side (conceptually):

```text
if Accept-Language contains "fr"
    serve index-fr.html
else
    serve index-en.html
```

Always set the document language using the `lang` attribute:

```html
<html lang="fr"></html>
```

This tells browsers, screen readers, spell checkers, and search engines the language of the document.

---

## Accessibility & SEO

### Accessibility

- Always specify the page language:

```html
<html lang="en"></html>
```

- For multilingual content:

```html
<p lang="es">Hola Mundo</p>
```

- Screen readers use `lang` to:
  - Switch pronunciation rules
  - Select the correct speech synthesizer or voice
  - Improve reading accuracy

- The `Accept-Language` header **does not** replace the HTML `lang` attribute. The header is used during the HTTP request, while `lang` describes the language of the delivered document.

### SEO

- Use the correct `lang` attribute on each page.
- For multilingual sites, use the `hreflang` attribute in alternate links to help search engines understand language and regional variants.
- Give each language its own URL (for example, `/en/`, `/fr/`, `/de/`) rather than relying solely on browser negotiation, so pages can be indexed and shared reliably.
- Do not automatically redirect users solely based on `Accept-Language`; always allow manual language switching because browser settings may not reflect a user's actual preference.

---

## Integration & Trade-offs

### Server-side rendering (SSR)

SSR frameworks (e.g., Next.js, Nuxt, ASP.NET, Django) commonly inspect `Accept-Language` during the initial request to render localized HTML, improving first-page load and SEO.

### Single Page Applications (SPA)

SPAs often:

- Read the browser language using JavaScript:

```javascript
navigator.language;
```

or

```javascript
navigator.languages;
```

- Load translation files dynamically after the application starts.

This approach is flexible but may delay localized content unless combined with SSR or pre-rendering.

### Progressive enhancement

A robust strategy is:

1. Detect the preferred language on the server.
2. Serve localized HTML.
3. Let users change the language manually.
4. Persist their choice (e.g., cookie or profile setting), overriding `Accept-Language` on future visits.

### Performance

- Cache localized pages separately using:

```http
Vary: Accept-Language
```

- Avoid creating excessive cache variants if only a few languages are supported.

---

## Testing & Validation

- Change your browser's preferred languages and verify that the server returns the expected localized page.
- Use browser DevTools or command-line tools to inspect the `Accept-Language`, `Content-Language`, and `Vary` headers.
- Validate HTML to ensure the correct `lang` attribute is present.
- Use accessibility tools such as axe DevTools and Lighthouse to detect missing or incorrect document language declarations.
- Test screen readers to verify pronunciation changes for multilingual content.

---

## Pitfalls

- **Using `Accept-Language` as the only source of truth.** Always allow users to manually choose and persist their preferred language.
- **Forgetting the `lang` attribute.** Screen readers, spell checkers, and search engines rely on it regardless of HTTP negotiation.
- **Omitting `Vary: Accept-Language`.** Shared caches may serve the wrong language if language-specific responses aren't varied correctly.

## Question 2. How does `lang` attribute improve accessibility?

## Question 3. What is hreflang?

## Question 4. What is bidirectional isolation?

## Question 5. What is the purpose of `<bdi>`?

## Question 6. What is text direction inheritance?

## Question 7. What is Unicode bidi algorithm?

## Question 8. How does HTML support RTL layouts?

## Question 9. What is the difference between logical and physical direction?

## Question 10. What is locale-sensitive content in HTML?

## Question 11. What is the preload scanner?

## Question 12. What is speculative parsing?

## Question 13. What is DOMContentLoaded event?

## Question 14. What is the load event?

## Question 15. What is document.readyState?

## Question 16. What is mutation of DOM during parsing?

## Question 17. What is parser-inserted script?

## Question 18. What is dynamically inserted script?

## Question 19. How does document.write() affect parsing?

## Question 20. Why is document.write discouraged?
