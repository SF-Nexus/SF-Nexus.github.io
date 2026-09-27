# SF-Nexus Website: TODO and handoff

Operator-facing checklist of outstanding work for sfnexus.org (Hugo, this repo). See README.md for where things live.

## Done in the 2026-09 redesign

- [x] **Change the featured/cover image.** The homepage hero is now the Paskow paperback spread (`about_1.jpeg`) under a retro duotone wash. The old `books.jpg` appears only as tinted card and header art.
- [x] **Link the HathiTrust library listing from the homepage.** It is now a hero button, a feature card, and a footer link.
- [x] **Look at Temple's ArchivesSpace for SF.** Linked from About: the Science Fiction Fanzine Collection (SCRC 439), the Science Fiction Collection Vertical File (SCRC 383), and the Eshbach Papers and Fantasy Press Archives. No ArchivesSpace record was found for the Paskow paperbacks themselves; they appear to be a catalogued book collection.
- [x] Merged the `data-lifecycle` branch. Its hand-written stage banners are now generated from `data/lifecycle.yaml`.
- [x] Fixed the robots `noindex` bug. The old theme only allowed indexing when `HUGO_ENV=production` was set, and netlify.toml never set it, so the live site has probably been hidden from search engines. Production builds are now indexable; deploy previews are not.

## Things only you can do

- [ ] **Update the link in future videos** to the owned domain: https://sfnexus.org/
- [ ] **Finalize the HathiTrust tracking metadata sheet**, which records what is in HathiTrust and what is not.
- [ ] **After the next deploy, request indexing** of https://sfnexus.org/ in Google Search Console. Confirm that the live page source shows `<meta name="robots" content="index, follow">`.
- [ ] **Check that the Netlify UI build settings don't override netlify.toml.** netlify.toml now sets `command = "hugo --gc --minify"` and `publish = "public"`.
- [ ] **HTRC Data Capsules shut down on 2026-09-30.** The Data page now says so. Decide whether Temple's local data capsule appliance should become the recommended route for remote full-text work.
- [ ] **Verify external links from a normal network.** The build sandbox could not reach most external hosts. GitHub links were verified; the rest were checked only against search results. Newly added links to verify:
  - Scholarship: the collections-as-data DOIs (Zenodo 3152935, 10161976, 8342171), the copyright.gov case summaries, the HathiTrust non-consumptive use policy URL, the Building LLTDM DOI, copyright.gov/1201/2024/, the Underwood DOIs, the *Distant Horizons* page, the Milner & Burgmann and *Convergence* DOIs, the Eaton, Merril, Liverpool SF Hub, and KU Gunn Center pages, and the DHQ article on The Stuff of Science Fiction
  - About: the three scrcarchivesspace.temple.edu links
  - Timeline: the Stanford CESTA seminar page
- [ ] **Confirm the article title.** Sources disagree between "Speculating on the Future of Library Curation" and "Speculation on the Future of Library Curation" (*Trans. APS* 110.3, 2022, pp. 211–241). Check JSTOR.
- [ ] **Confirm the "5,164-volume" Thompson & Mimno workset count** on the Word Embeddings page. Their HTRC report gives 5,135 volumes, their ACH 2021 slides "5,160 volumes," and the GitHub TSV 5,811.
- [ ] **Add a dataset license.** The Hugging Face datasets and the site don't state one. Once chosen, add `license` to `data/datasets.yaml` and to the schema.org markup in `layouts/partials/schema.html`.
- [ ] **Profile links to recheck:** Jeremy Brett's VIVO link (it points at a "View All" page), Nicole Lemire-Garlic's student page, and Crystal Tatis. The old link went to a WordPress profile-picture attachment, so it was removed.

## Ideas for next iterations

- A browsable title list of the corpus (author, title, year, HathiTrust ID) as a `data/corpus.yaml`-driven page. The HathiTrust tracking sheet above could feed it.
- A cover gallery (PixPlot or a simple grid) drawn from the Omeka exhibit, to bring the paperback art onto the site.
- Unused figures still in `static/images/` for future use: BERTopic word clouds for Desert Landscape, Disease Outbreak, and Street Car Driving; `booknlp_1.png`; `extracted_1–4.png`; `hathi_1.png`; `ocr_input.png`; and `ocr_output.png`.
- Fix the Data Speculations Events page (separate repo), which dates "Toxic Water" to ADHO 2024. It was DH2023 in Graz.

## Research / collections

- [ ] Survey what other SF Collecting Libraries Consortium members hold that could join a multi-institution corpus.
