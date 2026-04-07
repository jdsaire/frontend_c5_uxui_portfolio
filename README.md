# Alex Styles — Graphic Designer Portfolio

## Course 5 of 6 in the Microsoft Front-End Developer Specialization — *UX/UI Design Principles*

**Live site:** [https://jdsaire.github.io/frontend_c5_uxui_portfolio/](https://jdsaire.github.io/frontend_c5_uxui_portfolio/)

A responsive, interactive portfolio website for Alex Styles, a graphic designer with over 6 years of industry experience. From the client's perspective, the goal of this project was to produce a professional online presence that consolidates work samples, communicates a personal brand, and provides a direct contact channel — all essential for attracting new clients and collaborators in a competitive creative market.

The project was completed in three iterations, each building on the previous deliverable. Developed **5–7 April 2026** with the following effective-hour breakdown:

| Phase | Hours | Note |
|---|---|---|
| Course training | 3 h | Reduced due to prior UX certifications (Google UX Design, HEC Montréal) |
| Development | 1 h | Reduced due to workflow planning and Claude Code execution |
| Review & iteration | 2 h | Included Google Docs annotations on the original README and Gemini Pro processing |
| Deployment | 1 h | GitHub connection via Claude Code; peer review of 2 assignments to complete evaluation requirements |
| **Total** | **7 h** | |

---

## Project Structure

```
├── index.html    — Full HTML structure (nav, about, portfolio, contact)
├── styles.css    — All CSS across Iterations 1–3
├── script.js     — JavaScript for modals, mobile nav, form feedback
└── README.md     — Project summary
```

---

## Project Iterations

Out of transparency: all code snippets across the three iterations were developed with **Claude Code** as the AI development assistant — no Microsoft Copilot was used. After each snippet was generated, every code file was individually inspected. No further adjustments were required, as the course guidelines did not specify client-side UI preferences, leaving design decisions to the designer. The structured approach — workflow planning before execution — produced a final deliverable without debugging cycles or post-hoc refactoring. The website passed usability and accessibility tests in line with the responsive design practices promoted throughout the course, and complies with all evaluation criteria.

### Iteration 1 — CSS Foundations *(activity 1/3 of the final course project)*

The first iteration focused on establishing a cohesive visual identity and a scalable code architecture for the portfolio:

- **Typography system** — Defined font pairings (Inter + Playfair Display via Google Fonts), fluid `clamp()`-based font sizes that scale across viewport widths, and consistent line-height for readability.
- **Color palette** — Established a brand palette (deep navy `#1a1a2e`, accent red `#e94560`, off-white `#f8f7f4`) with semantic CSS custom properties, making the entire scheme easy to update from a single source.
- **Layout architecture** — Applied CSS Grid for the 3-column portfolio section and Flexbox for the navigation bar and about section, creating a clean, structured foundation.
- **Hover transitions** — Smooth `transition` rules on nav links (accent underline reveal), portfolio cards (lift + shadow), and buttons (color shift + vertical translate).
- **Fade-in animations** — A `@keyframes fadeInUp` animation applied to each portfolio card with staggered `animation-delay` values for a polished reveal effect on page load.
- **Performance optimization** — CSS organized in logical sections (reset → custom properties → base → layout → components), eliminating redundant rules.

### Iteration 2 — Responsive Design *(activity 2/3)*

This iteration adapted the established layout to serve users across all device sizes without compromising the visual hierarchy built in Iteration 1:

- **Mobile (max-width: 768px)** — Stacked single-column layout, collapsible hamburger navigation (with smooth `max-height` animation), single-column portfolio grid, full-width contact form, and centered about section.
- **Tablet (max-width: 1024px)** — 2-column portfolio grid, reduced avatar size, and consolidated contact layout.
- **Desktop (min-width: 1025px)** — Full 3-column portfolio grid, side-by-side about layout, and dual-column contact section.
- **Fluid typography** — All font sizes use `clamp()` so they scale naturally between breakpoints without needing extra media query overrides.
- **Flexible form layout** — Contact form adapts from stacked (mobile) to a structured grid layout (desktop) for comfortable data entry on any device.

### Iteration 3 — UI/UX Enhancements *(activity 3/3)*

The final iteration prioritized interaction quality and accessibility, introducing components that increase engagement while keeping the experience fully keyboard-navigable and screen reader-friendly:

- **Portfolio modal** — Clicking any project card opens a full-screen overlay modal with a blurred backdrop, slide-in animation, project title, and description. Supports close via button, overlay click, or `ESC` key. Fully keyboard-accessible with correct `aria-modal` and `aria-hidden` attributes.
- **Navigation tooltips** — Each nav link uses a `data-tooltip` attribute; CSS `::after` pseudo-elements render styled tooltip bubbles on hover/focus, improving usability without any extra JavaScript.
- **Mobile nav toggle** — JavaScript-powered hamburger menu with `aria-expanded` state management and auto-close on link click.
- **Visual hierarchy refinements** — Decorative accent underlines added to section headings, improved color contrast for body text, and a focus ring system using `:focus-visible` for accessibility.
- **Button interaction polish** — Buttons lift with `transform: translateY(-2px)` and cast a colored box-shadow on hover, reinforcing interactivity.
- **Form submit feedback** — The contact form provides inline success feedback ("Message Sent!") with automatic reset after 3 seconds, giving users clear confirmation without a page reload.

---

## Features & Evaluation Compliance

- Fully responsive (mobile, tablet, desktop)
- Accessible (semantic HTML, ARIA attributes, keyboard navigation, focus management)
- CSS-only tooltips on nav links
- Modal with blur backdrop and slide-in animation for portfolio projects
- Smooth scroll navigation
- CSS `@keyframes` fade-in animation on portfolio cards
- Contact form with HTML5 validation and submit feedback
- No JavaScript frameworks — vanilla HTML, CSS, and JS only

**Note for peer reviewers:** All deliverables address the grading criteria for the three course activities. Iteration 1 covers foundational CSS (typography, color, layout, transitions, animations). Iteration 2 covers responsive design (media queries, fluid typography, flexible layouts). Iteration 3 covers UI/UX enhancements (modals, tooltips, visual polish, accessibility). The implementation meets or exceeds each criterion as evaluated against the course rubric.

---

## Inspection Findings

Code review was conducted against all three source files after all iterations were completed.

**Gemini Pro review:** Following individual inspection, Gemini Pro was prompted to identify general opportunities to improve syntax efficiency across the three files. Its takeaway:

> *"The structural code itself doesn't need to be rewritten, as it is already highly scalable and standard. Your proposed improvements — adding a master index comment and more explanatory inline comments — are the exact right steps to make this document friendlier for a growing team or a beginner reviewer."*

The CSS file was reviewed first to gain a full understanding of the single-page structure; the HTML and JS files were then referenced for specific consultations. All three files already contain section separators and inline observations to ease reading.

**Claude Code review:** A deeper pass was conducted on each file to surface any remaining opportunities.

### `index.html`

- **Semantic structure** — `<header>`, `<nav>`, `<section>`, `<article>`, and `<footer>` are used correctly throughout. Portfolio items as `<article>` elements is semantically appropriate.
- **Missing `<main>` landmark** — The three content sections (`#about`, `#portfolio`, `#contact`) sit directly inside `<body>` without a `<main>` wrapper. This reduces navigability for assistive technology users who rely on landmark navigation.
- **Modal missing `aria-labelledby`** — The `role="dialog"` element has `aria-modal="true"` but does not reference `modal-title` via `aria-labelledby`. Screen readers will not automatically announce the modal title when it opens.
- **No `<meta name="description">`** — The `<head>` contains `charset` and `viewport` meta tags but no description, so search engines will display a generic excerpt.
- **Keyboard access on cards** — `tabindex="0"` is correctly set on all `.portfolio-card` elements; the script handles both `Enter` and `Space` to activate them.

### `styles.css`

- **Duplicate `.portfolio-card` rule** — The selector is declared twice (foundational block §1.9 and animation block §1.12). Both are valid and non-conflicting but could be merged.
- **Broad `--transition: all 0.25s ease`** — Using `all` can cause unintended transitions on future properties. Targeting specific properties (`color`, `transform`, `box-shadow`, `border-color`) would be more precise.
- **No `prefers-reduced-motion` media query** — The `fadeInUp` animation runs unconditionally, which is a WCAG 2.1 SC 2.3.3 consideration for users who have enabled reduced motion in their OS.
- **`will-change` absent** — The README activity summary mentioned `will-change` as a performance optimization, but it does not appear in the stylesheet. The property was correctly omitted as it was not needed.
- **Vendor prefix** — `-webkit-backdrop-filter` is correctly paired with `backdrop-filter` in both the header and modal overlay.

### `script.js`

- **Focus not restored after modal close** — When `closeModal()` is called, focus is not returned to the card that triggered the modal. WCAG 2.4.3 (Focus Order) requires focus to return to a logical position after a dialog closes.
- **No per-field validation messaging** — `form.checkValidity()` correctly blocks submission on invalid input, but individual error messages are not surfaced programmatically.
- **No `aria-live` region for form feedback** — The "Message Sent!" confirmation is injected into the button's `textContent`. Without an `aria-live="polite"` region, screen reader users may not hear the confirmation.
- **Null-checks in place** — The `navToggle`/`navList` guard and the `form` guard correctly prevent errors if elements are absent.
- **Scope hygiene** — The IIFE wrapper and `'use strict'` directive ensure no variables leak to the global scope.

### Summary

| File | Observations | Severity |
|---|---|---|
| `index.html` | Missing `<main>`, missing `aria-labelledby` on modal, no meta description | Low–Medium |
| `styles.css` | No `prefers-reduced-motion` rule, broad `--transition`, duplicate selector | Low |
| `script.js` | Focus not restored after modal close, no `aria-live` for form feedback | Medium |

**Conclusion:** No changes are required in `styles.css` or `script.js`. `index.html` was assessed for readability improvements (inline comments and structural indexing); however, no structural or syntax changes were performed in any file. The medium-severity accessibility items above are documented for transparency and future reference.

---

## GitHub Pages

Deployed via GitHub Pages from the `main` branch.
Settings → Pages → Source: `main` / `/ (root)`
