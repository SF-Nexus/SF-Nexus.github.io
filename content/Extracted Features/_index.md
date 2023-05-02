---
title: "Extracted Features"
description: "Curating Extracted Features Datasets with NLTK and BookNLP"
cascade:
  featured_image: '/images/extracted_header.png'
menu:
  main:
    weight: 1
---

We used several natural language processing (NLP) tools to curate a dataset of extracted features from our corpus of science fiction texts. Extracted features datasets are particularly useful for researchers who are interested in exploring copyrighted work like our New Wave science fiction collection. Though sharing original, full-text versions of copyrighted work is a violation of copyright law, it is permissible to share "extracted features" from these works, such as disaggregated texts, word frequency counts, and syntactical and semantic descriptors. Extracted features can be used for a variety of analyses, including topic modeling. 

An extended discussion on extracted features can be found on the Scholars' Studio blog: https://sites.temple.edu/tudsc/2019/07/18/curating-copyrighted-corpora-an-r-script-for-extracting-and-structuring-textual-features/

This project made use of multiple Python pipelines to extract features from the science fiction collection. These pipelines are available as both Jupyter Notebooks and Google Colab Notebooks in our Extracted Features Github repository: https://github.com/SF-Nexus/extracted-features/tree/main/notebooks

## Pipeline 1: Text Sectioning and Disaggregation

Our first pipeline focuses on sectioning and disaggregatingthe science fiction texts. Breaking texts into sections (in this case, chapters and n-word chunks) is helpful for researchers working with large texts and corpora. In our case, many of the science fiction texts in the sci-fi collection are 50,000+ words long - quite a lot of words per text to process! Sectioning the data into chapters and "chunks" of 1000 words or less enables faster processing time when analyses like topic modeling and word2vec are performed. It also allows researchers to ask more granular questions about the composition of their texts; for example, what multiple topics or themes emerge across chapters of a book, and what do these indicate about the text's narrative arc?

Disaggregation is the process of transforming full texts into "bag-of-word" models that are not human-readable. These bag-of-word models can be shared where copyrighted full texts cannot, and they're still usable in processes like LDA topic modeling which rely primarily on word *frequencies* rather than word order. 

### Input: TXT Files (Machine-readable versions of science fiction books)

In the case of the sci-fi collection, splitting books into chapters was easy because of the standardized chapter naming conventions employed during the OCR cleaning process. Python code was written to retrieve all text between the "START OF BOOK" and "END OF BOOK" tags in each text, excluding info on title pages, dedications, acknowledgements, etc. From here, we searched for each instance of "CHAPTER" in each text and split the text whenever an occurence was found. 

 ![](/images/extracted_1.png)

The resulting DataFrame contained each chapter of each book as a separate text.

 ![](/images/extracted_2.png)

Because the chapters in some sci-fi texts were much longer than others, we then split each chapter into chunks of 1000 words each.

  ![](/images/extracted_3.png)

Finally, we sorted the words in each chapter-chunk alphabetically in order to transform them from human-readable texts to "bags of words." 
  
### Output: CSV File ("Bag-of-words" versions of segmented science fiction books)
  
The resulting dataframe is available for download on our Extracted Features Github repository: https://github.com/SF-Nexus/extracted-features/tree/main/data 
