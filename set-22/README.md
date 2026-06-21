# Set 22

| S.No. | Question                                                                                                                       |
| ----- | ------------------------------------------------------------------------------------------------------------------------------ |
| 1.    | [What is constraint validation candidate?](#question-1-what-is-constraint-validation-candidate)                                |
| 2.    | [What is labelable element?](#question-2-what-is-labelable-element)                                                            |
| 3.    | [What is listed form-associated element?](#question-3-what-is-listed-form-associated-element)                                  |
| 4.    | [What is submittable element?](#question-4-what-is-submittable-element)                                                        |
| 5.    | [What is resettable element?](#question-5-what-is-resettable-element)                                                          |
| 6.    | [What is layout containment in HTML?](#question-6-what-is-layout-containment-in-html)                                          |
| 7.    | [What is paint containment?](#question-7-what-is-paint-containment)                                                            |
| 8.    | [What is size containment?](#question-8-what-is-size-containment)                                                              |
| 9.    | [What is content-visibility?](#question-9-what-is-content-visibility)                                                          |
| 10.   | [How does HTML affect Largest Contentful Paint (LCP)?](#question-10-how-does-html-affect-largest-contentful-paint-lcp)         |
| 11.   | [What HTML patterns improve First Contentful Paint (FCP)?](#question-11-what-html-patterns-improve-first-contentful-paint-fcp) |
| 12.   | [What is render tree vs DOM tree?](#question-12-what-is-render-tree-vs-dom-tree)                                               |
| 13.   | [What is accessibility tree?](#question-13-what-is-accessibility-tree)                                                         |
| 14.   | [What is flat tree vs composed tree?](#question-14-what-is-flat-tree-vs-composed-tree)                                         |
| 15.   | [How does Shadow DOM affect accessibility tree?](#question-15-how-does-shadow-dom-affect-accessibility-tree)                   |
| 16.   | [What is slotting algorithm?](#question-16-what-is-slotting-algorithm)                                                         |
| 17.   | [What is event retargeting in Shadow DOM?](#question-17-what-is-event-retargeting-in-shadow-dom)                               |
| 18.   | [What is declarative custom elements definition?](#question-18-what-is-declarative-custom-elements-definition)                 |
| 19.   | [What is HTML module script type?](#question-19-what-is-html-module-script-type)                                               |
| 20.   | [What is blocking="render" attribute?](#question-20-what-is-blockingrender-attribute)                                          |

## Question 1. What is constraint validation candidate?

# Short answer

A **constraint validation candidate** is a form control that the browser considers eligible for HTML's built-in **Constraint Validation API**. Only validation candidates participate in native validation (`required`, `pattern`, `min`, `max`, etc.). Controls that are **barred from constraint validation** are ignored during validation.

---

# Explanation

The HTML specification defines whether a form-associated element is a **candidate for constraint validation** (`willValidate` is `true`) or not (`willValidate` is `false`).

A control is typically a validation candidate if it:

- Is associated with a form.
- Supports constraint validation.
- Is not disabled.
- Is not barred from constraint validation.

Examples of controls that are **not validation candidates** include:

- `<input type="hidden">`
- Disabled controls (`disabled`)
- `<button>` elements
- `<output>`
- Elements inside a disabled `<fieldset>` (with some exceptions)
- Controls that the specification explicitly bars from constraint validation

JavaScript exposes this through the `willValidate` property:

```javascript
const input = document.querySelector("input");
console.log(input.willValidate); // true or false
```

If `willValidate` is `false`, methods like `checkValidity()` will not report validation errors for that control because the browser skips it.

---

# Example

```html
<form>
  <label>
    Name
    <input type="text" required />
  </label>

  <input type="hidden" required />

  <label>
    Disabled Email
    <input type="email" required disabled />
  </label>

  <button type="submit">Submit</button>
</form>

<script>
  const controls = document.querySelectorAll("input");

  controls.forEach((control) => {
    console.log(control.type, "willValidate:", control.willValidate);
  });
</script>
```

**Expected output:**

```
text willValidate: true
hidden willValidate: false
email willValidate: false
```

The text input participates in validation, while the hidden and disabled inputs do not.

---

# Accessibility & SEO

### Accessibility

- Native constraint validation provides built-in error handling and integrates with assistive technologies better than custom validation alone.
- Pair inputs with `<label>` elements and provide clear validation messages.
- When using custom validation (`setCustomValidity()`), ensure errors are announced (e.g., via `aria-live`) and that invalid fields expose `aria-invalid="true"` if you override native behavior.
- Do not disable native validation (`novalidate`) unless you replace it with an accessible alternative.

### SEO

- Constraint validation has **no direct SEO impact**.
- It improves form completion and user experience, which can indirectly improve engagement metrics.

---

# Integration & Trade-offs

- **CSS:** Use the `:valid`, `:invalid`, `:required`, and `:optional` pseudo-classes for styling validation states without JavaScript.
- **JavaScript:** Use `checkValidity()`, `reportValidity()`, `setCustomValidity()`, and `willValidate` to integrate native validation with custom logic.
- **Frameworks (React/Vue/Angular):**
  - Many applications implement validation in JavaScript, but native HTML validation remains useful as a baseline.
  - Native validation can reduce duplicated logic and provides progressive enhancement.

- **SSR vs SPA:**
  - Server-side validation is always required because client-side validation can be bypassed.
  - Native constraint validation improves UX but should complement—not replace—server-side validation.

---

# Testing & Validation

- Verify `element.willValidate` for controls that should or should not participate in validation.
- Test with `checkValidity()` and `reportValidity()`.
- Validate markup with the HTML validator and run accessibility audits using tools such as axe DevTools and Lighthouse.
- Test keyboard-only interactions and screen reader announcements for validation errors.

---

# Pitfalls

- Assuming every form control is validated—elements like `type="hidden"` and disabled controls are not validation candidates.
- Relying solely on client-side validation instead of validating on the server.
- Disabling native validation (`novalidate`) without implementing an accessible replacement.

## Question 2. What is labelable element?

## Question 3. What is listed form-associated element?

## Question 4. What is submittable element?

## Question 5. What is resettable element?

## Question 6. What is layout containment in HTML?

## Question 7. What is paint containment?

## Question 8. What is size containment?

## Question 9. What is content-visibility?

## Question 10. How does HTML affect Largest Contentful Paint (LCP)?

## Question 11. What HTML patterns improve First Contentful Paint (FCP)?

## Question 12. What is render tree vs DOM tree?

## Question 13. What is accessibility tree?

## Question 14. What is flat tree vs composed tree?

## Question 15. How does Shadow DOM affect accessibility tree?

## Question 16. What is slotting algorithm?

## Question 17. What is event retargeting in Shadow DOM?

## Question 18. What is declarative custom elements definition?

## Question 19. What is HTML module script type?

## Question 20. What is blocking="render" attribute?
