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
