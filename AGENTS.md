# Notes for coding agents

Hugo source for [sfnexus.org](https://sfnexus.org), the SF Nexus project at Temple University Libraries (science fiction collections as data). Netlify builds `main` to production; every PR gets a deploy preview.

## Start here

- `TODO.md`: open items. Most need a human with account access, such as Google Search Console, Netlify, or confirming facts.
- `PHASES.md`: the 2026 staged rollout. Phases 1–3 are merged (PR #28). The retro redesign is parked on `phase-4-redesign` and `phase-5-polish`, with steps to resume it.
- `README.md`: build commands and how to edit content, data files, and shortcodes.

## Build

- Hugo **0.168.0 extended**, pinned in `netlify.toml`. `themes/gohugo-theme-ananke` is ananke v2.19.1, vendored unmodified; put changes in `layouts/` or `sfnexus.css`, never in the theme, so it can be replaced wholesale on the next bump.
- `hugo --gc --minify` for a production build. The build should report 0 warnings.
- Pages are `index, follow` only when `hugo.IsProduction` is true, which is any plain `hugo` build, local ones included. netlify.toml builds deploy previews and branch deploys with `--environment preview`, so they are `noindex` on purpose, as is `hugo server`.

## Where things live (on `main`)

- `content/<Section>/_index.md`: page text. A page joins a lifecycle stage with `stage: source|curate|analyze|publish` in its front matter.
- `data/lifecycle.yaml` drives the stage rail and prev/next pager. `data/datasets.yaml` drives the dataset cards and the schema.org Dataset JSON-LD. `data/timeline.yaml` drives the About timeline.
- `layouts/`: overrides on top of Ananke.
  - render hooks in `_default/_markup/`: images become responsive WebP figures, external links get ↗ and a new tab, headings get anchors
  - shortcodes: `notebook`, `notice`, `datasets`, `timeline`
  - partials: `stage-rail`, `stage-pager`, `sfnexus-schema`, `responsive-image`
  - `home.html`: ananke's home layout without its centering and narrow measure
- `assets/ananke/css/sfnexus.css`: extra styles. Ananke concatenates it after its own CSS (`params.ananke.custom_css`), uncompiled.
- `static/images/` is also mounted as `assets/images`, so the image hook can resize originals. Reference images as `/images/...`.
- `static/ldaviz/`: standalone pyLDAvis page. `/models/lda_clifi_1` redirects to it (see netlify.toml).

## Gotchas

- The main menu lives only in `config.toml`. Don't add `menu:` to front matter; that caused duplicate-menu warnings.
- Don't add `params.github`, `twitter`, and similar keys to config: Ananke turns them into social icons in the header and footer.
- Put each shortcode on its own line with blank lines around it, including back-to-back `notebook` shortcodes. Otherwise they are wrapped in `<p>`, which produces invalid HTML.
- The phase 4/5 branches use their own templates and `assets/css/sfnexus.css`. They do not use the Ananke CSS file. To keep them current, merge `main` into `phase-4-redesign`, then `phase-4-redesign` into `phase-5-polish`.

## Checks used before merging

- A clean build, then an axe-core accessibility audit of every page at 1280px and 390px. `main` had 0 violations as of PR #28.
- A horizontal-overflow check from 320 to 1280px.
- Cloud sandboxes may block most external hosts. Verify links from a normal network, or by cloning the SF-Nexus GitHub repos.
