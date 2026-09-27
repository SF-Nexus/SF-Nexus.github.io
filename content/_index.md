---
title: The SF Nexus
description: "A hub for science fiction collections as data"
cascade:
  featured_image: '/images/about_1.jpeg'
---
SF Nexus is an open-access hub for studying science fiction as data. Based at Temple University Libraries, it started from a practical question: how can a library digitize a collection of copyrighted paperbacks and still share it with researchers? Our answer is a demonstration project built on Temple's Paskow Science Fiction Collection: 403 novels and anthologies, mostly New Wave SF published between 1945 and 1990. Data and resources here are free for everyone, including:

* **Extracted features:** disaggregated datasets from copyrighted literature, [ready to load](/data/) for research
* **Notebooks:** Jupyter and Google Colab notebooks for exploring the data
* **Documentation:** every step of the pipeline, from OCR cleanup to topic modeling and visualization
* **Visualizations:** topic models, semantic maps, and word embeddings of a climate-fiction subset

**Search the corpus:** 348 Temple-scanned volumes are preserved in the HathiTrust Digital Library. Most are in copyright and therefore *search-only*: you can search the full text and see which pages match. [Browse Temple's science fiction in HathiTrust →](https://babel.hathitrust.org/cgi/ls?field1=ocr;q1=%2A;a=srchls;facet=htsource%3A%22Temple%20University%22)

## Explore the project as a data lifecycle

The SF Nexus follows a single corpus of science fiction through four stages, from the library shelf to a reusable dataset. Each section below is an exhibit of one stage in that pipeline. It documents the process and its concepts, not just its outputs.

**1 · Source: digitizing the collection.** [**OCR**](/ocr/) shows how we turned print scans of Temple's Paskow Science Fiction Collection into machine-readable text with ABBYY FineReader: removing blank pages, tagging chapters, and cleaning the raw recognition output. This is where a copyrighted print collection becomes data under controlled conditions.

**2 · Curate: building the dataset.** [**Data**](/data/) covers how the cleaned texts become shareable "extracted features": disaggregated word-frequency datasets and BookNLP entity and supersense tags drawn from the 403-text corpus. These are legal to share where the full texts are not, and we publish them openly on [Hugging Face](https://huggingface.co/SF-Corpus).

**3 · Analyze: reading the corpus at scale.** We apply two analytical lenses to the same data. [**Topic Models**](/models/) covers LDA and BERTopic on a climate-fiction subset. [**Word Embeddings**](/analysis/) covers Word2Vec, comparing how the SF corpus conceptualizes ecological concepts with broader HathiTrust worksets.

**4 · Publish: making it citable and reusable.** [**Scholarship**](/scholarship/) gathers the datasets, digital archives, and related science-fiction-as-data projects the Nexus builds on. The corpus itself is [browsable in the HathiTrust Digital Library](https://babel.hathitrust.org/cgi/ls?field1=ocr;q1=%2A;a=srchls;facet=htsource%3A%22Temple%20University%22). The aim is a dataset others can find, search, cite, and extend.

The [**About**](/about/) and [**People**](/people/) pages frame the lifecycle: the project's history, the Paskow Collection, and the collaborators behind it.

Ultimately, the SF Nexus seeks to build and share a comprehensive dataset of science fiction literature. Because of copyright restrictions, the project explores speculative approaches to data curation that make elements of each book (its extracted features) available to scholars doing large-scale analysis of text as data. For an overview of our approach, see Alex Wermer-Colan and James Kopaczewski, ["The New Wave of Digital Collections: Speculating on the Future of Library Curation"](https://www.jstor.org/stable/45420508), *Transactions of the American Philosophical Society* 110, no. 3 (2022).
