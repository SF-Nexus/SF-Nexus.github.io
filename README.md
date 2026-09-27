# SF Nexus website

Source for [sfnexus.org](https://sfnexus.org), a hub for science fiction collections as data. The SF Nexus is based at Temple University Libraries' Loretta C. Duckworth Scholars Studio. It digitizes mid-century science fiction from the Paskow Science Fiction Collection, deposits it in HathiTrust, and publishes extracted-features datasets on [Hugging Face](https://huggingface.co/SF-Corpus).

Related sites:

* The Omeka exhibit of SF book covers: https://lcdssgeo.com/omeka-s/s/scifi/page/digitizing-science-fiction
* The Data Speculations national forum: https://dataspeculations.org

## Building locally

The site is built with [Hugo](https://gohugo.io), pinned to **0.131.0 extended** in `netlify.toml`. Netlify deploys `main` automatically.

```bash
hugo server          # preview at http://localhost:1313 (pages are marked noindex)
hugo --gc --minify   # production build into public/
```

## How the site is organized

The site is structured as a **data lifecycle**: one corpus followed through four stages.

| Stage | Page | Folder |
|---|---|---|
| 01 Source | OCR | `content/OCR/` |
| 02 Curate | Data | `content/Data/` |
| 03 Analyze | Topic Models, Word Embeddings | `content/Models/`, `content/Analysis/` |
| 04 Publish | Scholarship | `content/Scholarship/` |

About and People frame the lifecycle. A page joins a stage with `stage: source|curate|analyze|publish` in its front matter. It then gets the stage chip, the progress rail at the top, and previous/next links at the bottom automatically.

### Where to edit things

| To change… | Edit |
|---|---|
| Page text | `content/<Section>/_index.md` |
| Homepage hero, stats, and feature cards | front matter of `content/_index.md` |
| Lifecycle stages (names, blurbs, card images, page order) | `data/lifecycle.yaml` |
| Hugging Face dataset cards and their schema.org markup | `data/datasets.yaml` |
| Project timeline on the About page | `data/timeline.yaml` |
| Navigation menu | `config.toml` (`[[menu.main]]`) |
| Colors, fonts, layout | `assets/css/sfnexus.css` (color tokens at the top) |
| Page templates | `layouts/` |

### Writing content

* **Images:** `![Alt text](/images/file.png)` is automatically served as responsive WebP and links to the full-size original. Add a title to get a captioned figure: `![Alt text](/images/file.png "Caption")`. Put image files in `static/images/`.
* **External links** open in a new tab and get a small ↗ automatically.
* **Shortcodes:**
  * `{{< notebook path="notebooks/…/file.ipynb" title="…" >}}` links a file in [extracted-features-notebooks](https://github.com/SF-Nexus/extracted-features-notebooks), with an "Open in Colab" button for notebooks
  * `{{< notice title="…" type="note|warning" >}}Markdown{{< /notice >}}` adds a callout box
  * `{{< datasets >}}` adds the dataset cards
  * `{{< timeline >}}` adds the project timeline
* Use `##` for section headings. The page title is the only `#` heading. `##` and `###` headings feed the "On this page" contents box.

## Theme

The look is a retro science fiction paperback theme: pulp-paper grounds, deep-space navy bands, duotone halftone art, and self-hosted Michroma, Space Grotesk, and Space Mono fonts (SIL OFL, in `static/fonts/`). It lives entirely in `layouts/` and `assets/css/sfnexus.css`.

Several structural and accessibility patterns are adapted from the [Philly Community Wireless](https://github.com/phillycommunitywireless/phillycommunitywireless) Hugo theme: the skip link, the accessible menu toggle, focus styles, the responsive-image render hook, and the notice and timeline components. The vendored `themes/gohugo-theme-ananke` is kept only as a fallback. The site's own templates override everything it renders.

`static/ldaviz/` is a standalone copy of the interactive pyLDAvis topic model, served at [sfnexus.org/ldaviz/](https://sfnexus.org/ldaviz/).
