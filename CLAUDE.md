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

## Working conventions

- Before implementing any non-trivial feature, ask clarifying questions about
  scope, edge cases, and constraints first — don't propose a plan until
  you've asked.
