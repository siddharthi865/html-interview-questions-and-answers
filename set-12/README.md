# Set 12

| S.No. | Question                                                                                                                                     |
| ----- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [How do you create a mailto link?](#question-1-how-do-you-create-a-mailto-link)                                                              |
| 2.    | [How do you create a phone dial link?](#question-2-how-do-you-create-a-phone-dial-link)                                                      |
| 3.    | [How do you open a link in the same tab explicitly?](#question-3-how-do-you-open-a-link-in-the-same-tab-explicitly)                          |
| 4.    | [What is the default type of a `<button>`?](#question-4-what-is-the-default-type-of-a-button)                                                |
| 5.    | [How do you prevent form submission using HTML?](#question-5-how-do-you-prevent-form-submission-using-html)                                  |
| 6.    | [What happens if the `action` attribute is empty?](#question-6-what-happens-if-the-action-attribute-is-empty)                                |
| 7.    | [How do you group radio buttons?](#question-7-how-do-you-group-radio-buttons)                                                                |
| 8.    | [What happens if radio buttons don't share the same name?](#question-8-what-happens-if-radio-buttons-dont-share-the-same-name)               |
| 9.    | [What is the difference between `checked` and `selected`?](#question-9-what-is-the-difference-between-checked-and-selected)                  |
| 10.   | [What is the purpose of the `selected` attribute?](#question-10-what-is-the-purpose-of-the-selected-attribute)                               |
| 11.   | [What blocks HTML parsing?](#question-11-what-blocks-html-parsing)                                                                           |
| 12.   | [How does CSS affect HTML rendering?](#question-12-how-does-css-affect-html-rendering)                                                       |
| 13.   | [What happens when the browser encounters a script in the head?](#question-13-what-happens-when-the-browser-encounters-a-script-in-the-head) |
| 14.   | [What is render-blocking resource?](#question-14-what-is-render-blocking-resource)                                                           |
| 15.   | [How does preconnect improve performance?](#question-15-how-does-preconnect-improve-performance)                                             |
| 16.   | [What is the difference between inline SVG and image SVG?](#question-16-what-is-the-difference-between-inline-svg-and-image-svg)             |
| 17.   | [How does lazy loading improve performance?](#question-17-how-does-lazy-loading-improve-performance)                                         |
| 18.   | [What is above-the-fold content?](#question-18-what-is-above-the-fold-content)                                                               |
| 19.   | [How do you prioritize critical assets in HTML?](#question-19-how-do-you-prioritize-critical-assets-in-html)                                 |
| 20.   | [What is resource hinting?](#question-20-what-is-resource-hinting)                                                                           |

## Question 1. How do you create a mailto link?

# Short answer

A **mailto link** is created using the `mailto:` URL scheme in the `href` attribute of an `<a>` element. Clicking it attempts to open the user's default email client with a new email draft.

```html
<a href="mailto:hello@example.com">Email us</a>
```

---

# Explanation

The `mailto:` protocol instructs the browser to launch the user's configured email application (such as Outlook, Apple Mail, Thunderbird, or a webmail client registered as the default handler).

Basic syntax:

```html
<a href="mailto:recipient@example.com">Send Email</a>
```

You can also prefill email fields using query parameters:

- `subject` – Email subject
- `body` – Email body
- `cc` – Carbon copy recipients
- `bcc` – Blind carbon copy recipients

Example:

```text
mailto:john@example.com?subject=Meeting&body=Hello%20John
```

Multiple parameters are separated with `&`.

Example:

```text
mailto:john@example.com?subject=Interview&cc=hr@example.com&body=Hello
```

Special characters and spaces must be URL-encoded:

- Space → `%20`
- New line → `%0A`
- `&` → `%26`

### Browser behavior

- The browser does **not** send the email.
- It only opens the user's configured email application.
- If no email client is configured, the link may fail or prompt the user to choose one.

---

# Example

```html
<a
  href="mailto:jobs@example.com?subject=Frontend%20Developer%20Application&body=Hello%20Team,%0A%0AI%20would%20like%20to%20apply%20for%20the%20Frontend%20Developer%20role.%0A"
>
  Apply via Email
</a>
```

> This example works without JavaScript and progressively enhances naturally.

---

# Accessibility & SEO

### Accessibility

- Use descriptive link text instead of generic text like "Click here."

```html
<a href="mailto:support@example.com">Email customer support</a>
```

- Keyboard accessible by default.
- Screen readers announce it as a link.
- No ARIA attributes are normally required.

### SEO

- Search engines generally do **not** treat `mailto:` links as navigational links.
- Publishing plain email addresses may increase spam harvesting risk.
- Consider using a contact form when appropriate.

---

# Integration & Trade-offs

### Progressive enhancement

- Works without JavaScript.
- Lightweight and supported across browsers.

### Client-side frameworks

React:

```jsx
<a href="mailto:hello@example.com">Contact</a>
```

Vue/Angular:

```html
<a :href="'mailto:' + email">Contact</a>
```

or

```html
<a [href]="'mailto:' + email">Contact</a>
```

### Server-side rendering

- Fully compatible with SSR since it is plain HTML.
- No hydration or JavaScript required.

### Trade-offs

**Advantages**

- Very simple.
- No backend required.
- Opens the user's preferred email client.

**Disadvantages**

- Depends on the user having a configured email client.
- Limited customization.
- Cannot validate submissions or handle attachments like a server-backed form can.
- Exposes email addresses to potential scraping.

---

# Testing & Validation

- Verify the generated `mailto:` URL is correctly URL-encoded.
- Test on different operating systems and browsers to ensure the expected email client opens.
- Run accessibility audits with tools like **axe DevTools** or **Lighthouse** to confirm descriptive link text and keyboard accessibility.
- Validate HTML using the WHATWG HTML checker.

---

# Pitfalls

- **Don't forget URL encoding** (`%20`, `%0A`, etc.) for subjects and bodies.
- **Avoid generic link text** like "Click here"; describe the destination or action.
- **Don't rely solely on `mailto:`** for business-critical communication, since it depends on the user's local email setup.

## Question 2. How do you create a phone dial link?

## Question 3. How do you open a link in the same tab explicitly?

## Question 4. What is the default type of a `<button>`?

## Question 5. How do you prevent form submission using HTML?

## Question 6. What happens if the `action` attribute is empty?

## Question 7. How do you group radio buttons?

## Question 8. What happens if radio buttons don’t share the same name?

## Question 9. What is the difference between `checked` and `selected`?

## Question 10. What is the purpose of the `selected` attribute?

## Question 11. What blocks HTML parsing?

## Question 12. How does CSS affect HTML rendering?

## Question 13. What happens when the browser encounters a script in the head?

## Question 14. What is render-blocking resource?

## Question 15. How does preconnect improve performance?

## Question 16. What is the difference between inline SVG and image SVG?

## Question 17. How does lazy loading improve performance?

## Question 18. What is above-the-fold content?

## Question 19. How do you prioritize critical assets in HTML?

## Question 20. What is resource hinting?
