# Set 24

| S.No. | Question                                                                                                                     |
| ----- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1.    | [What is aria-current?](#question-1-what-is-aria-current)                                                                    |
| 2.    | [What is aria-expanded lifecycle?](#question-2-what-is-aria-expanded-lifecycle)                                              |
| 3.    | [What is aria-controls relationship?](#question-3-what-is-aria-controls-relationship)                                        |
| 4.    | [What is accessible error identification?](#question-4-what-is-accessible-error-identification)                              |
| 5.    | [What is form error announcement?](#question-5-what-is-form-error-announcement)                                              |
| 6.    | [What is color contrast compliance in HTML context?](#question-6-what-is-color-contrast-compliance-in-html-context)          |
| 7.    | [What is semantic heading hierarchy rule?](#question-7-what-is-semantic-heading-hierarchy-rule)                              |
| 8.    | [Why should there be only one `<main>` landmark?](#question-8-why-should-there-be-only-one-main-landmark)                    |
| 9.    | [What is landmark duplication issue?](#question-9-what-is-landmark-duplication-issue)                                        |
| 10.   | [What is accessible table summary alternative in HTML5?](#question-10-what-is-accessible-table-summary-alternative-in-html5) |
| 11.   | [What is accessible icon button pattern?](#question-11-what-is-accessible-icon-button-pattern)                               |
| 12.   | [What is visually hidden technique?](#question-12-what-is-visually-hidden-technique)                                         |
| 13.   | [What is focus trap implementation conceptually?](#question-13-what-is-focus-trap-implementation-conceptually)               |
| 14.   | [What is skip-to-content best practice?](#question-14-what-is-skip-to-content-best-practice)                                 |
| 15.   | [What is ARIA overuse problem?](#question-15-what-is-aria-overuse-problem)                                                   |
| 16.   | [What is DOM-based clobbering attack?](#question-16-what-is-dom-based-clobbering-attack)                                     |
| 17.   | [What is prototype pollution via HTML injection?](#question-17-what-is-prototype-pollution-via-html-injection)               |
| 18.   | [What is sandbox escape scenario?](#question-18-what-is-sandbox-escape-scenario)                                             |
| 19.   | [What is cross-origin isolation?](#question-19-what-is-cross-origin-isolation)                                               |
| 20.   | [What is COOP and COEP?](#question-20-what-is-coop-and-coep)                                                                 |

## Question 1. What is aria-current?

# Short answer

`aria-current` is an **ARIA state** that tells assistive technologies which item in a group represents the **current** item. It is commonly used in navigation menus, breadcrumbs, pagination, calendars, and step indicators so screen reader users know where they are.

Unlike `aria-selected`, which indicates the currently selected item in a widget (such as a tab or listbox), `aria-current` indicates the item that represents the user's **current location or context**.

---

# Explanation

The `aria-current` attribute is applied to **one element within a related set**. Screen readers announce that element as the current one, helping users understand their position.

Common values include:

| Value             | Use case                                                    |
| ----------------- | ----------------------------------------------------------- |
| `page`            | Current page in site navigation or pagination (most common) |
| `step`            | Current step in a multi-step form or wizard                 |
| `location`        | Current location on a map or route                          |
| `date`            | Today's date in a calendar                                  |
| `time`            | Current time in a timetable                                 |
| `true`            | Current item when no specific type applies                  |
| `false` (default) | Item is not current                                         |

For example:

- Navigation menu → current page
- Breadcrumb → current page
- Pagination → current page number
- Checkout wizard → current step
- Calendar → today's date

Only **one item in a related group** should usually have `aria-current`.

---

# Example

```html
<nav aria-label="Main navigation">
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/blog" aria-current="page">Blog</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>
```

A screen reader may announce:

> "Blog, current page, link."

Another example for a checkout wizard:

```html
<ol>
  <li>Cart</li>
  <li aria-current="step">Shipping</li>
  <li>Payment</li>
  <li>Confirmation</li>
</ol>
```

---

# Accessibility & SEO

### Accessibility

- Use `aria-current` to communicate the user's **current location**, not selection.
- Only one item in a related set should typically be marked as current.
- Common landmarks:
  - `<nav>` for navigation
  - `<ol>` for breadcrumbs and step indicators

- No keyboard behavior is added by `aria-current`; it is purely semantic.
- Prefer semantic HTML first, then enhance it with `aria-current` where appropriate.

### SEO

- `aria-current` has **no direct SEO impact**.
- Semantic structures (`<nav>`, `<ol>`, proper heading hierarchy) improve document structure, which can indirectly benefit search engines and accessibility.

---

# Integration & Trade-offs

### CSS

You can style the current item using an attribute selector:

```css
a[aria-current="page"] {
  font-weight: bold;
  text-decoration: underline;
}
```

This keeps styling synchronized with accessibility semantics.

### JavaScript

When navigation changes dynamically, update `aria-current` so only the active item has it.

### React/Vue/Angular

Most routing libraries handle this automatically:

- React Router's `NavLink` can set `aria-current="page"` for the active route.
- Similar functionality exists in Vue Router and Angular Router.

### SSR vs SPA

- **Server-side rendering (SSR):** Render the correct `aria-current` on the server based on the requested URL.
- **Single-page applications (SPAs):** Update `aria-current` whenever client-side routing changes.

### Progressive Enhancement

Even if JavaScript is disabled, server-rendered navigation with `aria-current` remains accessible.

---

# Testing & Validation

- Verify that only one item in a navigation or breadcrumb has `aria-current`.
- Test with screen readers such as NVDA, VoiceOver, or JAWS to confirm the current item is announced.
- Run accessibility audits using:
  - axe DevTools
  - Lighthouse

- Validate HTML to ensure the surrounding semantic structure is correct.

---

# Pitfalls

- **Don't use `aria-current` instead of `aria-selected`.** They represent different concepts.
- **Don't mark multiple items as current** within the same navigation or step sequence unless the UI genuinely has multiple current items.
- **Don't rely solely on visual styling.** Keep `aria-current` synchronized with the visible active state.

## Question 2. What is aria-expanded lifecycle?

## Question 3. What is aria-controls relationship?

## Question 4. What is accessible error identification?

## Question 5. What is form error announcement?

## Question 6. What is color contrast compliance in HTML context?

## Question 7. What is semantic heading hierarchy rule?

## Question 8. Why should there be only one `<main>` landmark?

## Question 9. What is landmark duplication issue?

## Question 10. What is accessible table summary alternative in HTML5?

## Question 11. What is accessible icon button pattern?

## Question 12. What is visually hidden technique?

## Question 13. What is focus trap implementation conceptually?

## Question 14. What is skip-to-content best practice?

## Question 15. What is ARIA overuse problem?

## Question 16. What is DOM-based clobbering attack?

## Question 17. What is prototype pollution via HTML injection?

## Question 18. What is sandbox escape scenario?

## Question 19. What is cross-origin isolation?

## Question 20. What is COOP and COEP?
