# CLAUDE.md

Guidance for Claude Code (and any other contributor) working in this repository.

## Stack & Conventions

This project has hard constraints that override general best practices. Do not
"improve" the architecture by deviating from them, even if a more conventional
setup seems better.

1. **Single-file project.** The entire project must live in one `index.html`
   file. All CSS must be inlined in `<style>` tags and all JavaScript inlined
   in `<script>` tags inside that same file — never in separate `.css` or
   `.js` files, and never in additional `.html` pages. Linking *external*
   resources (images, CSS libraries, JS libraries) via URLs (e.g. a CDN
   `<link>` or `<script src="https://...">`) is allowed, since that doesn't
   require shipping extra local files. No multi-page apps and no additional
   local pages. This constraint exists so the finished project can be
   copy-pasted as a single file for sharing in class and on single-file code
   platforms (e.g. CodePen, JSFiddle).

2. **Vanilla only.** Use plain HTML, CSS, and JavaScript only. No frameworks
   or libraries that require a build step (no React, Vue, Svelte, Tailwind
   CLI, TypeScript compilation, bundlers, etc.), and no build/compile step of
   any kind. `index.html` must run as-is when opened directly or uploaded
   as-is. Externally linked libraries loaded via `<script src>`/`<link>` are
   fine as long as no build step is required to use them.

3. **Must run inside BrightSpace LMS.** The final result must work when
   embedded/uploaded in BrightSpace at the module/course level. Assume no
   admin access to BrightSpace — only course/module-level content permissions
   are available, so do not rely on:
   - Custom BrightSpace/Valence API integrations or org-level config changes
   - Server-side code, custom domains, or non-default CORS/CSP exceptions
   - Any BrightSpace admin/system setting that a course-level instructor or
     student cannot themselves configure

   Prefer approaches that work when `index.html` is uploaded as a course file
   or embedded in an iframe/HTML topic: avoid assumptions about top-level
   navigation, avoid features that require secure/cross-origin contexts
   BrightSpace won't grant, and keep all state/storage client-side
   (e.g. `localStorage`, in-memory JS) since there is no backend.

## Accessibility & Styling

These rules apply to all text/UI in the project and override general styling
defaults, same as the constraints above.

1. **Font.** All text must use Tahoma as the primary typeface, with a safe
   fallback stack for systems where Tahoma isn't installed (e.g.
   `font-family: Tahoma, Verdana, "Segoe UI", sans-serif;`). Apply this
   globally (e.g. on `body`), not just to isolated elements.

2. **Light and dark theme.** The page must support both a light and a dark
   theme, not just one fixed look. Default to the user's OS preference via
   `prefers-color-scheme`, and provide a manual toggle (persisted in
   `localStorage`) so a student can override it regardless of device
   settings. Implement themes with CSS custom properties (variables) swapped
   per theme rather than duplicating styles.

3. **Low-vision-friendly colors.** Students with poor/low vision must be
   able to use the page comfortably:
   - Meet WCAG AA contrast at minimum — 4.5:1 for normal text, 3:1 for large
     text and meaningful UI components/icons — in *both* themes.
   - Never use color as the only signal. Any status/state conveyed by color
     (success/warning/danger, safe/unsafe, on/off, etc.) must also be
     conveyed by text, an icon/symbol, or position — not color alone.
   - Use a colorblind-safe palette for anything categorical (avoid
     red/green as the only distinguishing pair; prefer combinations
     distinguishable under deuteranopia/protanopia/tritanopia).
   - Keep body text reasonably large (≥14px) and avoid low-contrast
     placeholder-gray-on-gray text.

4. **Minimal, clean interface.** Favor a minimal, uncluttered UI over a
   busy/decorative one: generous whitespace, a restrained color palette,
   no unnecessary chrome, borders, gradients, icons, or animation. Only show
   controls/information the student actually needs for the task at hand.
   When in doubt, cut an element rather than add one.

## Working conventions

- Before implementing any non-trivial feature, ask clarifying questions about
  scope, edge cases, and constraints first — don't propose a plan until
  you've asked.

- For the first few times a new interface/page is built in this project,
  don't jump straight to writing the final `index.html`. First present a
  few quick options — different layouts, color palettes, visual styles —
  as lightweight descriptions or sketches, and let the user pick a
  direction before implementing it for real.

- Don't default to building everything requested in one pass. When a
  request is large, ask which parts matter most, and/or implement the
  lower-priority parts as clearly-labeled placeholders (e.g. a stub
  section, a "coming soon" control, a TODO comment) instead of fully
  building them — so effort isn't wasted on scope that might still change.
  Confirm with the user before treating something as a placeholder if it's
  not obvious which parts are lower priority.
