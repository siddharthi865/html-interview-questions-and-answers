# Set 13

| S.No. | Question                                                                                                                                |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is constraint validation API?](#question-1-what-is-constraint-validation-api)                                                     |
| 2.    | [How do you display custom validation messages?](#question-2-how-do-you-display-custom-validation-messages)                             |
| 3.    | [What is progressive form enhancement?](#question-3-what-is-progressive-form-enhancement)                                               |
| 4.    | [How can HTML improve mobile UX?](#question-4-how-can-html-improve-mobile-ux)                                                           |
| 5.    | [What is the difference between `tel` and `number` input types?](#question-5-what-is-the-difference-between-tel-and-number-input-types) |
| 6.    | [How do you make a form accessible?](#question-6-how-do-you-make-a-form-accessible)                                                     |
| 7.    | [What is autofocus?](#question-7-what-is-autofocus)                                                                                     |
| 8.    | [What are default form behaviors?](#question-8-what-are-default-form-behaviors)                                                         |
| 9.    | [What is form submission encoding?](#question-9-what-is-form-submission-encoding)                                                       |
| 10.   | [How do you create a search input field properly?](#question-10-how-do-you-create-a-search-input-field-properly)                        |
| 11.   | [What is the difference between iframe and frame?](#question-11-what-is-the-difference-between-iframe-and-frame)                        |
| 12.   | [Why are frames deprecated?](#question-12-why-are-frames-deprecated)                                                                    |
| 13.   | [What is the purpose of allow attribute in iframe?](#question-13-what-is-the-purpose-of-allow-attribute-in-iframe)                      |
| 14.   | [What is fullscreen API integration in HTML?](#question-14-what-is-fullscreen-api-integration-in-html)                                  |
| 15.   | [What is picture-in-picture support?](#question-15-what-is-picture-in-picture-support)                                                  |
| 16.   | [How does media query support in `<link>` tag?](#question-16-what-is-media-query-support-in-link-tag)                                   |
| 17.   | [How does `<base>` tag work?](#question-17-how-does-base-tag-work)                                                                      |
| 18.   | [What happens if multiple `<base>` tags exist?](#question-18-what-happens-if-multiple-base-tags-exist)                                  |
| 19.   | [What is crossorigin behavior in images?](#question-19-what-is-crossorigin-behavior-in-images)                                          |
| 20.   | [What is referrerpolicy attribute?](#question-20-what-is-referrerpolicy-attribute)                                                      |

## Question 1. What is constraint validation API?

# Constraint Validation API

## Short answer

The **Constraint Validation API** is a built-in browser API that allows developers to **check, customize, and report HTML form validation** using JavaScript. It works with HTML validation attributes like `required`, `min`, `max`, `pattern`, `minlength`, `maxlength`, `type`, and `step`, enabling both native validation and custom validation messages without requiring external libraries.

---

## Explanation

The Constraint Validation API extends HTML forms with JavaScript methods and properties for validating form controls.

Instead of writing validation logic from scratch, browsers automatically validate fields based on HTML attributes. JavaScript can then inspect validation state, trigger validation, or define custom validation rules.

### Common validation attributes

```html
required min max minlength maxlength pattern type="email" type="url" step
```

### Important methods

| Method                       | Purpose                                                                                        |
| ---------------------------- | ---------------------------------------------------------------------------------------------- |
| `checkValidity()`            | Returns `true` if the element is valid; otherwise `false`. Does **not** display validation UI. |
| `reportValidity()`           | Validates and displays the browser's error message if invalid.                                 |
| `setCustomValidity(message)` | Sets a custom validation message. An empty string clears the custom error.                     |

### Important properties

| Property            | Description                                                          |
| ------------------- | -------------------------------------------------------------------- |
| `validity`          | Returns a `ValidityState` object describing why validation failed.   |
| `validationMessage` | Returns the browser's current validation message.                    |
| `willValidate`      | Indicates whether the element participates in constraint validation. |

### `ValidityState` flags

Some useful properties include:

- `valueMissing`
- `typeMismatch`
- `patternMismatch`
- `tooShort`
- `tooLong`
- `rangeOverflow`
- `rangeUnderflow`
- `stepMismatch`
- `badInput`
- `customError`
- `valid`

---

## Example

```html
<form id="signup">
  <label for="username">Username</label>
  <input id="username" type="text" required minlength="4" />

  <button type="submit">Submit</button>
</form>

<script>
  const form = document.getElementById("signup");
  const username = document.getElementById("username");

  form.addEventListener("submit", (e) => {
    username.setCustomValidity("");

    if (username.value === "admin") {
      username.setCustomValidity('Username "admin" is not allowed.');
    }

    if (!form.reportValidity()) {
      e.preventDefault();
    }
  });
</script>
```

Here:

- Native validation checks `required` and `minlength`.
- `setCustomValidity()` adds a business-specific rule.
- `reportValidity()` displays the browser's validation UI.

> **Note:** Custom validation messages require JavaScript. Without JavaScript, the browser still enforces native HTML constraints such as `required` and `minlength`.

---

## Accessibility & SEO

### Accessibility

- Native HTML validation is generally accessible because browsers expose validation errors to assistive technologies.
- Associate inputs with `<label>` elements.
- Use `aria-invalid="true"` only when a field is actually invalid if you are managing validation yourself.
- If displaying custom error text, associate it with the input using `aria-describedby`.
- Avoid relying solely on color to indicate errors.
- Ensure keyboard users can easily reach and correct invalid fields.

### SEO

- Constraint validation has **no direct SEO impact**.
- It improves data quality and user experience, reducing invalid form submissions.
- Server-side validation is still required because client-side validation can be bypassed.

---

## Integration & Trade-offs

### HTML + JavaScript

- Best paired with semantic HTML validation attributes.
- Reduces the amount of custom JavaScript required.

### CSS

Use CSS pseudo-classes:

```css
input:valid {
  border-color: green;
}

input:invalid {
  border-color: red;
}
```

### React / Vue / Angular

- Frameworks often use controlled components and custom validation logic.
- The Constraint Validation API still works and can simplify validation for simple forms.
- Many teams disable native browser validation (`novalidate`) and implement custom UI while still using `checkValidity()` or `validity` internally.

### Server-side rendering & Progressive Enhancement

- Native HTML validation works immediately after the page loads, even before JavaScript hydrates.
- Always perform **server-side validation** as the authoritative check.
- Progressive enhancement approach:
  1. Use HTML validation attributes.
  2. Enhance with the Constraint Validation API for custom rules and messages.
  3. Revalidate on the server.

---

## Testing & Validation

- Verify native validation in multiple browsers.
- Test keyboard-only interactions.
- Use browser DevTools to inspect `validity` and `validationMessage`.
- Run accessibility audits with tools like **axe DevTools** and **Lighthouse**.
- Validate HTML markup to ensure constraint attributes are used correctly.
- Test server-side validation independently to ensure invalid requests cannot bypass client-side checks.

---

## Pitfalls

- **Don't rely only on client-side validation.** Users can disable JavaScript or craft requests manually.
- **Remember to clear custom errors** using `setCustomValidity('')`; otherwise, the field remains invalid.
- **Avoid replacing native validation unnecessarily.** Native validation provides accessibility and localization benefits with minimal code.

## Question 2. How do you display custom validation messages?

## Question 3. What is progressive form enhancement?

## Question 4. How can HTML improve mobile UX?

## Question 5. What is the difference between `tel` and `number` input types?

## Question 6. How do you make a form accessible?

## Question 7. What is autofocus?

## Question 8. What are default form behaviors?

## Question 9. What is form submission encoding?

## Question 10. How do you create a search input field properly?

## Question 11. What is the difference between iframe and frame?

## Question 12. Why are frames deprecated?

## Question 13. What is the purpose of allow attribute in iframe?

## Question 14. What is fullscreen API integration in HTML?

## Question 15. What is picture-in-picture support?

## Question 16. What is media query support in `<link>` tag?

## Question 17. How does `<base>` tag work?

## Question 18. What happens if multiple `<base>` tags exist?

## Question 19. What is crossorigin behavior in images?

## Question 20. What is referrerpolicy attribute?
