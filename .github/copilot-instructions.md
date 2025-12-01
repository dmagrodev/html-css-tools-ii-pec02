# Copilot / AI assistant instructions for this repo

This project is the UOC Boilerplate scaffold used in HTML/CSS courses. The guidance below is targeted and actionable so an AI agent can be productive immediately.

- **Run / Build**: Use the NPM scripts in `package.json`.
  - Development server: `npm run dev` (alias for `start` in this fork).
  - Production build: `npm run build`.
  - Clean caches: `npm run clean`.
  - Parcel serves on port `8123` by default (`parcel -p 8123`).

- **Important constraints**:
  - Only edit files under `src/` unless the change explicitly requires config updates (e.g., `package.json`, Parcel config).
  - Do NOT remove the two asset lines in `src/index.html`:
    - `<link rel="stylesheet" ... href="./assets/styles/main.scss"> <!-- do not remove this line! -->`
    - `<script type="module" src="./assets/scripts/main.js"></script> <!-- do not remove this line! -->`

- **Project architecture (big picture)**:
  - Entrypoint: `src/index.html` (Parcel target `web` uses `src/index.html`).
  - CSS pipeline: `src/assets/styles/main.scss` imports SCSS partials organized by layers and folders:
    - Utilities: `01_utilities/*` (variables, mixins).
    - Base: `02_base/_reset.scss`.
    - Vendors: `03_vendors/_bootstrap-custom.scss`.
    - Layouts: `04_layout/*` (one partial per page or layout piece).
    - Components: `05_components/*` (prefix `c-` for components, e.g. `_c-navbar.scss`).
    - Pages: `06_pages/*` (page-specific styles, e.g. `_p-home.scss`).
    - States: `07_states/*` (utility state styles).
  - JS pipeline: `src/assets/scripts/main.js` is a module (`type="module"`). Node dependencies (e.g., `bootstrap`) are imported via ES modules and bundled by Parcel.
  - HTML partials: `src/views/*.html` are included into pages using PostHTML `include` tags like `<include src="./views/header.html"></include>`.

- **Conventions & patterns to follow**:
  - SCSS: Keep `main.scss` as an imports-only file. Add SCSS code into the appropriate partials under `assets/styles/`.
  - Naming: Partial file prefixes indicate purpose (`_c-` components, `_p-` pages, `_` common partials).
  - HTML structure uses layout classes like `l-grid__main`, `l-grid__visual-area` and block/component prefixes like `Poster__title`. Follow existing class patterns.

- **Examples (how to implement a small change)**:
  - Add a new component `c-alert`:
    1. Create `src/assets/styles/05_components/_c-alert.scss` and import it in `main.scss` with the `components` layer.
    2. Add markup in the appropriate HTML file (e.g., `src/views/header.html` or a page partial).
    3. Run `npm run dev` to verify styling and live reload.

- **Tests & checks**:
  - There are no test suites defined. Use `npm run build` to validate the production build finishes without Parcel errors.
  - On Windows, `sharp` (an image dependency) may require native binaries; if build errors mention `sharp`, ensure build environment has necessary tools (or run `npm rebuild sharp`).

- **Where to look for answers in this repo**:
  - General project info and scripts: `package.json` and `README.md` at repo root.
  - HTML entry & includes: `src/index.html`, `src/views/*.html`.
  - Styles organization: `src/assets/styles/main.scss` and subfolders `01_utilities` .. `07_states`.
  - Scripts: `src/assets/scripts/main.js`.

- **When making PRs / commits**:
  - Keep changes minimal and scoped (e.g., single component or page per PR).
  - If changing build/config (`package.json`, parcel targets), document why and how to reproduce locally (`npm install`, `npm run dev`).

If anything here is unclear or you want more examples (e.g., a sample component or updated build scripts), tell me what you'd like and I'll iterate.
