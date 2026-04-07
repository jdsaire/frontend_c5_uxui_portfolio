# Alex Styles — Graphic Designer Portfolio

A responsive, interactive portfolio website built for the **Microsoft Front End Developer** course (UI/UX Design Principles). This project is completed in three activities, each building on the last.

**Live site:** [https://jdsaire.github.io/portfolio](https://jdsaire.github.io/portfolio)

---

## Project Structure

```
├── index.html    — Full HTML structure (nav, about, portfolio, contact)
├── styles.css    — All CSS across Activities 1–3
├── script.js     — JavaScript for modals, mobile nav, form feedback
└── README.md     — Project summary
```

---

## How Claude Code Assisted Development

This project was built using **Claude Code** as the AI development assistant (replacing Microsoft Copilot) at every stage.

### Activity 1 — Writing and Enhancing CSS

Claude Code generated the complete foundational CSS for Alex Styles' portfolio site:

- **Typography system** — Defined font pairings (Inter + Playfair Display via Google Fonts), fluid `clamp()`-based font sizes that scale across viewport widths, and consistent line-height for readability.
- **Color palette** — Established a cohesive brand palette (deep navy `#1a1a2e`, accent red `#e94560`, off-white `#f8f7f4`) with semantic CSS custom properties, making the entire scheme easy to update.
- **Layout architecture** — Applied CSS Grid for the 3-column portfolio section and Flexbox for the navigation bar and about section, creating a clean, structured foundation.
- **Hover transitions** — Generated smooth `transition` rules on nav links (accent underline reveal), portfolio cards (lift + shadow), and buttons (color shift + vertical translate).
- **Fade-in animations** — Created a `@keyframes fadeInUp` animation applied to each portfolio card with staggered `animation-delay` values for a polished reveal effect on page load.
- **Performance optimization** — Organized CSS in logical sections (reset → custom properties → base → layout → components) and eliminated redundant rules.

### Activity 2 — Responsive Design

Claude Code produced all media queries and responsive layout adaptations:

- **Mobile (max-width: 768px)** — Stacked single-column layout, collapsible hamburger navigation (with smooth `max-height` animation), single-column portfolio grid, full-width contact form, and centered about section.
- **Tablet (max-width: 1024px)** — 2-column portfolio grid, reduced avatar size, and consolidated contact layout.
- **Desktop (min-width: 1025px)** — Full 3-column portfolio grid, side-by-side about layout, and dual-column contact section.
- **Fluid typography** — All font sizes use `clamp()` so they scale naturally between breakpoints without needing extra media query overrides.
- **Flexible form layout** — Contact form adapts from stacked (mobile) to a structured grid layout (desktop) for comfortable data entry on any device.

### Activity 3 — UI/UX Enhancements

Claude Code implemented interactive elements and refined the visual design:

- **Portfolio modal** — Clicking any project card opens a full-screen overlay modal with a blurred backdrop, slide-in animation, project title, and description. Supports close via button, overlay click, or `ESC` key. Fully keyboard-accessible with correct `aria-modal` and `aria-hidden` attributes.
- **Navigation tooltips** — Each nav link uses a `data-tooltip` attribute; CSS `::after` pseudo-elements render styled tooltip bubbles on hover/focus, improving usability without any extra JavaScript.
- **Mobile nav toggle** — JavaScript-powered hamburger menu with `aria-expanded` state management and auto-close on link click.
- **Visual hierarchy refinements** — Added decorative accent underlines to section headings, improved color contrast for body text, and added a focus ring system using `:focus-visible` for accessibility.
- **Button interaction polish** — Buttons lift with `transform: translateY(-2px)` and cast a colored box-shadow on hover, reinforcing interactivity.
- **Form submit feedback** — The contact form provides inline success feedback ("Message Sent!") with automatic reset after 3 seconds, giving users clear confirmation without a page reload.

---

## Features

- Fully responsive (mobile, tablet, desktop)
- Accessible (semantic HTML, ARIA attributes, keyboard navigation, focus management)
- CSS-only tooltips on nav links
- Modal with blur backdrop and slide-in animation for portfolio projects
- Smooth scroll navigation
- CSS `@keyframes` fade-in animation on portfolio cards
- Contact form with HTML5 validation and submit feedback
- No JavaScript frameworks — vanilla HTML, CSS, and JS only

---

## Inspection Findings

Code review conducted against all three source files after Activities 1–3 were completed.

### `index.html`

- **Semantic structure** — `<header>`, `<nav>`, `<section>`, `<article>`, and `<footer>` are used correctly throughout. Portfolio items as `<article>` elements is semantically appropriate.
- **Missing `<main>` landmark** — The three content sections (`#about`, `#portfolio`, `#contact`) sit directly inside `<body>` without a `<main>` wrapper. This reduces navigability for assistive technology users who rely on landmark navigation.
- **Modal missing `aria-labelledby`** — The `role="dialog"` element has `aria-modal="true"` but does not reference `modal-title` via `aria-labelledby`. Screen readers will not automatically announce the modal title when it opens.
- **No `<meta name="description">`** — The `<head>` contains `charset` and `viewport` meta tags but no description, so search engines will display a generic excerpt.
- **Keyboard access on cards** — `tabindex="0"` is correctly set on all `.portfolio-card` elements; script handles both `Enter` and `Space` to activate them.

### `styles.css`

- **Duplicate `.portfolio-card` rule** — The selector is declared twice (foundational block at §1.9 and animation block at §1.12). Both blocks are valid and non-conflicting, but they could be merged into one rule.
- **Broad `--transition: all 0.25s ease`** — Using `all` as the transition property can cause unintended transitions on future properties (e.g., `height`, `color`, `display`). Targeting specific properties (`color`, `transform`, `box-shadow`, `border-color`) would be more precise.
- **No `prefers-reduced-motion` media query** — The `fadeInUp` animation runs unconditionally. Users who have set "Reduce Motion" in their OS preferences will still see the animation, which is a WCAG 2.1 SC 2.3.3 (Animation from Interactions) consideration.
- **`will-change` absent** — The README activity summary mentions `will-change` as a performance optimization, but it does not appear in the stylesheet. The README claim is slightly inaccurate; the property was not needed and was correctly omitted.
- **Vendor prefix** — `-webkit-backdrop-filter` is correctly paired with `backdrop-filter` in both the header and modal overlay.

### `script.js`

- **Focus not restored after modal close** — When `closeModal()` is called, focus is not returned to the card that triggered the modal. WCAG 2.4.3 (Focus Order) requires that focus be returned to a logical position after a dialog closes.
- **No per-field validation messaging** — `form.checkValidity()` correctly blocks submission on invalid input, but individual error messages are not surfaced programmatically. Native browser tooltips appear on submit, but these vary by browser and are not announced by all screen readers.
- **No `aria-live` region for form feedback** — The "Message Sent!" confirmation is injected into the button's `textContent`. Without an `aria-live="polite"` region, screen reader users may not hear the confirmation message.
- **Null-checks in place** — The `navToggle` / `navList` guard (`if (navToggle && navList)`) and the `form` guard correctly prevent errors if elements are absent.
- **Scope hygiene** — The IIFE wrapper and `'use strict'` directive ensure no variables leak to the global scope.

### Summary

| File | Issues Found | Severity |
|------|-------------|----------|
| `index.html` | Missing `<main>`, missing `aria-labelledby` on modal, no meta description | Low–Medium |
| `styles.css` | No `prefers-reduced-motion` rule, broad `--transition`, duplicate selector | Low |
| `script.js` | Focus not restored after modal close, no `aria-live` for form feedback | Medium |

All three issues flagged as **Medium** severity are accessibility gaps relative to WCAG 2.1 AA. No blocking bugs or security issues were found. The codebase is clean, well-organized, and fully meets the course requirements for Activities 1–3.

---

## GitHub Pages

Deployed via GitHub Pages from the `main` branch.
Settings → Pages → Source: `main` / `/ (root)`
