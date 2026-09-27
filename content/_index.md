---
title: The SF Nexus
description: "SF Nexus digitizes mid-century science fiction from Temple University Libraries and shares it as open, research-ready data."
featured_image: '/images/about_1.jpeg'

# Homepage hero. The buttons render left to right.
hero:
  image: /images/about_1.jpeg
  alt: "A spread of vintage science fiction paperbacks and magazines from the Paskow Collection, including Amazing Stories, Marvel Science Fiction, and DAW novels."
  kicker: "Temple University Libraries · Paskow Science Fiction Collection"
  tagline: "Mid-century science fiction, digitized and shared as open, research-ready data."
  buttons:
    - text: Get the data
      url: /data/
      class: btn--primary
    - text: "Search the corpus in HathiTrust ↗"
      url: "https://babel.hathitrust.org/cgi/ls?field1=ocr;q1=%2A;a=srchls;facet=htsource%3A%22Temple%20University%22"
      class: btn--ghost

# "By the numbers" band under the hero.
stats:
  - value: "5,000"
    label: paperbacks in the 1972 gift that founded the Paskow Collection
  - value: "403"
    label: novels and anthologies digitized as machine-readable text
  - value: "348"
    label: Temple-scanned volumes deposited in HathiTrust
  - value: "5"
    label: open extracted-features datasets on Hugging Face

# Three cards at the foot of the page. color: rocket | atomic | ray | nebula
features:
  - kicker: The corpus
    title: Search it in HathiTrust
    color: rocket
    text: "Temple's scans are preserved in the HathiTrust Digital Library. Most titles are in copyright, so they are *search-only*: you can search the full text and see which pages match without reading the scans."
    link:
      text: Browse Temple's SF in HathiTrust
      url: "https://babel.hathitrust.org/cgi/ls?field1=ocr;q1=%2A;a=srchls;facet=htsource%3A%22Temple%20University%22"
  - kicker: The approach
    title: The New Wave of Digital Collections
    color: ray
    text: "Alex Wermer-Colan and James Kopaczewski on speculative approaches to curating copyrighted literature as data. *Transactions of the American Philosophical Society* 110, no. 3 (2022): 211–241."
    link:
      text: Read on JSTOR
      url: "https://www.jstor.org/stable/45420508"
  - kicker: What's next
    title: Data Speculations
    color: nebula
    text: "An IMLS-funded national forum, led by Temple and Texas A&M, on how libraries can steward copyrighted contemporary culture as data."
    link:
      text: Visit dataspeculations.org
      url: "https://dataspeculations.org"
---
SF Nexus is an open-access hub for studying science fiction as data. Based at Temple University Libraries, it started from a practical question: how can a library digitize a collection of copyrighted paperbacks and still share it with researchers?

Our answer is a demonstration project built on Temple's [Paskow Science Fiction Collection](/about/#the-paskow-science-fiction-collection). We have 403 novels and anthologies, mostly New Wave SF published between 1945 and 1990. They were scanned, run through OCR, deposited in HathiTrust, and released as **extracted features**: derived datasets that support text mining without reproducing the books. Everything here is free to use:

* **Extracted features:** disaggregated datasets from copyrighted literature, [ready to load](/data/) for research
* **Notebooks:** Jupyter and Google Colab notebooks for exploring the data
* **Documentation:** every step of the pipeline, from [OCR cleanup](/ocr/) to [topic modeling](/models/) and [word embeddings](/analysis/)
* **Visualizations:** topic models, semantic maps, and embedding studies of a climate-fiction subset

The SF Nexus is also a prototype for something larger. It could grow into a collaborative network of research and public libraries, including members of the [Science Fiction Collecting Libraries Consortium](http://sfspecialcollections.pbworks.com/w/page/75814541/About%20the%20SciFi%20Collection%20Libraries%20Consortium%20(SFCLC)), that make the world's science fiction collections available as data. [Read the project's story →](/about/)
