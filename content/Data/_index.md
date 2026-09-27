---
title: "Data"
description: "Extracted-features datasets built from 403 copyrighted science fiction texts, curated with Python, R, and BookNLP."
featured_image: '/images/extracted_header.png'
---
> **Data lifecycle · Stage 2 of 4 — Curate.** Building the shareable dataset. [← Source](/ocr/) · Next: [Analyze the corpus →](/models/)

Our core corpus is 403 texts from the [Temple University SCRC Paskow Science Fiction Collection](https://library.temple.edu/collections/paskow-science-fiction-collection-science-fiction-and-fantasy). It is mostly New Wave SF novels published between 1945 and 1990, along with short story anthologies and magazines. The texts were scanned and [converted to `.txt` files with ABBYY FineReader](/ocr/). After post-processing and cleaning the OCR output, we curated several datasets at different levels of granularity.

## Extracted features

Most texts in the corpus are still in copyright, so we cannot share the full works. We can share **extracted features**: disaggregated texts, word frequency counts, and syntactic and semantic descriptors. HathiTrust pioneered this approach with its [Extracted Features dataset](https://doi.org/10.13012/R2TE-C227) for millions of volumes. Extracted features still support many kinds of analysis, including topic modeling. These datasets are free for public use:

* **[EF_Full_Texts](https://huggingface.co/datasets/SF-Corpus/EF_Full_Texts)** (403 texts, Python / NLTK): Disaggregated ("bag of words") versions of all 403 texts in the corpus, with cleaned and uncleaned variants and basic metadata (title, author, year, word count).
* **[EF_Chapters_and_Chunks](https://huggingface.co/datasets/SF-Corpus/EF_Chapters_and_Chunks)** (403 texts, Python / NLTK): All 403 texts split into chapters and then into chunks of roughly 1,000 words, each disaggregated into a bag of words. Uniform segments suit topic modeling.
* **[EF_Chapters_Only](https://huggingface.co/datasets/SF-Corpus/EF_Chapters_Only)** (306 texts, Python / NLTK): The 306 texts whose chapters could be detected from OCR tags, split by chapter and disaggregated into bags of words.
* **[EF_Named_Entities](https://huggingface.co/datasets/SF-Corpus/EF_Named_Entities)** (403 texts, BookNLP): BookNLP entity files listing the people, organizations, locations, vehicles, and other named entities in each text, with part of speech and position.
* **[EF_Supersense_Tags](https://huggingface.co/datasets/SF-Corpus/EF_Supersense_Tags)** (403 texts, BookNLP): BookNLP supersense files tagging a broader range of tokens, including emotions, substances, artifacts, animals, and cognition, with part of speech and position.

The three bag-of-words datasets each contain two versions of every text. One is "cleaned" (lowercased, with punctuation, extra spaces, and numbers removed) and one is not. They also include basic metadata about each book: title, author, publication year, and word count. Metadata curation is ongoing, and we plan to add publication details, descriptions, and Library of Congress genre categories.

Loaded into Python, the head of a dataframe looks like this:

![The first five rows of an extracted-features dataframe, with columns for Title, Author, Pub Year, Text, Clean_Text, and Word Count](/images/EF_Header.png)

## Loading the data

All of our extracted-features sets are in the [SF-Corpus organization on Hugging Face](https://huggingface.co/SF-Corpus). You can download them from the website, like files on GitHub, or load them straight into Python with the `datasets` library. The library downloads and caches them locally:

```python
# pip install datasets
from datasets import load_dataset

# Load the chapters-and-chunks version of the SF Nexus corpus
dataset = load_dataset("SF-Corpus/EF_Chapters_and_Chunks")

# Work with it as a pandas DataFrame
df = dataset["train"].to_pandas()
```

For more on working with Hugging Face datasets, see the [loading guide](https://huggingface.co/docs/datasets/loading).

### How to cite

If you use these datasets, please cite the SF Nexus and the specific dataset, for example:

> SF Nexus, Temple University Libraries. *EF_Chapters_and_Chunks* [dataset]. Hugging Face. https://huggingface.co/datasets/SF-Corpus/EF_Chapters_and_Chunks.

For the project's approach, cite Wermer-Colan and Kopaczewski, ["The New Wave of Digital Collections"](https://www.jstor.org/stable/45420508), *Transactions of the American Philosophical Society* 110, no. 3 (2022).

## How the datasets were made

We extracted features from the collection with several Python and R pipelines. They are available as Jupyter and Google Colab notebooks in our [extracted-features-notebooks repository](https://github.com/SF-Nexus/extracted-features-notebooks/tree/main/notebooks). Jeff Antsen discusses the method at length on the Scholars Studio blog in ["Curating Copyrighted Corpora: An R Script for Extracting and Structuring Textual Features"](https://web.archive.org/web/20201030014610/https://sites.temple.edu/tudsc/2019/07/18/curating-copyrighted-corpora-an-r-script-for-extracting-and-structuring-textual-features/) (2019).

### Pipeline 1: Text sectioning and disaggregation

* [Text sectioning and disaggregation (Python)](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Extracting_Features/Text_Sectioning_and_Disaggregation%20(Colab).ipynb) · [Open in Colab](https://colab.research.google.com/github/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Extracting_Features/Text_Sectioning_and_Disaggregation%20(Colab).ipynb)
* [Text sectioning and disaggregation (R)](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/R_scripts/Text%20Sectioning_and_Disaggregation%20(R).R)

Our first pipeline sections and disaggregates the science fiction texts. Breaking long texts into sections (here, chapters and n-word chunks) helps researchers working with large texts and corpora. Many books in the collection run to 50,000 words or more. Splitting them into chapters and chunks of 1,000 words or fewer speeds up analyses like topic modeling and Word2Vec. It also lets researchers ask more granular questions: for example, which topics or themes emerge across a book's chapters, and what they suggest about its narrative arc.

Disaggregation turns full texts into "bag-of-words" models that humans cannot read. These can be shared where copyrighted full texts cannot, and they still work for methods like LDA topic modeling that depend mainly on word *frequencies* rather than word order.

**Input:** machine-readable text files of 403 science fiction books.

To build an extracted-features set of the full corpus, we first split each text into 1,000-word segments. These uniform chunks suit analyses like topic modeling, whereas chapters (below) vary in length. Here is the approach in Python (the R pipeline is documented in the [repository README](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Extracting_Features/extracting_features_readme.md)):

```python
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

After segmenting, we sorted the words in each segment alphabetically. This turns human-readable text into bags of words.

**Output 1:** [disaggregated versions of 403 texts, split into 1,000-word segments](https://huggingface.co/datasets/SF-Corpus/EF_Chapters_and_Chunks).

We also split texts by chapter rather than by 1,000-word chunk. This was possible for a large part of the corpus (306 texts) because chapters were tagged consistently during [OCR cleanup](/ocr/). Python code retrieves all text between each book's `START OF BOOK` and `END OF BOOK` tags, leaving out title pages, dedications, acknowledgements, and so on. It then splits the text at every occurrence of `CHAPTER`:

```python
# Count number of chapters in each text
chapter_counts = books_cleaned['Text'].str.count('CHAPTER')

# Append chapter counts to dataframe
books_cleaned["Chapters"] = chapter_counts

# Make new cell each time new chapter starts
new = books_cleaned["Text"].str.split("CHAPTER", expand = True).set_index(books_cleaned['Title'])
```

The resulting DataFrame holds each chapter of each book as a separate text:

![A dataframe with one row per chapter, labeled by year, author, title, and chapter number (for example 1973_PESEK_THEEARTHISNEAR.txt_Chapter_1), beside the chapter's text](/images/Sectioning_Output_1.png)

As with the chunks, we then sorted the words in each chapter alphabetically to turn them into bags of words.

**Output 2:** [disaggregated versions of 306 texts, split into chapters](https://huggingface.co/datasets/SF-Corpus/EF_Chapters_Only).

Finally, we disaggregated each full text for researchers who don't need smaller units.

**Output 3:** [disaggregated versions of 403 full texts](https://huggingface.co/datasets/SF-Corpus/EF_Full_Texts).

### Pipeline 2: Part-of-speech tagging, named entities, and supersenses

* [Text enrichment with BookNLP](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Extracting_Features/BookNLP%20(Jupyter%20Notebook).ipynb) · [Open in Colab](https://colab.research.google.com/github/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Extracting_Features/BookNLP%20(Jupyter%20Notebook).ipynb)

Our second pipeline "enriches" the corpus by extracting parts of speech, named entities, and supersense tags (such as "animal," "artifact," "body," and "cognition") from each text. BookNLP retrieves all of this and more. It is a natural language processing pipeline for book-length texts, developed by David Bamman at UC Berkeley. Its functions include:

* tokenization
* sentence boundary detection
* part-of-speech tagging
* dependency parsing
* entity recognition
* entity mapping (aligning aliases to a single character ID)
* gender prediction

Digital humanists have used BookNLP to study [character](https://txtlab.org/2019/01/how-can-we-understand-characters-using-data/) and [gender bias in children's literature](https://etd.library.emory.edu/concern/etds/bk128c14w?locale=en). For a fuller introduction, see [*Introduction to BookNLP* by W. J. B. Mattingly](https://booknlp.pythonhumanities.com/01_intro.html).

**Input:** machine-readable text files of 403 science fiction books.

We ran the full (aggregated) texts through BookNLP in Python. It takes only a few lines:

```python
# Define folder where files are stored to run BookNLP on
files = [f for f in os.listdir(path) if os.path.isfile(f)]

# Loop to run BookNLP on each file
for f in files:
    # Define filename as each file in folder
    inputFile = f
    # Set folder for BookNLP results
    outputDir = "BookNLP_Results/"
    # Set ID as name of each file
    idd = f
    # Run BookNLP on each file
    booknlp.process(inputFile, outputDir, idd)
```

This produces a folder of BookNLP files for each text. Two kinds of files are published on our Hugging Face page.

**Output 1:** [entity files for 403 science fiction books](https://huggingface.co/datasets/SF-Corpus/EF_Named_Entities). These list the named entities in each text (people, organizations, locations, vehicles, and more), with each entity's part of speech and position in the text.

![BookNLP entity output for William Hope Hodgson's The House on the Borderland, with columns for coreference ID, start and end token, mention type, category (PER, LOC, FAC), and entity text](/images/booknlp_3.png)

**Output 2:** [supersense files for 403 science fiction books](https://huggingface.co/datasets/SF-Corpus/EF_Supersense_Tags). These tag a broader range of tokens beyond people, places, and locations, including tokens identified as "emotions," "substances," or "artifacts." Each tag also records part of speech and position in the text.

![BookNLP supersense output listing start and end tokens, supersense categories such as noun.location, noun.substance, and verb.emotion, and the tagged text](/images/booknlp_2.png)

For a fuller overview of BookNLP's output, see [Chapter 3, "The Output Files"](https://booknlp.pythonhumanities.com/03_files.html) of Mattingly's *Introduction to BookNLP*.

## Full-text analysis

Researchers can analyze the full texts, without reading them, in two ways. On site at Temple, the Scholars Studio provides supervised access for non-consumptive research (see [OCR](/ocr/#output-txt-files)). Remotely, researchers have been able to analyze HathiTrust volumes, including in-copyright works, in the HathiTrust Research Center (HTRC) Data Capsule, a secure computing environment. Temple's [data capsule appliance](https://github.com/TempleDSS/data-capsule-appliance) is a way to set up and run that kind of environment locally.

> **HathiTrust Research Center transition.** HathiTrust is ending its funding of the HathiTrust Research Center at the end of 2026. **HTRC Data Capsules, and the data in them, will no longer be accessible after September 30, 2026.** Derived datasets such as HTRC Extracted Features will remain available from HathiTrust and the University of Illinois. See the [HTRC transition FAQ](https://www.hathitrust.org/about/research-center/htrc-transition-faq/) for details.

## Take-down notice

This site shares only extracted features of copyrighted fiction. No copyrighted work is made available to read. These derived files are provided for education and research. Temple University Libraries has credited rights holders where possible. If you hold rights to materials in our digitized collections that are not credited, please let us know so we can keep our information accurate.

If you are a rights holder and believe this site includes material you have not permitted (or that is not covered by an exception under U.S. copyright law), you can request its removal by writing to [digitalscholarship@temple.edu](mailto:digitalscholarship@temple.edu). For more on non-consumptive research, see HathiTrust's [Non-Consumptive Use Research Policy](https://www.hathitrust.org/the-collection/terms-conditions/non-consumptive-use-policy/).
