# Overview

This repository is for the SF Nexus website, a hub for the curation of science fiction digital collections as data. The current scope of this website focuses on an ongoing project at Temple University's Scholars Studio to digitize and curate science fiction, with a particular emphasis on mid-century climate fiction.

# Relevant Sites

A secondary site where Temple University's science fiction project has been showcased is our Omeka exhibit of science fiction book covers, available at: https://lcdssgeo.com/omeka-s/s/scifi/page/digitizing-science-fiction

# Building locally

The site is built with [Hugo](https://gohugo.io), pinned to 0.131.0 (extended) in `netlify.toml`.

```bash
hugo server   # preview at http://localhost:1313
hugo          # build into public/
```

Netlify deploys `main`. Production deploys set `HUGO_ENV=production`, which the ananke theme requires before it lets search engines index the site.

See `PHASES.md` for the staged improvement plan and `TODO.md` for open items.

# Editing the site

| To change… | Edit |
|---|---|
| Page text | `content/<Section>/_index.md` |
| Navigation menu | `config.toml` (`[[menu.main]]`) |
| Lifecycle stages and their page order (stage rail, previous/next links) | `data/lifecycle.yaml`; a page joins a stage with `stage: source`, `curate`, `analyze`, or `publish` in its front matter |
| Dataset cards and their Google Dataset Search markup | `data/datasets.yaml` |
| Project timeline on About | `data/timeline.yaml` |
| Extra styles | `assets/ananke/css/sfnexus.css` |

Writing tips:

* `![Alt text](/images/file.png "Optional caption")`: images are served as responsive WebP and link to the full-size original, and a title becomes a caption.
* External links get a ↗ and open in a new tab automatically.
* Shortcodes:
  * `{{< notebook path="notebooks/…" title="…" >}}` adds GitHub and "Open in Colab" links
  * `{{< notice title="…" type="note|warning" >}}…{{< /notice >}}` adds a callout box
  * `{{< datasets >}}` adds the dataset cards
  * `{{< timeline >}}` adds the project timeline
  * Put each shortcode on its own line with a blank line before and after, including between two `notebook` lines in a row. Otherwise Markdown wraps them in a paragraph and the HTML is invalid.
* Use `##` for section headings. `##` and `###` headings feed the "On this page" box.
