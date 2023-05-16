---
title: "Data"
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
*Full Code Available on SF Nexus Github:*
* [Text_Sectioning and Disaggregation.ipynb (Google Colab)](https://github.com/SF-Nexus/extracted-features/blob/main/notebooks/google-colab/1_Text_Sectioning_and_Disaggregation%20(Colab).ipynb)
* [Text_Sectioning and Disaggregation.ipynb (Jupyter Notebook)](https://github.com/SF-Nexus/extracted-features/blob/main/notebooks/jupyter-notebooks/1-Text%20Sectioning%20%26%20Disaggregation%20(Jupyter%20Notebook).ipynb)

Our first pipeline focuses on sectioning and disaggregating the science fiction texts. Breaking texts into sections (in this case, chapters and n-word chunks) is helpful for researchers working with large texts and corpora. In our case, many of the science fiction texts in the sci-fi collection are 50,000+ words long - quite a lot of words per text to process! Sectioning the data into chapters and "chunks" of 1000 words or less enables faster processing time when analyses like topic modeling and word2vec are performed. It also allows researchers to ask more granular questions about the composition of their texts; for example, what multiple topics or themes emerge across chapters of a book, and what do these indicate about the text's narrative arc?

Disaggregation is the process of transforming full texts into "bag-of-word" models that are not human-readable. These bag-of-word models can be shared where copyrighted full texts cannot, and they're still usable in processes like LDA topic modeling which rely primarily on word *frequencies* rather than word order. 

**Input: Machine-readable versions (TXT files) of 403 science fiction books**

To develop an extracted features dataset of the full corpus, we first split each text into segments of 1000 words each. These text "chunks" may be particularly useful for analyses like topic modeling given their uniformity across texts, whereas other ways of segmenting texts (like per chapter, as below) will yield segments of various lengths. 

```
# Define chunking function
def split(list_a, chunk_size):
  for i in range(0, len(list_a), chunk_size):
    yield list_a[i:i + chunk_size]

# Set desired size of chunks
chunk_size = 1000

# Create new list for chunked sentences
chunked_ch = []

# Perform chunking function on each row of tokens
s = new_chapters_df['Tokens']
for content in s:
  chunks = list(split(content, chunk_size))
  # Add to new list
  chunked_ch.append(chunks)
```

After running the segmentation function, we sorted  the words in each segment alphabetically in order to transform them from human-readable texts to "bags of words." 

The resulting extracted feature set of disaggregated, chapterized texts is available for download on our [SF Nexus Github page](https://github.com/SF-Nexus/extracted-features/tree/main/data).

**Output 1: [Disaggregated Versions of 403 Texts, Split into 1000-Word Segments](https://github.com/SF-Nexus/extracted-features/tree/main/data).**

We also developed another set of extracted features from our corpus: disaggregated texts split by chapter, rather than 1000-word chunk. Chapter segmentation was possible for a large subsection of our corpus (306 texts), given standardized chapter naming conventions employed during the OCR cleaning process. Python code was written to retrieve all text between the "START OF BOOK" and "END OF BOOK" tags in each text, excluding info on title pages, dedications, acknowledgements, etc. From here, we searched for each instance of "CHAPTER" in each text and split the text whenever an occurence was found. 

```
# Count number of chapters in each text
chapter_counts = books_cleaned['Text'].str.count('CHAPTER')

# Append chapter counts to dataframe
books_cleaned["Chapters"] = chapter_counts

# Make new cell each time new chapter starts 
new = books_cleaned["Text"].str.split("CHAPTER", expand = True).set_index(books_cleaned['Title'])
```

The resulting DataFrame contained each chapter of each book as a separate text.

 ![](/images/Sectioning_Output_1.png)

After splitting texts by chapters, we again sorted the words in each chapters alphabetically in order to transform them from human-readable texts to "bags of words." 

**Output 2: [Disaggregated Versions of 306 Texts, Split into Chapters](https://github.com/SF-Nexus/extracted-features/tree/main/data).**

Finally, we disaggregated the full versions of each text files, for use for researchers who are not interested in using smaller chunks (chapters or 1000-word segments) in their analyses.

**Output 3: [Disaggregated Versions of 403 Full Texts](https://github.com/SF-Nexus/extracted-features/tree/main/data).**

## Pipeline 2: Part-of-Speech Tagging, Named Entity Recognition, and Supersense Tagging
*Full Code Available on SF Nexus Github:*
* [Text Enrichment with BookNLP.ipynb (Google Colab)]()
* [Text Enrichment with BookNLP.ipynb (Jupyter Notebook)]()

Our second pipeline focuses on "enriching" the SF corpus by extracting information like parts of speech, named entities, and "supersense tags" (e.g., "animal", "artifact", "body", "cognition", etc.) from each text. This information (and much more) can be retrieved by running BookNLP in Python. Developed by David Bamman at UC Berkeley, BookNLP is a natural language processing pipeline for large texts. Its functionalities include:
* tokenization
* sentence boundary identification
* part of speech tagging
* dependency parsing
* entity recognition
* entity mapping (aligning aliases to a single character ID)
* gender prediction
Digital humanists have used BookNLP in a variety of capacities, including analyses of [character](https://txtlab.org/2019/01/how-can-we-understand-characters-using-data/) and [gender bias in children's literature](https://etd.library.emory.edu/concern/etds/bk128c14w?locale=en). For a more comprehensive introduction to BookNLP, check out [*Introduction to BookNLP* by W.J.B. Mattingly](https://booknlp.pythonhumanities.com/01_intro.html).

**Input: Machine-readable versions (TXT files) of 403 science fiction books**

We ran the aggregated full texts in our SF collection through BookNLP in Python. Only a few lines of code are needed to run BookNLP in Python:
```
# Define folder where files are stored to run BookNLP on
files = [f for f in os.listdir(path) if os.path.isfile(f)]

# Loop to run book NLP on each file
for f in files: 
    # Define filename as each file in folder
    inputFile = f
    # Set folder for booknlp results
    outputDir = "BookNLP_Results/"
    # Set ID as name of each file
    idd = f
    # Run book nlp on each file
    booknlp.process(inputFile, outputDir, idd)
```
The result of the code above is a folder containing several BookNLP-generated files for each text. Three types of files are available to access on our SF Nexus Github page.

**Output 1: [Tokens files for 403 science fiction books](https://github.com/SF-Nexus/extracted-features/tree/main/data)**
* Files containing information about each token (word, numeral, punctuation mark) in the text, including the position of each token in a paragraph and sentence, general and granular part of speech tags, dependency relationship, syntactic head (indicates relation of token to other words in sentence) and whether or not token indicates an "event" occurence. Token files also contain each token in the text as well as its corresponding lemma, but these columns have been removed before sharing due to copyright regulations.

![](/images/booknlp_1.png)

**Output 2: [Entities files for 403 science fiction books](https://github.com/SF-Nexus/extracted-features/tree/main/data)**
* Files containing information about the "named entities" appearing in the texts: people, organizations, locations, vehicles, among others. As seen in the output, the entity file also denotes the part of speech of each entity and their position in the text. 

![](/images/booknlp_3.png)

**Output 3: [Supersense files for 403 science fiction books](https://github.com/SF-Nexus/extracted-features/tree/main/data)**
* Files containing information about a broader collection of entities appearing in the texts - not only people, places, and locations, but also tokens identified as "emotions," "substances," or "artifacts," among others. As seen in the output, the supersense file also denotes the part of speech of each entity and their position in the text. 

![](/images/booknlp_2.png)

For a more comprehensive overview of BookNLP's output, check out [Chapter 3: "The Output Files"](https://booknlp.pythonhumanities.com/03_files.html) in W. J. B. Mattingly's *Introduction to BookNLP*.