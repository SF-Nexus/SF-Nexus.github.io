---
title: The SF Nexus
description: "A hub for science fiction collections as data"
cascade:
  featured_image: '/images/hero_genre_atlas.png'
---
SF Nexus is an open access project. Data and resources provided here are free for everyone, including:
* **Extracted Features:** Disaggregated feature sets from copyrighted literature, available for research purposes
* **Python Notebooks:** Custom Jupyter notebooks in Google colab environments for easy exploration of our data
* **Documentation:** Descriptions of pipelines used to digitize and analyze our dataset, from OCR cleaning to topic modeling and visualization
* **Visualizations:** Output generated from analyses of our dataset, including topic modeling and word embeddings

# Overviewing the SF Nexus
The SF Nexus comprises a collaborative network of research and public libraries with collections of SF, dedicated to making science fiction available online, including as data. While the SF Nexus project is based at Temple University’s Charles Library, we are committed to growing our collaborations with a SF-focused collective research community. This project presents a prototype of what could be developed as a large-scale collaborative digitization between the dozens of science fiction collections across England and North America, including but not limited to the members of the [Science Fiction Collecting Libraries Consortium](http://sfspecialcollections.pbworks.com/w/page/75814541/About%20the%20SciFi%20Collection%20Libraries%20Consortium%20(SFCLC))

The current phase of this website showcases a demonstration project of how libraries can digitize and make available their copyrighted cultural collections as data. Our current focus has been on sharing extracted features of the data, as well as documenting the corpus' ingestion and curation in the HathiTrust Research Center. Additional projects at Temple Libraries involve developing localized data capsules for confidential computing access to copyrighted corpora, as well as novel ways of digitizing corpora under controlled circumstances. 

## Explore the project as a data lifecycle

The SF Nexus follows a single corpus of science fiction through four stages — from the library shelf to a reusable dataset. Each section below is an exhibit of one stage in that pipeline, documenting the process and its concepts, not just its outputs.

**1 · Source — digitizing the collection.** [**OCR**](/ocr/) shows how we turned print scans of Temple's Paskow Science Fiction Collection into machine-readable text with ABBYY FineReader: removing blank pages, tagging chapters, and cleaning the raw recognition output. This is where a copyrighted print collection becomes data under controlled conditions.

**2 · Curate — building the dataset.** [**Data**](/data/) covers how the cleaned texts become shareable "extracted features" — disaggregated word-frequency datasets and BookNLP entity and supersense tags drawn from the 403-text corpus. These are legal to share where the full texts are not, and they are published openly through our [HuggingFace repository](https://huggingface.co/datasets/SF-Corpus/extracted_features).

**3 · Analyze — reading the corpus at scale.** Two analytical lenses over the same data: topic modeling in [**Models**](/models/) (LDA and BERTopic, including a climate-fiction subset), and word-embedding studies in [**Analysis**](/analysis/) (Word2Vec, comparing how the SF corpus conceptualizes ecological concepts against broader HathiTrust worksets).

**4 · Publish — making it citable and reusable.** [**Scholarship**](/scholarship/) gathers the datasets, digital archives, and related science-fiction-as-data projects the Nexus builds on, and the corpus itself is [browsable in the HathiTrust Digital Library](https://babel.hathitrust.org/cgi/ls?field1=ocr;q1=%2A;a=srchls;facet=htsource%3A%22Temple%20University%22). The aim is a dataset others can find, search, cite, and extend.

The [**About**](/about/) and [**People**](/people/) pages frame the lifecycle — the project's history, the Paskow Collection, and the collaborators behind it.

Ultimately, the SF Nexus seeks to build and share a comprehensive dataset of science fiction literature. Due to limitations imposed on copyright, this project explores speculative approaches to data curation that can make elements of each book (extracted features) available to scholars seeking to engage in large scale analysis of text as data. 

For an overview of our approach, see Alex Wermer-Colan's and James Kopaczewski's article, ["The New Wave of Digital Collections: Speculating on the Future of Library Curation"](https://www.jstor.org/stable/45420508#metadata_info_tab_contents) (2022). 
