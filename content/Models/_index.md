---
title: "Topic Models"
description: "Modeling a climate-fiction corpus with LDA, BERTopic, and Nomic Atlas semantic maps."
featured_image: '/images/lda_1.png'
---
> **Data lifecycle · Stage 3 of 4 — Analyze.** Reading the corpus at scale through topic modeling. [← Curate](/data/) · See also [Word Embeddings](/analysis/) · Next: [Publish →](/scholarship/)

Topic models find groups of words that tend to occur together across a corpus. That makes them a way to read hundreds of novels at once, and to find the smaller sets of books and chapters worth reading closely. We applied three approaches to the corpus. The first two, LDA and BERTopic, focus on the subset of Temple's collection identified as **climate fiction**. The third maps that subset alongside other genres.

## LDA topic modeling

*By Megan Kane*

* [Topic modeling with LDA (Gensim)](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Analyzing_Extracted_Features/Topic_Modeling_with_LDA%20(Colab).ipynb) · [Open in Colab](https://colab.research.google.com/github/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Analyzing_Extracted_Features/Topic_Modeling_with_LDA%20(Colab).ipynb)

**LDA (Latent Dirichlet Allocation) topic modeling** assumes that documents are mixtures of topics, with the number of topics set by the researcher, and that topics are mixtures of words. To decide which words belong to which topic, LDA starts by assigning each word in the corpus to a topic at random. It then iterates over those assignments, adjusting them until each word sits in the topic where it most probably belongs. Because LDA depends on word frequencies rather than word order, it works well on disaggregated texts like our [extracted-features datasets](/data/).

We ran LDA with Gensim on the climate-fiction subset of Temple's science fiction corpus, after removing stopwords and non-English words. We compared C_V and U_Mass coherence scores across models and found that 200 topics gave the most coherent co-occurrences of words and documents.

![The pyLDAvis interface: an intertopic distance map of the 200-topic model on the left, and on the right the thirty most relevant terms for Topic 35 (water, sea, ocean, lake, shore, waves, wet, sink)](/images/clfi_lda_tm.png)

*Topic 35 in the 200-topic model is dominated by water: *water, sea, ocean, lake, shore*. Topics like this one guided the water-and-toxicity study on the [Word Embeddings](/analysis/) page.*

[**Explore the interactive LDAvis model →**](/ldaviz/) Select any of the 200 topics, and adjust the relevance slider to move between a topic's most frequent terms and its most distinctive ones.

## BERTopic topic modeling

* [Topic modeling with BERTopic](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Analyzing_Extracted_Features/Topic_Modeling_with_BERTopic%20(Colab).ipynb) · [Open in Colab](https://colab.research.google.com/github/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Analyzing_Extracted_Features/Topic_Modeling_with_BERTopic%20(Colab).ipynb)

**BERTopic** builds topic clusters from word embeddings and a class-based TF-IDF. It produces a set of topics, the top words in each, and the likelihood that each text belongs to each topic. Because it relies on embeddings of words in context, it does not work well with disaggregated texts.

Unlike LDA, BERTopic chooses the number of topics itself, though you can set parameters to merge topics that are very similar. On our corpus it produced 91 topics, not counting outliers.

![A two-dimensional map of the topics in the BERTopic model](/images/bertopic_plot.png)

*A two-dimensional map of the topics in our BERTopic model.*

To look more closely, we can extract and visualize the top words per topic:

![Bar charts of the highest-scoring words in each of the eight most frequent BERTopic topics](/images/bertopic_topwords.png)

*Top words in the eight most frequent topics in the corpus.*

### Topics of interest

The most frequent words in a few topics that speak to the climate-fiction focus of the corpus:

![Word cloud for the War Command topic](/images/BERTopic_War_Command_WordCloud.png)

*Topic 33: War Command*

![Word cloud for the Disease Outbreak topic, dominated by vaccine, epidemic, and virus](/images/BERTopic_Epidemic_WordCloud.png)

*Topic 18: Disease Outbreak*

![Word cloud for the Energy topic](/images/BERTopic_Energy_WordCloud.png)

*Topic 47: Energy*

![Word cloud for the Air Pollution topic, dominated by smog, air, hydrocarbon, ozone, and nitrogen oxide](/images/BERTopic_Air_Pollution_WordCloud.png)

*Air Pollution: *smog, air, hydrocarbon, ozone, photochemical, nitrogen oxide**

### Topic usage by author

We can also compare how different authors use topics. Here, for example, is the distribution of topics in the work of Brian Aldiss and Ursula K. Le Guin:

![Chart comparing how often Brian Aldiss and Ursula K. Le Guin use each BERTopic topic](/images/BERTopic_Topic_Use_Comparison_Between_Aldiss_Leguin.png)

*Topic use compared: Brian Aldiss and Ursula K. Le Guin.*

### Topic usage over time

This graph shows how often authors used topics of interest across the twentieth century.

![Chart of how frequently selected topics appear by year of publication across the twentieth century](/images/BERTopic_Topic_Usage_over_Time.png)

*Frequency of selected topics by year of publication.*

> **Reading this chart.** Frequency is counted each time a topic is the dominant topic of a chapter or chunk. A topic can look frequent because it dominates many chapters of a single book, not because it appears across many books. We plan to refine this in future versions of the visualization.

## Mapping semantic similarity with Atlas

* [Mapping semantic similarity with Atlas](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Analyzing_Extracted_Features/Mapping%20Semantic%20Similarity%20with%20Atlas%20(Jupyter%20Notebook).ipynb) · [Open in Colab](https://colab.research.google.com/github/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Analyzing_Extracted_Features/Mapping%20Semantic%20Similarity%20with%20Atlas%20(Jupyter%20Notebook).ipynb)

**Atlas**, from Nomic, is a web platform for exploring large datasets. Researchers can use it to cluster texts by semantic similarity and project them onto a map, as shown below. You can then investigate similarities between data points, refine the dataset, and build new maps from relevant subsets. Maps can be shared publicly for others to explore.

We used Python to map embeddings of 142 texts from our corpus identified as climate fiction. Alongside them we mapped embeddings of science fiction, detective fiction, and fantasy texts from Project Gutenberg. This let us compare the semantic similarities among the three genres, and look for anything that sets climate fiction apart from science fiction more broadly.

![An Atlas map titled Modeling Fiction Genres: thousands of points colored Gutenberg Detective, Gutenberg Sci-Fi, Gutenberg Fantasy, and Temple Cli-Fi. Detective and fantasy form distinct clusters, while the cli-fi points mingle with Gutenberg SF](/images/atlas-output.png)

*Temple's climate fiction (teal) sits within the broader science fiction cloud (orange), while detective fiction (blue) and fantasy (red) form their own regions.*

Explore the interactive version of this map on [Nomic Atlas](https://atlas.nomic.ai/map/9d412be6-372d-4f15-9fde-ec845e74ce52/6e8c245a-1a17-44cc-9858-4022f9683af5).
