# Set 8

| S.No. | Question                                                                                                                                                    |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is `enctype="multipart/form-data"`?](#question-1-what-is-enctypemultipartform-data)                                                                   |
| 2.    | [What is the difference between client-side and server-side validation?](#question-2-what-is-the-difference-between-client-side-and-server-side-validation) |
| 3.    | [What is the `minlength` and `maxlength` attribute?](#question-3-what-is-the-minlength-and-maxlength-attribute)                                             |
| 4.    | [What is input masking?](#question-4-what-is-input-masking)                                                                                                 |
| 5.    | [What is the `inputmode` attribute?](#question-5-what-is-the-inputmode-attribute)                                                                           |
| 6.    | [What is the `<details>` tag?](#question-6-what-is-the-details-tag)                                                                                         |
| 7.    | [What is the `<summary>` tag?](#question-7-what-is-the-summary-tag)                                                                                         |
| 8.    | [What is the `<dialog>` element?](#question-8-what-is-the-dialog-element)                                                                                   |
| 9.    | [What is the `hidden` attribute?](#question-9-what-is-the-hidden-attribute)                                                                                 |
| 10.   | [What is the `contenteditable` attribute?](#question-10-what-is-the-contenteditable-attribute)                                                              |
| 11.   | [What is the difference between `<iframe>` and `<embed>`?](#question-11-what-is-the-difference-between-iframe-and-embed)                                    |
| 12.   | [What is the purpose of the `sandbox` attribute in iframes?](#question-12-what-is-the-purpose-of-the-sandbox-attribute-in-iframes)                          |
| 13.   | [What is the `srcdoc` attribute in iframe?](#question-13-what-is-the-srcdoc-attribute-in-iframe)                                                            |
| 14.   | [What are global attributes in HTML?](#question-14-what-are-global-attributes-in-html)                                                                      |
| 15.   | [What is the `translate` attribute?](#question-15-what-is-the-translate-attribute)                                                                          |
| 16.   | [What is the `spellcheck` attribute?](#question-16-what-is-the-spellcheck-attribute)                                                                        |
| 17.   | [What is the `draggable` attribute?](#question-17-what-is-the-draggable-attribute)                                                                          |
| 18.   | [What is the `tabindex` attribute?](#question-18-what-is-the-tabindex-attribute)                                                                            |
| 19.   | [What is the difference between `aria-hidden` and `hidden`?](#question-19-what-is-the-difference-between-aria-hidden-and-hidden)                            |
| 20.   | [What is the `role` attribute?](#question-20-what-is-the-role-attribute)                                                                                    |

## Question 1. What is `enctype="multipart/form-data"`?

# Short answer

`enctype="multipart/form-data"` is a form encoding type used with the `<form>` element to send form data as separate parts in an HTTP request. It is **required when a form includes file uploads** (`<input type="file">`) because it allows binary data (such as images, PDFs, or videos) to be transmitted correctly.

---

# Explanation

The `enctype` (encoding type) attribute specifies **how the browser encodes form data before sending it to the server**. It only applies when `method="post"`.

```html
<form method="post" enctype="multipart/form-data"></form>
```

There are three common encoding types:

| `enctype`                                     | Use case                                        |
| --------------------------------------------- | ----------------------------------------------- |
| `application/x-www-form-urlencoded` (default) | Regular text fields                             |
| `multipart/form-data`                         | Forms containing file uploads                   |
| `text/plain`                                  | Mainly for debugging; rarely used in production |

### Why `multipart/form-data`?

With the default encoding, all form values are URL-encoded into a single string:

```text
name=John&age=25
```

This works well for text but **cannot efficiently represent binary file contents**.

With `multipart/form-data`, each field is sent as an individual "part" separated by a boundary:

```text
------boundary
Content-Disposition: form-data; name="username"

john
------boundary
Content-Disposition: form-data; name="photo"; filename="me.jpg"
Content-Type: image/jpeg

(binary data)
------boundary--
```

This allows the server to process both text fields and uploaded files independently.

### When is it required?

Use it whenever your form contains:

```html
<input type="file" />
```

Without it:

- Files are **not uploaded correctly**
- The server may receive only the filename or no file at all
- Upload APIs/frameworks may reject the request

---

# Example

```html
<form action="/upload" method="post" enctype="multipart/form-data">
  <label for="photo">Choose a photo</label>
  <input id="photo" name="photo" type="file" accept="image/*" required />

  <button type="submit">Upload</button>
</form>
```

> **Note:** This form requires server-side handling to process the uploaded file. The browser only packages and sends the request.

---

# Accessibility & SEO

### Accessibility

- Always associate `<label>` elements with file inputs.
- Use the `accept` attribute only as a user convenience—it does **not** enforce file type validation.
- Provide clear instructions about allowed file formats and size limits.
- If upload errors occur, expose them accessibly (e.g., associate error text with the input using `aria-describedby` and announce dynamic updates when appropriate).

### SEO

- `enctype` has **no direct SEO impact**.
- Ensure forms remain crawl-friendly if they are part of user workflows, but search engines generally do not index uploaded content via forms.

---

# Integration & Trade-offs

### CSS

- `enctype` has no effect on styling.
- File inputs are difficult to style consistently across browsers; many applications visually customize them while keeping the native control accessible.

### JavaScript

Using the `FormData` API automatically creates a `multipart/form-data` request.

```javascript
const formData = new FormData(form);
fetch("/upload", {
  method: "POST",
  body: formData,
});
```

**Do not manually set the `Content-Type` header** when sending `FormData`. The browser automatically sets the correct `multipart/form-data` value along with the required boundary.

### Client-side frameworks

- **React:** Use `FormData` with controlled or uncontrolled file inputs. File inputs cannot be fully controlled like text inputs.
- **Vue/Angular:** Similar pattern—collect files from the input and submit them via `FormData`.

### Server-side rendering

SSR does not change how uploads work. The browser still submits a multipart request, and the server must parse it using middleware or framework-specific upload handlers.

### Progressive enhancement

A standard HTML form with `multipart/form-data` works without JavaScript. JavaScript can enhance the experience by adding drag-and-drop, upload progress indicators, previews, or asynchronous uploads without replacing the underlying form behavior.

---

# Testing & Validation

- Validate HTML using the WHATWG/W3C HTML validator.
- Test uploads with browser developer tools by inspecting the **Network** request to confirm:
  - Request method is `POST`
  - `Content-Type` is `multipart/form-data`
  - The file appears in the request payload

- Verify accessibility with tools such as axe DevTools and Lighthouse.
- Test:
  - Valid and invalid file types
  - Maximum file size
  - Multiple file uploads (if supported)
  - Server-side validation and error handling

---

# Pitfalls

- **Forgetting `enctype="multipart/form-data"`** when using `<input type="file">`, causing uploads to fail.
- **Manually setting the `Content-Type` header** when sending `FormData`; let the browser include the required boundary.
- **Relying only on client-side validation** (`accept` attribute). Always validate file type, size, and content on the server.

## Question 2. What is the difference between client-side and server-side validation?

## Question 3. What is the `minlength` and `maxlength` attribute?

## Question 4. What is input masking?

## Question 5. What is the `inputmode` attribute?

## Question 6. What is the `<details>` tag?

## Question 7. What is the `<summary>` tag?

## Question 8. What is the `<dialog>` element?

## Question 9. What is the `hidden` attribute?

## Question 10. What is the `contenteditable` attribute?

## Question 11. What is the difference between `<iframe>` and `<embed>`?

## Question 12. What is the purpose of the `sandbox` attribute in iframes?

## Question 13. What is the `srcdoc` attribute in iframe?

## Question 14. What are global attributes in HTML?

## Question 15. What is the `translate` attribute?

## Question 16. What is the `spellcheck` attribute?

## Question 17. What is the `draggable` attribute?

## Question 18. What is the `tabindex` attribute?

## Question 19. What is the difference between `aria-hidden` and `hidden`?

## Question 20. What is the `role` attribute?
