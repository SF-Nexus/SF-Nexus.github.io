# SF-Nexus Website: TODO and handoff

Operator-facing checklist of outstanding work for sfnexus.org (Hugo, this repo). Agents: see AGENTS.md. See PHASES.md for the staged rollout (phases 1–3 are merged, PR #28; phases 4–5, the visual redesign, are parked on their branches).

## Review, 2026-10-23 (pick what to fix; nothing below has been changed on the site)

Fresh pass over the `hugo-0.168` branch and live sfnexus.org: a clean 0.168 build (0 warnings), every link on every page checked, axe-core on all pages at 1280px and 390px, an overflow check from 320 to 1280px, and the 09-13 content review (`../data-lifecycle-review-2026-09.md`) re-checked against the merged site. Internal links and in-page anchors are all fine, no page overflows sideways, and every page except the homepage has 0 axe violations.

### 1. Fix before merging `hugo-0.168`

- [ ] **Homepage link contrast regressed with the theme bump.** On `hugo-0.168` the homepage's body links are `#357edd` on the `#f4f4f4` page (3.68:1; WCAG AA needs 4.5:1). axe flags 5 links at both widths. Live (0.131) shows them as `#0000ee`. Cause: ananke 2.19 colors `.nested-links a` `#357edd`, and `layouts/home.html` keeps the `nested-links` class. Fix: drop the class from `home.html`, or set a darker link color in `sfnexus.css`.

### 2. Broken or dying links

- [ ] **The Omeka exhibit is offline.** `lcdssgeo.com` no longer resolves: the domain is registered until 2027-03-23, but its AcuGIS nameservers no longer answer for it. It is linked from About ("Our Omeka S exhibit") and Scholarship ("Digitizing the New Wave"). Wayback has a copy from 2026-02-15. Restore the hosting, point at the Wayback copy, or remove the link.
- [ ] **Two People-page domains have lapsed and are unregistered:** `jameskopaczewski.com` (James Kopaczewski) and `urbandigitalhistory.com` (Gary Scales). Anyone can buy them, so drop the links or point them at Wayback (2022-03-08 and 2025-06-16).
- [ ] **The Paskow collection page is gone.** `library.temple.edu/collections/paskow-science-fiction-collection-science-fiction-and-fantasy` returns 404, and Temple's SCRC page now lists six collecting areas, none of them SF. It is linked from About, Data, and Scholarship. The last Wayback copy is 2025-01-07. The other options are SCRC catalog search or dropping the link.
- [ ] **The Temple Now "Byte-size books" article is a soft 404.** It redirects to an empty now.temple.edu "Latest News" page. It is linked from About and the timeline. Wayback copy: 2025-10-09.
- [ ] **People page:**
  - Matt Shoemaker's profile moved to `/people/matthew-shoemaker`. His title is unchanged.
  - Jeff Antsen's faculty page is a 404 (Wayback: 2024-03-27).
  - Nicole Lemire-Garlic's link now redirects to the generic Klein directory.
  - Temple profiles now give different titles: Holly Tomren, "Head of Metadata Strategy and Digitization Services"; Matthew Ducmanas, "Special Collections Cataloging Librarian"; Kimberly Tully, "Librarian and Curator of Rare Books".
- [ ] **Still unverified (bot walls block scripts and the Claude browser; click them in a normal browser):**
  - every HathiTrust link: the Temple search, the transition FAQ, the non-consumptive use policy, and the submission requirements
  - the three ArchivesSpace links (403)
  - Jeremy Brett's VIVO page
  - the core.ac.uk Brinkley PDF
  - the SAGE, OUP, and De Gruyter landing pages (their DOIs resolve)

### 3. Content that reads out of date

- [ ] **The HTRC notice on Data is in the future tense.** It says capsules "will no longer be accessible after September 30, 2026", and that date has passed. It also says Extracted Features "will remain available from HathiTrust and the University of Illinois". HathiTrust's transition guide only says EF moves to "HathiTrust and/or other host", with no host named (see `../sf-hathitrust-mining/working/htrc-ef-retirement-research-2026-10.md`).
- [ ] **`sfnexus.io` expires 2026-12-28** (Name.com). Temple's Datasets page and the SF-Nexus GitHub org profile still link to `sfnexus.io`, which 301s here. Either renew it, or get those two links changed to sfnexus.org before it lapses. sfnexus.org and sfnexus.net run to 2027-05-30.
- [ ] **Points from the 09-13 review still open on the homepage:**
  - "disaggregated word-frequency datasets": the published sets are sorted bags of words, not frequency tables.
  - "These are legal to share where the full texts are not": a categorical legal claim; your call on the register.
  - "We apply two analytical lenses to the same data": Word2Vec ran on full text in HathiTrust, not on the EF sets.
  - Stage 4 says "the corpus itself is browsable" in HathiTrust: 348 of 403 volumes are deposited, they are search-only, and the link is the whole Temple-contributed facet, not an SF list. Your 08-10 note has a curated HathiTrust collection (`c=1482459616`) as a possible better target.
  - Stage 4, "Publish: making it citable and reusable", still points at Scholarship, which is mostly other people's resources.
  - The lifecycle section is still the 07-03 machine-drafted copy, waiting on the Alex/SaraGrace read.

  Resolved since that review: the Hugging Face link goes to the org page, and the hero is the Paskow photo.
- [ ] **Article citation.** Crossref confirms the title as "...Speculating on the Future of Library Curation", pp. 211–242 (About says 211–241), with DOI 10.70249/9781606181089-012. That closes the "confirm the article title" item below once you pick the page range.
- [ ] **The timeline stops at "2026: sfnexus.org".** It is dated 2026-05-30, but the lifecycle reorganization it describes merged 09-26. There are no entries for later talks (your notes list TCDL 2024). Add entries only if you want them.

### 4. Layout (minor; not a redesign)

- [ ] **Page descriptions are hard to read over the screenshot headers** on Data, Topic Models, Word Embeddings, and OCR: thin light text over busy text images. It is worst on Data at phone width. The live site looks the same. A stronger header overlay in `sfnexus.css` would fix it.
- [ ] **The stage rail wraps on phones.** At 375px the current item "03 Analyze" breaks onto two lines on Topic Models and Word Embeddings.
- [ ] **The BookNLP snippet on Data** filters with `os.path.isfile(f)` on bare names, so it finds nothing unless it runs inside `path`.

### 5. Your site notes, answered by the site itself

- "Did we upload SF Nexus data to Nomic AI?": Topic Models says embeddings of 142 cli-fi texts were mapped in Nomic Atlas, and the public map still loads.
- "Laure says don't use Gensim on the website": Gensim is named on Topic Models (the LDA notebook title and text) and Word Embeddings.

### 6. Housekeeping in this file and PHASES.md

- The "request indexing" item below: live now serves `index, follow`, robots.txt says `Allow: /`, and the sitemap lists all 8 pages. Only the Search Console request is left.
- The "check that Netlify is reading netlify.toml" item: it is. Live reports Hugo 0.131.0, which is `main`'s pin, and the `/models/lda_clifi_1` and `sfnexus.io` redirects, which exist only in netlify.toml, work. Re-check for 0.168 after the merge.
- The "verify external links" item: covered by section 2 above. Only the bot-walled list is left.
- The idea "Fix the Data Speculations Events page": dataspeculations.org/events still dates "Toxic Water" to 2024.
- PHASES.md "Branches no longer needed once PR #28 is merged": PR #28 merged 09-26, but all seven branches are still on GitHub. PHASES.md also predates the Hugo 0.168 and ananke 2.19 bump, so resuming `phase-4-redesign` now means merging the new `main` into it first.
- Forgejo's default branch is `modernize-theme` (07-03, superseded by `hugo-0.168`). The local branches `modernize-theme` and `wip-lifecycle-homepage-stash` are also left over.

## Things only you can do

- [ ] **Update the link in future videos** to the new owned domain, https://sfnexus.org/. You own sfnexus.org now.
- [ ] **Finalize the HathiTrust tracking metadata sheet**, which records what is in HathiTrust and what is not.
- [ ] **After this deploy, request indexing** of https://sfnexus.org/ in Google Search Console. The site shipped `noindex` until phase 1. Confirm that the live page source now shows `<meta name="robots" content="index, follow">` and that https://sfnexus.org/robots.txt says `Allow: /`.
- [ ] **Check that Netlify is reading netlify.toml.** Settings in the file take precedence over the Netlify UI, but only if Netlify finds it (base directory = repo root). The first deploy log should show the build command `hugo --gc --minify` and Hugo 0.168.0.
- [ ] **HTRC Data Capsules shut down on 2026-09-30.** The Data page now says so. Decide whether Temple's local data capsule appliance should become the recommended route for remote full-text work.
- [ ] **Verify external links from a normal network.** The build sandbox could not reach most external hosts; GitHub links were verified. Newly added links to click-test:
  - Scholarship: the collections-as-data DOIs (Zenodo 3152935, 10161976, 8342171), the copyright.gov case summaries, the HathiTrust non-consumptive use policy URL, the Building LLTDM DOI, copyright.gov/1201/2024/, the Underwood DOIs, the *Distant Horizons* page, the Milner & Burgmann and *Convergence* DOIs, the Eaton, Merril, Liverpool SF Hub, and KU Gunn Center pages, and the DHQ article on The Stuff of Science Fiction
  - About: the three scrcarchivesspace.temple.edu links
  - Timeline: the Stanford CESTA seminar page
- [ ] **Confirm the article title.** Sources disagree between "Speculating on the Future of Library Curation" and "Speculation on the Future of Library Curation" (*Trans. APS* 110.3, 2022, pp. 211–241). Check JSTOR.
- [ ] **Confirm the "5,164-volume" Thompson & Mimno workset count** on the Word Embeddings page. Their HTRC report gives 5,135 volumes, their ACH 2021 slides "5,160 volumes," and the GitHub TSV 5,811.
- [ ] **Add a dataset license.** The Hugging Face datasets and the site don't state one. Once chosen, add `license` to `data/datasets.yaml` and to the schema.org markup in `layouts/partials/sfnexus-schema.html`.
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
