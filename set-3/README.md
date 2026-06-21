# Set 3

| S.No. | Question                                                                                                                                         |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1.    | [What is the difference between `<input>` and `<textarea>`?](#question-1-what-is-the-difference-between-input-and-textarea)                      |
| 2.    | [What is the difference between `<input type="button">` and `<button>`?](#question-2-what-is-the-difference-between-input-typebutton-and-button) |
| 3.    | [What is the `name` attribute used for in forms?](#question-3-what-is-the-name-attribute-used-for-in-forms)                                      |
| 4.    | [What is form validation in HTML5?](#question-4-what-is-form-validation-in-html5)                                                                |
| 5.    | [What are `required`, `pattern`, `min`, `max` attributes?](#question-5-what-are-required-pattern-min-max-attributes)                             |
| 6.    | [What is the difference between `readonly` and `disabled`?](#question-6-what-is-the-difference-between-readonly-and-disabled)                    |
| 7.    | [What is the purpose of the `<label>` tag?](#question-7-what-is-the-purpose-of-the-label-tag)                                                    |
| 8.    | [How do you associate a label with an input?](#question-8-how-do-you-associate-a-label-with-an-input)                                            |
| 9.    | [What is the `<fieldset>` tag?](#question-9-what-is-the-fieldset-tag)                                                                            |
| 10.   | [What is the `<legend>` tag?](#question-10-what-is-the-legend-tag)                                                                               |
| 11.   | [How do you create a table in HTML?](#question-11-how-do-you-create-a-table-in-html)                                                             |
| 12.   | [What is the difference between `<th>` and `<td>`?](#question-12-what-is-the-difference-between-th-and-td)                                       |
| 13.   | [What is the purpose of `<thead>`, `<tbody>`, `<tfoot>`?](#question-13-what-is-the-purpose-of-thead-tbody-tfoot)                                 |
| 14.   | [What is `colspan`?](#question-14-what-is-colspan)                                                                                               |
| 15.   | [What is `rowspan`?](#question-15-what-is-rowspan)                                                                                               |
| 16.   | [How do you create accessible tables?](#question-16-how-do-you-create-accessible-tables)                                                         |
| 17.   | [What is the `scope` attribute in `<th>`?](#question-17-what-is-the-scope-attribute-in-th)                                                       |
| 18.   | [What is semantic HTML?](#question-18-what-is-semantic-html)                                                                                     |
| 19.   | [What are semantic elements introduced in HTML5?](#question-19-what-are-semantic-elements-introduced-in-html5)                                   |
| 20.   | [What is the difference between `<div>` and `<section>`?](#question-20-what-is-the-difference-between-div-and-section)                           |

## Question 1. What is the difference between `<input>` and `<textarea>`?

# Short answer

`<input>` is used for **single-line user input** (text, email, password, number, etc.), while `<textarea>` is used for **multi-line text input** such as comments, messages, descriptions, or notes.

---

# Explanation

Although both elements collect user input and participate in form submission, they serve different purposes:

| Feature           | `<input>`                            | `<textarea>`                        |
| ----------------- | ------------------------------------ | ----------------------------------- |
| Purpose           | Single-line input                    | Multi-line input                    |
| Closing tag       | Void element (no closing tag)        | Requires opening and closing tags   |
| Default content   | `value` attribute                    | Text between tags                   |
| Line breaks       | Not supported                        | Supported                           |
| Typical use cases | Name, email, phone, search, password | Comments, messages, article content |
| Resizable by user | No                                   | Usually yes (browser-dependent)     |

### Semantics

Choose the element based on the expected content:

- Use `<input>` when users should enter a short value.
- Use `<textarea>` when users may need paragraphs, multiple lines, or formatted text.

This improves form usability and communicates intent to browsers, assistive technologies, and developers.

### HTML, CSS, and JavaScript interaction

Both elements:

- Can be associated with a `<label>`.
- Participate in form submission.
- Support validation (`required`, `maxlength`, etc.).
- Can be accessed through JavaScript using `.value`.

Differences:

- `<textarea>` preserves line breaks entered by users.
- `<input>` supports specialized types (`email`, `url`, `number`, `date`, etc.) that provide built-in validation and optimized mobile keyboards.

Example:

```html
<input type="email" />
```

provides email validation and an email-friendly keyboard on mobile, whereas a textarea cannot provide this specialized behavior.

### Performance and Progressive Enhancement

For standard forms, both elements work without JavaScript and are excellent examples of progressive enhancement.

Avoid replacing native controls with custom JavaScript widgets unless there is a strong requirement, because native controls provide:

- Better accessibility
- Better mobile support
- Lower maintenance
- Built-in validation

---

# Example

```html
<form>
  <div>
    <label for="name">Name</label>
    <input id="name" name="name" type="text" required />
  </div>

  <div>
    <label for="message">Message</label>
    <textarea id="message" name="message" rows="5" required> </textarea>
  </div>

  <button type="submit">Send</button>
</form>
```

---

# Accessibility & SEO

### Accessibility

- Always associate inputs with a `<label>`.
- Use `required`, `aria-describedby`, and validation messages where appropriate.
- Ensure sufficient touch target size on mobile.
- Preserve keyboard navigation and focus states.

Example:

```html
<label for="feedback">Feedback</label>
<textarea id="feedback" aria-describedby="feedback-help"></textarea>

<p id="feedback-help">Maximum 500 characters.</p>
```

### SEO

Form controls themselves have minimal direct SEO impact, but:

- Proper labels improve usability and accessibility.
- Better user experience can indirectly improve engagement metrics.
- Use semantic forms and meaningful field names.

---

# Integration & Trade-offs

### CSS

`<textarea>` often requires more styling consideration:

```css
textarea {
  resize: vertical;
}
```

This allows users to expand the field vertically while preventing layout issues.

### React / Vue / Angular

- `<input>` is commonly used with controlled or uncontrolled components.
- `<textarea>` behaves similarly, but frameworks typically bind its content through a value property rather than child text.

React example:

```jsx
<textarea value={message} onChange={handleChange} />
```

instead of:

```jsx
<textarea>Text</textarea>
```

### SSR and Progressive Enhancement

Server-rendered forms work naturally with both elements.

In SPAs, keep native form behavior where possible and enhance it with JavaScript rather than replacing it entirely.

---

# Testing & Validation

### HTML Validation

Validate markup using:

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/?utm_source=chatgpt.com)
- [W3C Nu Validator](https://validator.w3.org/nu/?utm_source=chatgpt.com)

### Accessibility Testing

Use:

- [axe DevTools](https://www.deque.com/axe/?utm_source=chatgpt.com)
- [Lighthouse](https://developer.chrome.com/docs/lighthouse/?utm_source=chatgpt.com)

Verify:

- Labels are announced correctly.
- Keyboard navigation works.
- Validation messages are accessible.
- Screen readers properly identify multiline fields.

---

# Pitfalls

- Using `<input type="text">` for long-form content that should be entered in a `<textarea>`.
- Forgetting to associate controls with `<label>` elements.
- Not specifying appropriate input types (`email`, `tel`, `url`, etc.), losing built-in validation and mobile optimizations.

## Question 2. What is the difference between `<input type="button">` and `<button>`?

## Question 3. What is the `name` attribute used for in forms?

## Question 4. What is form validation in HTML5?

## Question 5. What are `required`, `pattern`, `min`, `max` attributes?

## Question 6. What is the difference between `readonly` and `disabled`?

## Question 7. What is the purpose of the `<label>` tag?

## Question 8. How do you associate a label with an input?

## Question 9. What is the `<fieldset>` tag?

## Question 10. What is the `<legend>` tag?

## Question 11. How do you create a table in HTML?

## Question 12. What is the difference between `<th>` and `<td>`?

## Question 13. What is the purpose of `<thead>`, `<tbody>`, `<tfoot>`?

## Question 14. What is `colspan`?

## Question 15. What is `rowspan`?

## Question 16. How do you create accessible tables?

## Question 17. What is the `scope` attribute in `<th>`?

## Question 18. What is semantic HTML?

## Question 19. What are semantic elements introduced in HTML5?

## Question 20. What is the difference between `<div>` and `<section>`?
