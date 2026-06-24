# Javier Ramírez — personal site (javier-ramirez.com)

Static personal site. Hand-edited HTML, no build step. Published via GitHub Pages
(the `master` branch) and also deployed separately to an EC2 web server, so changes
here only go live on GitHub Pages; the EC2 copy needs its own deploy.

## Design policy: modern pages vs. legacy pages

Only **two** pages use the modern design:

- `index.html` — home page
- `bio.html` — bio / press kit (English + Spanish, avatars, headshots)

The modern design ("bold-sketch") is now applied directly to `index.html` and
`bio.html` (self-contained: each page carries its own embedded `<style>`/`<script>`,
no shared stylesheet). Key traits and design tokens:

- Dark theme by default, with a **light/dark toggle** (🌙/☀️ button in the nav). The
  choice is remembered in `localStorage`; it does **not** follow the OS setting — it
  always starts dark unless the user previously chose light.
- Hand-drawn **Cabin Sketch** headline (loaded from Google Fonts over **https**) with a
  **deep green → cyan** gradient: `linear-gradient(90deg,#1f9e57,#3fb6c9)`.
- Terminal/developer-green links: `#3fe07a` (dark mode), `#0f8f48` (light mode).
- Cyan sub-labels on the bio (`#3fb6c9`); collapsible sections use a `+`/`–` toggle.
- Instant, theme-styled custom tooltips that follow the cursor (not native `title`).
- Fully responsive / mobile-first: a `width=device-width` viewport, a two-column grid
  that collapses to one column at ≤820px, the sidebar un-sticks on mobile, the nav
  wraps, the headline scales with `clamp()`, and the bio photo grid reflows to one
  column. Keep these intact when editing.

Colors are CSS custom properties in `:root` (dark) and `:root[data-theme="light"]`
(light) at the top of each page's `<style>`; change palette there, not inline.

`previews/` holds throwaway prototypes (bold-sketch, retro, minimal, gradient testers,
etc.). It is **git-ignored** — do not rely on it shipping, and don't put anything
canonical there.

**Every other page is intentionally left as-is in the old Blueprint-grid look, on
purpose, for legacy and nostalgia. Do NOT modernize them.** This includes, among
others: `groovy_gandalf.html`, `curso-gratuito-solidario-ruby-on-rails.html`,
`curso-rails-bolsa-empleo.html`, `twitter.html`, `widget.html`, `original_index.html`,
and anything under `casareal/`.

### Content rules

- Never change wording unless explicitly asked. In particular the job title
  **"Head of Developer —and Agent— Relations"** is deliberate; the em dashes are an
  intentional tell of agent-assisted work and must be preserved.
- Em dashes are used **only** in that title. Everywhere else, rewrite to avoid them.
- The QuestDB domain is **questdb.com** (not questdb.io).

## The `casareal/` archive

`casareal/` is a saved snapshot (from the Wayback Machine, `web.archive.org/...`) of a
page from the Spanish Royal Household (Casa Real) website as it looked many years ago,
**before they removed the page for Iñaki Urdangarín**. Javier kept this snapshot as a
personal registry of how the page looked, in case it were ever taken down completely.
(As of this writing it is still available on the Internet Archive.) Leave it untouched.

## Machine-legible artifacts for the home and bio pages

Making content easy for AI agents to consume is literally Javier's job, so the two
modern pages get machine-legible Markdown mirrors plus an `llms.txt` index:

- `index.md` — Markdown version of the home page content
- `bio.md` — Markdown version of the bio page content
- `llms.txt` — root `llms.txt` (see https://llmstxt.org/) pointing to the two `.md` files

Whenever `index.html` or `bio.html` **content** changes, regenerate the matching `.md`
file and keep `llms.txt` in sync. The `.md` files mirror the *text content only* and are
design-agnostic, so they do not change when the page styling changes. Only `index.html`
and `bio.html` get `.md` mirrors; the legacy pages do not.
