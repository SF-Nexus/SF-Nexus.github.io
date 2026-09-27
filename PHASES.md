# SF Nexus site: phased rollout

The 2026 review of sfnexus.org is split into five stacked branches. Each branch builds on the one before, so they can be reviewed and merged into `main` **in order**, and you can stop after any phase. The complete end state is also kept whole on the `full-redesign` branch for reference.

| Phase | Branch | What a visitor notices |
|---|---|---|
| 1 | `phase-1-invisible` | Nothing. Behind-the-scenes fixes only |
| 2 | `phase-2-basics` | Same look; cleaner, corrected, better-organized content |
| 3 | `phase-3-features` | Same look; new components (figures, contents box, notebook buttons, dataset cards, timeline) |
| 4 | `phase-4-redesign` | New retro science-fiction paperback design |
| 5 | `phase-5-polish` | Dark mode, retro 404, print styles, accessibility pass, final touches |

To merge a phase: open a PR from `phase-N-…` into `main`, check the Netlify deploy preview, and merge. After phase N is merged, the phase N+1 PR shows only that phase's changes.

---

## Phase 1: Invisible fixes (`phase-1-invisible`)

Nothing a reader would notice. Every page was pixel-compared against `main` at desktop and phone widths. The homepage, People, and Scholarship pages are identical; the others differ only where a typo was corrected (under 0.6% of pixels).

- **Search engines can index the site.** The ananke theme only emits `index, follow` (and an `Allow` robots.txt) when `HUGO_ENV=production`. That was never set, so every page has been shipping as `noindex, nofollow`. netlify.toml now sets it for production deploys only; deploy previews stay `noindex`.
- **Explicit Netlify build:** `hugo --gc --minify`, `publish = "public"`. Deploy previews build with their own URL, and basic security headers are added.
- **No more duplicate-menu build warnings.** The menu was defined in `config.toml` and again in each page's front matter. It now lives only in `config.toml`, in the same order.
- **Empty pages removed:** `/tags/`, `/categories/`, and a leftover `/authors/admin/` page from an old theme. Nothing linked to them.
- **Broken link targets repointed, link text unchanged:**
  - three notebook links pointed at Jupyter files that no longer exist (they now go to the Colab versions)
  - two repo links used old names that only work through GitHub redirects
  - the "extracted features" link on OCR pointed at a repo, not the data
  - the Hugging Face docs link went to v1.1.1
  - HathiTrust's policy page and the Data Capsule docs had moved
- **Alt text** on all 21 content images, for screen readers.
- **Typos and names:** package/packaged, occurrence, co-occurrences, built, FineReader, HathiTrust, "An R Script," Institute of *Museum* and Library Services, Alliance of Digital Humanities Organizations, Texas A&M University, and "Hugging Face page" (was "Github page").
- **Canonical URL** tag on every page.
- **Roadmap and to-do:** the `redesign` branch's TODO.md is merged in, and this file is added.

## Phase 2: Basic improvements (`phase-2-basics`)

Same Ananke look; the content gets better.

- Merge the `data-lifecycle` branch: nav in lifecycle order (About → OCR → Data → Models → Analysis → Scholarship → People), stage banners, and the homepage "data lifecycle" overview.
- Replace the homepage hero image (the "creepy" one, per TODO) with the Paskow paperback photo.
- Make HathiTrust prominent on the homepage.
- De-duplicate the homepage and About (they shared whole paragraphs), and keep one copy of the HathiTrust ingestion section, on the OCR page.
- Clearer page names: Models → *Topic Models*, Analysis → *Word Embeddings*. URLs unchanged.
- Correct heading levels, list and quote formatting, and People-page formatting. Remove the link to a WordPress profile *picture*.
- **Data:**
  - fix the `load_dataset` example (it wrongly said data is "split into training and testing groups")
  - add "how to cite"
  - add a notice that HTRC Data Capsules end on Sept 30, 2026
- **Topic Models:**
  - restore the missing LDA figure (the text referred to it, but it never appeared)
  - add the Air Pollution topic
  - add "Open in Colab" links
- **Word Embeddings:** proper citations for the NovelTM and Thompson & Mimno comparison corpora, and links to the repo's Word2Vec notebooks.
- **OCR:** numbered cleanup steps, and an accurate description of the web-scraping repo.
- Replace the stray, untitled "Recent Models" card on the homepage and Models page with a proper link to the interactive LDAvis explorer, now hosted at sfnexus.org/ldaviz/.
- Favicon.
- Fix the Data page overflowing sideways on phones.

## Phase 3: Feature enhancements (`phase-3-features`)

Same look; new building blocks, styled to sit quietly inside Ananke.

- Images served as responsive WebP. Click to see full size. Captions come from image titles.
- External links are marked ↗ and open in a new tab.
- Heading anchors and an "On this page" contents box.
- The lifecycle stage banner and previous/next navigation are generated from `data/lifecycle.yaml`, replacing the hand-typed banners.
- Shortcodes:
  - `{{< notebook >}}`: GitHub and Open-in-Colab buttons
  - `{{< notice >}}`: callout boxes
  - `{{< datasets >}}`: dataset cards from `data/datasets.yaml`
  - `{{< timeline >}}`: project history from `data/timeline.yaml`
- schema.org Dataset markup, so Google Dataset Search can list the five datasets.
- Expanded context:
  - **About:** collections-as-data framing, related SCRC ArchivesSpace collections, Data Speculations grant details, and the timeline
  - **Scholarship:** annotated sections on collections as data, TDM law and policy, computational SF and cli-fi scholarship, reference works, and SF special collections

## Phase 4: Major redesign (`phase-4-redesign`)

The retro science-fiction paperback theme:

- pulp-paper backgrounds and deep-space navy bands with a starfield
- Microgramma-style display type (Michroma), with Space Grotesk and Space Mono for the interface, all self-hosted
- duotone halftone art and hard offset "misregistered print" shadows
- the homepage: paperback hero, "by the numbers" band, four lifecycle stage cards, dataset strip, and feature cards
- a chevron lifecycle rail, catalog-card datasets, and a sticky contents box

The site's own templates replace Ananke's (the theme stays as a fallback), and page styles move into one stylesheet.

## Phase 5: Polish (`phase-5-polish`)

- Dark mode.
- A retro "signal lost" 404 page.
- Print and reduced-motion styles.
- A full favicon set and theme color.
- An automated accessibility audit, with fixes.
- Final docs.
