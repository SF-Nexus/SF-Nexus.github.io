---
title: "OCR"
description: "Optical Character Recognition with Abbyy"
cascade:
  featured_image: '/images/ocr.png'
menu:
  main:
    weight: 1
---

We used Optical Character Recognition (OCR) software to convert scans of our print sci-fi books into computer-readable text files. OCR expands the potential uses of our corpus, allowing researchers to not only review scanned image files, but also to search, clean, and analyze digital texts using computational tools.

### Input: TIFF Files (Digital scans of science fiction book pages)

This project made use of Abbyy FineReader, a commercial software which uses AI-based technology to recognize text in image files including TIFFs, PNGs, and PDFs. We uploaded collections of page scans to Abbyy, one book at a time, and performed OCR. We also used Abbyy to assist in the following tasks: 

- **Removing blank pages**

 ![](/images/ocr_blank.png)

* **Reviewing pages with "unrecognized" elements (illustrations, charts, icons and other content that OCR cannot automatically convert)**

 ![](/images/ocr_unrecognized.png)


* **Identifying pages that were ripped, blurred, cut off, or otherwise require manual cleaning**

 ![](/images/ocr_cut.png)

* **Removing headers, footers and page numbers**

 ![](/images/ocr_header.png)

* **Adding tags denoting START OF BOOK, END OF BOOK, and CHAPTER (each time new section or chapter starts)**

 ![](/images/ocr_chapter.png)

Completing the above-mentioned tasks has yielded a collection of minimally cleaned and enriched text files that can be searched and analyzed digitally. 

### Output: TXT Files (Machine-readable versions of science fiction books)

Because the science fiction collection is under copyright, the exported text files can only be accessed through a visit to the Temple University Loretta C. Duckworth Scholars Studio, where researchers must sign an agreement to only use these materials at the Scholars Studio for non-consumptive research. A dataset of **[extracted features](https://github.com/SF-Nexus/extracted-features)** from these texts is freely availble on this website. 

See our full workflow for performing  OCR on the science fiction corpus here: https://github.com/SF-Nexus/OCR/blob/main/abbyy.md  
