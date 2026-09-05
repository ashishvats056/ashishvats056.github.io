# AGENTS.md

Static portfolio site (HTML/CSS/JS only). No package manager, build, test, lint, or CI. Live at https://ashishvats056.github.io/ via GitHub Pages — push to `main` to publish.

## Structure

- `index.html` — entire site: About / Resume / Contact sections (Projects nav + article are commented out, see below)
- `assets/css/style.css` — all styles (`.skill-progress-*` rules are unused leftovers; skills are grouped text lists via `.skills-category-text`)
- `assets/js/script.js` — all interactivity (vanilla JS, `"use strict"`)
- `assets/images/` — `my-photo.gif` is the live avatar; `og-cover.png` is the social/LinkedIn preview wired via `og:*` tags in `index.html` `<head>` (1200×627); `project-*` / `avatar-*` files are mostly unused leftovers from the `codewithsadee/vcard-personal-portfolio` template (placeholders still commented out in `index.html`)

## Verify

No toolchain. Open `index.html` directly in a browser (or `npx serve .`) and click through nav, filters, modal, and contact form. External CDN deps (Google Fonts Poppins, `ionicons@5.5.2` via unpkg) require network.

## Gotchas

- JS wiring is `data-*` attribute driven — keep hook names in sync between `index.html` and `script.js`:
  - nav: `data-nav-link` button text must case-insensitively match `data-page` on the `<article>` (nav loop also matches on `innerHTML`, so keep button labels plain text)
  - project filter: `data-filter-btn` / `data-select-item` text must match `data-category` on `data-filter-item` entries (`filterFunc` lowercases button text before comparing); desktop `filter-list` and mobile `filter-select-box` both drive the same `filterFunc` — update both
  - `data-selecct-value` (three c's) is a typo in both `index.html` and `script.js` — preserve it, do not "fix" one side
  - sidebar toggle: `data-sidebar` + `data-sidebar-btn`; testimonial modal: `data-testimonials-*` + `data-modal-container`/`data-overlay`/`data-modal-close-btn`; contact form: `data-form`/`data-form-input`/`data-form-btn`
- Contact form has no backend: submit builds a `mailto:ashishvats056@gmail.com` link via `window.location.href`. Submit button stays `disabled` until `form.checkValidity()` passes (`script.js:109-119`).
- Projects section is commented out (nav `<li>` + `<article data-page="projects">`, both tagged `COMMENTED OUT`); `script.js` select/filter blocks have null guards so they no-op while it is gone. To re-enable: uncomment both blocks — do not uncomment only one (orphan nav button does nothing; orphan article is unreachable).
- Resume `<article>` title is a link to the Drive resume PDF (`resume-title-link` + `open-outline` icon, tooltip "View resume doc"). Keep the anchor wrapping the header; icon must stay inside the `h2` (flex keeps it on one line).
- Personal data (email, phone, location, resume text, testimonial) is hardcoded in `index.html` — edit content there directly. Positioning is backend-focused for backend-role applications; keep it that way.
