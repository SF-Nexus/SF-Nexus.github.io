# SF-Nexus Website: TODO and handoff

Operator-facing checklist of outstanding work for sfnexus.org (Hugo, this repo). See PHASES.md for the staged rollout (phases 1–3 go live when this branch merges; phases 4–5, the visual redesign, are parked on their branches).

## Things only you can do

- [ ] **Update the link in future videos** to the new owned domain, https://sfnexus.org/. You own sfnexus.org now.
- [ ] **Finalize the HathiTrust tracking metadata sheet**, which records what is in HathiTrust and what is not.
- [ ] **After this deploy, request indexing** of https://sfnexus.org/ in Google Search Console. The site shipped `noindex` until phase 1. Confirm that the live page source now shows `<meta name="robots" content="index, follow">` and that https://sfnexus.org/robots.txt says `Allow: /`.
- [ ] **Check that Netlify is reading netlify.toml.** Settings in the file take precedence over the Netlify UI, but only if Netlify finds it (base directory = repo root). The first deploy log should show the build command `hugo --gc --minify` and Hugo 0.131.0.
- [ ] **HTRC Data Capsules shut down on 2026-09-30.** The Data page now says so. Decide whether Temple's local data capsule appliance should become the recommended route for remote full-text work.
- [ ] **Verify external links from a normal network.** The build sandbox could not reach most external hosts; GitHub links were verified. Newly added links to click-test:
  - Scholarship: the collections-as-data DOIs (Zenodo 3152935, 10161976, 8342171), the copyright.gov case summaries, the HathiTrust non-consumptive use policy URL, the Building LLTDM DOI, copyright.gov/1201/2024/, the Underwood DOIs, the *Distant Horizons* page, the Milner & Burgmann and *Convergence* DOIs, the Eaton, Merril, Liverpool SF Hub, and KU Gunn Center pages, and the DHQ article on The Stuff of Science Fiction
  - About: the three scrcarchivesspace.temple.edu links
  - Timeline: the Stanford CESTA seminar page
- [ ] **Confirm the article title.** Sources disagree between "Speculating on the Future of Library Curation" and "Speculation on the Future of Library Curation" (*Trans. APS* 110.3, 2022, pp. 211–241). Check JSTOR.
- [ ] **Confirm the "5,164-volume" Thompson & Mimno workset count** on the Word Embeddings page. Their HTRC report gives 5,135 volumes, their ACH 2021 slides "5,160 volumes," and the GitHub TSV 5,811.
- [ ] **Add a dataset license.** The Hugging Face datasets and the site don't state one. Once chosen, add `license` to `data/datasets.yaml` and to the schema.org markup in `layouts/partials/schema.html`.
- [ ] **Profile links to recheck:** Jeremy Brett's VIVO link (it points at a "View All" page) and Nicole Lemire-Garlic's student page.

## Done

- [x] **Change the featured/cover image.** The homepage hero is now the Paskow paperback photo (phase 2).
- [x] **Link the HathiTrust library listing from the homepage.** There is now a "Search the corpus" line near the top (phase 2).
- [x] **Look at Temple's ArchivesSpace for SF.** About now links the Science Fiction Fanzine Collection (SCRC 439), the Science Fiction Collection Vertical File (SCRC 383), and the Eshbach Papers and Fantasy Press Archives (phase 3). No ArchivesSpace record was found for the Paskow paperbacks themselves; they appear to be a catalogued book collection.
- [x] **Search-engine indexing fixed** (phase 1): the theme only allows indexing when `HUGO_ENV=production`, which was never set.
- [x] **Merged the `data-lifecycle` branch** (phase 2).

## Ideas for next iterations

- The retro SF paperback redesign: `phase-4-redesign`, then `phase-5-polish`.
- A browsable title list of the corpus (author, title, year, HathiTrust ID), possibly fed by the HathiTrust tracking sheet above.
- A cover gallery drawn from the Omeka exhibit.
- Unused figures in `static/images/` for future use: BERTopic word clouds for Desert Landscape, Disease Outbreak, and Street Car Driving; `booknlp_1.png`; `extracted_1–4.png`; `hathi_1.png`; `ocr_input.png`; `ocr_output.png`; and `hero_genre_atlas.png`.
- Fix the Data Speculations Events page (separate repo), which dates "Toxic Water" to ADHO 2024. It was DH2023 in Graz.

## Reference

- `config.toml`: site config and menu
- `content/`: Markdown pages
- `data/`: lifecycle stages, datasets, and project timeline
- `layouts/`: template overrides, render hooks, and shortcodes on top of the ananke theme
- `assets/ananke/css/sfnexus.css`: extra styles
- `static/`: images, favicon, and `/ldaviz/`
