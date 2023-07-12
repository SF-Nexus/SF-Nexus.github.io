---
title: "Models"
description: "Modeling Science Fiction"
cascade:
  featured_image: '/images/lda_1.png'
menu:
  main:
    weight: 1
---
## LDA Topic Modeling
*Full Code Available on SF Nexus Github:*
- [Topic Modeling with LDA (Jupyter Notebook)](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Analyzing_Extracted_Features/Topic%20Modeling%20with%20LDA%20(Jupyter%20Notebook).ipynb)
- [Topic Modeling with LDA (Google Colab)](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Analyzing_Extracted_Features/Topic_Modeling_with_LDA%20(Colab).ipynb)

**LDA (Gensim) Topic Modeling** is based on the assumption that documents are a mixture of topics (# topics is set by the researcher) and that topics are a mixture of words. To determine which words belong to each topic, the LDA model randomly assigns each word in a set of documents to a topic, then iterates through the assignments and makes adjustments until all words are assigned to the topics where they have the highest probability of belonging. LDA topic modeling works well on disaggregated texts (like the dataset generated above). 

We ran topic modeling on a subset of Temple's science fiction corpus which has been identified as "climate fiction." Using C_V and U_Mass Coherence calculations, we determined that optimal number of topics for the sci-fi collection was 200. In other words, a model with 200 topics provides the most coherent co-occurences of words and documents in each topic. Prior to this analysis, all stopwords and non-English words were removed. Here are the most frequent words present in the top topics in the model.

[Sample interactive visualization of LDA topic models of climate fiction using LDAviz](https://sf-nexus.github.io/ldaviz/)

## BERTopic Topic Modeling
*Full Code Available on SF Nexus Github:*
- [Topic Modeling with BERTopic (Jupyter Notebook)](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Analyzing_Extracted_Features/Topic%20Modeling%20with%20BERTopic%20(Jupyter%20Notebook).ipynb)
- [Topic Modeling with BERTopic (Google Colab)](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Analyzing_Extracted_Features/Topic_Modeling_with_BERTopic%20(Colab).ipynb)

**BERTopic Topic Modeling** is a topic modeling tool which creates topic clusters based on word embeddings and a class-based TF-IDF. It generates a set of topics, the top words in each topic, and the likelihood of each text in a corpus belonging to each topic. Because it makes use of word embeddings, it does not work well with disaggregated texts. 

Unlike LDA, BERTopic automatically chooses the number of topics to generate within the model, though parameters can be set to collapse extremely similar topics. Performing BERTopic modeling on the sci-fi corpus yielded 91 topics, excluding Outliers.

Here is a 2d representation of the topics in our BERTopic model:

![image](/images/bertopic_plot.png)

To get a closer look at the topics, we can extract and visualize the top words per topic. Here is a bar chart visualization of the top words appearing in the top 8 topics occuring in the corpus:

![image](/images/bertopic_topwords.png)

Here are the most frequent words in some specific topics of interest: 

Topic 33: War Command

![image](/images/BERTopic_War_Command_WordCloud.png)

Topic 18: Disease Outbreak

![image](/images/BERTopic_Epidemic_WordCloud.png)

Topic 47: Energy

![image](/images/BERTopic_Energy_WordCloud.png)

### Topic Usage Comparison Between Authors

We can also explore usage of topic per author. Here, for example, is a distribution of the topics Used By Brian Aldiss vs. Ursula Leguin

![image](/images/BERTopic_Topic_Use_Comparison_Between_Aldiss_Leguin.png)

### Topic Usage Over Time

Frequency with which authors use topics of interest throughout the 20th century. 
Note: frequency is calculated each time a "chapter/chunk" from a book uses the topic most frequently, so the most frequently used topics might be frequent because of their prevalence across chapters of a particular book rather than across multiple books. This is something to fine-tune in how we build the visualization.

![image](/images/BERTopic_Topic_Usage_over_Time.png)

## Mapping Semantic Similarity with Atlas
*Full Code Available on SF Nexus Github:*
- [Mapping Semantic Similarity with Atlas (Jupyter Notebook)](https://github.com/SF-Nexus/extracted-features-notebooks/blob/main/notebooks/Analyzing_Extracted_Features/Mapping%20Semantic%20Similarity%20with%20Atlas%20(Jupyter%20Notebook).ipynb)


**Atlas** is a web platform for exploring large datasets. Researchers can use Atlas to cluster texts based on semantic similarity and project them onto a map, as below. From here, similarities between data points can be investigated, datasets can be refined, and new maps can be build based on relevant subset of data. Maps served on the Atlas browser, Nomic, can be set for public sharing and interaction. 

We used Python to map embeddings of a subset of our science fiction corpus - 142 texts specifically identified as "climate fiction." Along with these texts, we mapped embeddings of Science Fiction, Detective Fiction and Fantasy texts from Project Gutenberg. This allowed us to explore the semantic similarities between the three major genres (science fiction, detective fiction and fantasy) as well as any distinctions between climate fiction texts and the broader genre of science fiction.

![image](/images/atlas-output.png)

View an interactive version of this map here: https://atlas.nomic.ai/map/9d412be6-372d-4f15-9fde-ec845e74ce52/6e8c245a-1a17-44cc-9858-4022f9683af5

