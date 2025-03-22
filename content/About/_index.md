---
title: "About"
description: 
cascade:
  featured_image: '/images/about_1.jpeg'
menu:
  main:
    weight: 1
---
SF Nexus is an open access project. Data and resources provided here are free for everyone, including:
* **Extracted Features:** Disaggregated feature sets from copyrighted literature, available for research purposes
* **Python Notebooks:** Custom Jupyter notebooks in Google colab environments for easy exploration of our data
* **Documentation:** Descriptions of pipelines used to digitize and analyze our dataset, from OCR cleaning to topic modeling and visualization
* **Visualizations:** Output generated from analyses of our dataset, including topic modeling and word embeddings

# The SF Nexus

The SF Nexus comprises a collaborative network of research and public libraries with collections of SF, dedicated to making science fiction available online, including as data. While the SF Nexus project is based at Temple University’s Charles Library, we are committed to growing our collaborations with a SF-focused collective research community. This project presents a prototype of what could be developed as a large-scale collaborative digitization between the dozens of science fiction collections across England and North America, including but not limited to the members of the [Science Fiction Collecting Libraries Consortium](http://sfspecialcollections.pbworks.com/w/page/75814541/About%20the%20SciFi%20Collection%20Libraries%20Consortium%20(SFCLC))

The current phase of this website showcases a demonstration project of how libraries can digitize and make available their copyrighted cultural collections as data. Our current focus has been on sharing extracted features of the data, as well as documenting the corpus' ingestion and curation in the HathiTrust Research Center. Additional projects at Temple Libraries involve developing localized data capsules for confidential computing access to copyrighted corpora, as well as novel ways of digitizing corpora under controlled circumstances. 

## Core SF Archive: Paskow Science Fiction Collection
### Temple University Special Collections Research Center
The [Loretta C. Duckworth Scholars Studio](https://library.temple.edu/lcdss) has partnered with [Temple University Libraries’ Special Collections Research Center (SCRC)](https://library.temple.edu/scrc) and [Digital Library Initiatives (DLI)](https://digital.library.temple.edu/) to build a digitized corpus of copyrighted science fiction literature. Besides its voluminous [Urban Archives](https://library.temple.edu/collections/urban-archives), the SCRC also houses a significant collection of science-fiction literature. The [Paskow Science Fiction Collection](https://library.temple.edu/collections/paskow-science-fiction-collection-science-fiction-and-fantasy) was originally established in 1972, when Temple acquired 5,000 science fiction paperbacks from a Temple alumnus, the late David C. Paskow. 

Subsequent donations, including troves of fanzines and the papers of such sci-fi writers as John Varley and Stanley G. Weinbaum, expanded the collection over the last few decades, both in size and in the range of genres. SCRC staff and undergraduate student workers recently performed the usual comparison of gift titles against cataloged books, removing science fiction items that were exact duplicates of existing holdings. A refocusing of the SCRC’s collection development policy for science fiction de-emphasized fantasy and horror titles, so some titles in those genres were removed as well. From this set of deduplicated science fiction, a subset has been digitized over the last few years.

## The SF Digitization Project
For more information on the history of this digitization project since it began in 2017, and to see an exhibit of selected SF book covers from the collection with related metadata, visit our [Omeka S site](https://lcdssgeo.com/omeka-s/s/scifi/page/digitizing-science-fiction)

For an overview of our approach to data curation of literary texts, see Alex Wermer-Colan's and James Kopaczewski's article, ["The New Wave of Digital Collections: Speculating on the Future of Library Curation"](https://www.jstor.org/stable/45420508#metadata_info_tab_contents)(2022). 

Ultimately, the SF Nexus seeks to build and share a comprehensive dataset of science fiction literature. Due to limitations imposed on copyright, this project explores speculative approaches to data curation that can make elements of each book available to enable large scale analysis. 

At this time, the most valuable web resources include:
* [**Project Gutenberg**](https://www.gutenberg.org/): A library containing 70,000+ free ebooks for which U.S. copyright has expired.
* [**Internet Archive**](https://archive.org/): A non-profit library containing millions of free books, movies, and music, as well as billions of archived web pages; books out of copyright are available to download.
* [**Luminist.org**](http://www.luminist.org/archives/SF/): A variety of cultural documents, including science fiction, fantasy and "weird fiction," available for download and purhcase: 

A future goal is to develop a dataset combining materials from these sources. Separately, work is ongoing to digitize old paperbacks and pulp magazines at institutions like Temple University Library. This hub will also help to make those copyrighted materials available, for example, as derived datasets of extracted features like those available from HathiTrust. 

## Ingesting Our SF Archive into HathiTrust Digital Library
Temple has ingested over 300 science fiction texts into the HathiTrust Digital Library. Because [HathiTrust requires specific file formats](https://www.hathitrust.org/member-libraries/resources-for-librarians/contributor-toolkit/submission-package-requirements/) for upload, Python code was used to packaged all necessary files for the sf collection. Running the Python ingestion code in the command line generated the following files for upload to HathiTrust:

* Image files (TIFF) for each page of each title (duplicated from server)
* OCR files for each page of each title (generated by Google Tesseract)
* Metadata file (YML) containing administrative and technical metadata
* Checksum file listing every file in package and its corresponding md5 hash value

The ingestion code and associated tutorial are available on our [HathiTrust-Ingestion-Scripts Github Repository](https://github.com/SF-Nexus/HathiTrust-Ingestion-Scripts).

# Funding and Support
This work has been made possible by Temple University's Arts and Humanities grant funding to support "The Stories We Tell Ourselves: The Cultural Analytics of Climate Fiction in the Age of the Anthropocene," a project to support graduate students in digital humanities research and work through contributing to the science fiction digitization project. Temple University Libraries has also continuously since 2017 invested money, staff, and resources into supporting the side project of digitizing deaccessioned books from the Paskow Science Fiction Collection.

This project has culminated in an Institute of Museums and Library Services National Leadership Grant for Libraries for Temple University in collaboration with Texas A&M Universities to host a National Forum on legal best practices for curating copyrighted literature. More information on the National Forum can be found on the [Data Speculations website](https://dataspeculations.org).
