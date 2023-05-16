---
title: "Extracted Features"
description: "Curating Extracted Features Datasets with NLTK and BookNLP"
cascade:
  featured_image: '/images/extracted_header.png'
menu:
  main:
    weight: 1
---

Our core SF corpus is comprised of 403 texts from the [Temple University SCRC Paskow Science Fiction Collection](https://library.temple.edu/collections/paskow-science-fiction-collection-science-fiction-and-fantasy). The corpus primarily contains New Wave SF novels published between 1945 and 1990, along with short story anthologies and magazines. The texts have been scanned, digitized and saved as ```.txt``` files using Abbyy OCR. While all texts have been cleaned, scanned, and run through OCR, thorough OCR cleaning of about 150 texts is still in progress. As such, we have several datasets of varying granularity available at this time; see below for details. Visit [our Github page](https://github.com/SF-Nexus/extracted-features/tree/main/data) to download metadata associated with our full corpus. 

Because the majority of texts in our corpus are under copyright, sharing the original, full-text works is a violation of copyright law. However, it is permissible to share "extracted features" from these works, such as disaggregated texts, word frequency counts, and syntactical and semantic descriptors. Extracted features can be used for a variety of analyses, including topic modeling.  We used several natural language processing (NLP) tools to curate a dataset of extracted features from our corpus of science fiction texts. 

An extended discussion on extracted features can be found on the Scholars' Studio blog: https://sites.temple.edu/tudsc/2019/07/18/curating-copyrighted-corpora-an-r-script-for-extracting-and-structuring-textual-features/

This project made use of multiple Python pipelines to extract features from the science fiction collection. These pipelines are available as both Jupyter Notebooks and Google Colab Notebooks in our Extracted Features Github repository: https://github.com/SF-Nexus/extracted-features/tree/main/notebooks

## Pipeline 1: Text Sectioning and Disaggregation

Our first pipeline focuses on sectioning and disaggregating the science fiction texts. Breaking texts into sections (in this case, chapters and n-word chunks) is helpful for researchers working with large texts and corpora. In our case, many of the science fiction texts in the sci-fi collection are 50,000+ words long - quite a lot of words per text to process! Sectioning the data into chapters and "chunks" of 1000 words or less enables faster processing time when analyses like topic modeling and word2vec are performed. It also allows researchers to ask more granular questions about the composition of their texts; for example, what multiple topics or themes emerge across chapters of a book, and what do these indicate about the text's narrative arc?

Disaggregation is the process of transforming full texts into "bag-of-word" models that are not human-readable. These bag-of-word models can be shared where copyrighted full texts cannot, and they're still usable in processes like LDA topic modeling which rely primarily on word *frequencies* rather than word order. 

### Input: TXT Files (Machine-readable versions of science fiction books)

In the case of the sci-fi collection, we were able to split many of the books into chapters because of the standardized chapter naming conventions employed during the OCR cleaning process. Python code was written to retrieve all text between the "START OF BOOK" and "END OF BOOK" tags in each text, excluding info on title pages, dedications, acknowledgements, etc. From here, we searched for each instance of "CHAPTER" in each text and split the text whenever an occurence was found. 

```
#Count number of chapters in each text
chapter_counts = books_cleaned['Text'].str.count('CHAPTER')

#Append chapter counts to dataframe
books_cleaned["Chapters"] = chapter_counts

#Make new cell each time new chapter starts 
new = books_cleaned["Text"].str.split("CHAPTER", expand = True).set_index(books_cleaned['Title'])
```

The resulting DataFrame contained each chapter of each book as a separate text.

 ![](/images/extracted_2.png)


After splitting texts by chapters, we sorted the words in each chapters alphabetically in order to transform them from human-readable texts to "bags of words." The resulting extracted feature set of disaggregated, chapterized texts is available for download on our [SF Nexus Github page](https://github.com/SF-Nexus/extracted-features/tree/main/data).

We were  able to segment XXX texts into chapters, as these are the texts that have been thoroughly cleaned in Abby FineReader thus far. To develop an extracted features dataset of the full corpus, we developed a second function to split each text into segments of 1000 words each. These text "chunks" are somewhat equivalent in chapter length, and indeed may be particularly useful for analyses like topic modeling given their uniformity across texts, whereas chapter lenghts often vary. 

```
#Define chunking function
def split(list_a, chunk_size):
  for i in range(0, len(list_a), chunk_size):
    yield list_a[i:i + chunk_size]

#Set desired size of chunks
chunk_size = 1000

#Create new list for chunked sentences
chunked_ch = []

#Perform chunking function on each row of tokens
s = new_chapters_df['Tokens']
for content in s:
  chunks = list(split(content, chunk_size))
  #Add to new list
  chunked_ch.append(chunks)
```

After running the segmentation function, we sorted again the words in each segment alphabetically in order to transform them from human-readable texts to "bags of words." The resulting extracted feature set of disaggregated, chapterized texts is available for download on our [SF Nexus Github page](https://github.com/SF-Nexus/extracted-features/tree/main/data).

### Output: CSV Files ("Bag-of-words" versions of segmented science fiction books)

## Pipeline 2: Part-of-Speech Tagging, Named Entity Recognition, and Supersense Tagging

Our second pipeline focuses on "enriching" the SF corpus by extracting information like parts of speech, named entities, and "supersense tags" (e.g., "animal", "artifact", "body", "cognition", etc.) from each text. This information (and much more) can be retrieved by running BookNLP in Python. Developed by David Bamman at UC Berkeley, BookNLP is a natural language processing pipeline for large texts. Its functionalities include:
* tokenization
* sentence boundary identification
* part of speech tagging
* dependency parsing
* entity recognition
* entity mapping (aligning aliases to a single character ID)
* gender prediction
Digital humanists have used BookNLP in a variety of capacities.
