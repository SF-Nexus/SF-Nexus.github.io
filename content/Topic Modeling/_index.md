---
title: "Topic Modeling"
description: "Modeling Science Fiction with Gensim LDA and BERTopic"
cascade:
  featured_image: '/images/lda_1.png'
menu:
  main:
    weight: 1
---
**LDA (Gensim) Topic Modeling** is based on the assumption that documents are a mixture of topics (# topics is set by the researcher) and that topics are a mixture of words. To determine which words belong to each topic, the LDA model randomly assigns each word in a set of documents to a topic, then iterates through the assignments and makes adjustments until all words are assigned to the topics where they have the highest probability of belonging. LDA topic modeling works well on disaggregated texts (like the dataset generated above). 

Using C_V and U_Mass Coherence calculations, we determined that optimal number of topics for the sci-fi collection was 178. In other words, a model with 178 topics provides the most coherent co-occurences of words and documents in each topic. Prior to this analysis, all stopwords and non-English words were removed. Here are the most frequent words present in the top topics in the model (access full dataframe [here](https://github.com/SF-Nexus/extracted-features/blob/main/data/LDA_output/LDA_topics_keywords_df.csv)).

![image](/images/lda_1.png)

**BERTopic Topic Modeling** is a topic modeling tool which creates topic clusters based on word embeddings and a class-based TF-IDF. It generates a set of topics, the top words in each topic, and the likelihood of each text in a corpus belonging to each topic. Because it makes use of word embeddings, it does not work well with disaggregated texts. 

Unlike LDA, BERTopic automatically chooses the number of topics to generate within the model, though parameters can be set to collapse extremely similar topics. Performing BERTopic modeling on the sci-fi corpus yielded 68 topics, excluding Outliers (access full dataframe [here]

Here are the most frequent words in some topics of interest: 
Topic 6: Street and Vehicles

![image](/images/BERTopic_Street_Car_Driving_WordCloud.png)

Topic 17: Disease Outbreak

![image](/images/BERTopic_Disease_Outbreak_WordCloud.png)

Topic 27: Desert Landscape Exploration

![image](/images/BERTopic_Desert_Landscape_Exploration_WordCloud.png)

Topic 61: Air Pollution

![image](/images/BERTopic_Air_Pollution_WordCloud.png)


### Topic Usage Comparison Between Authors

We can also explore usage of topic per author. Here, for example, is a distribution of the topics Used By Brian Aldiss vs. Ursula Leguin

![image](/images/BERTopic_Topic_Use_Comparison_Between_Aldiss_Leguin.png)

### Topic Usage Over Time

Frequency with which authors use topics of interest throughout the 20th century. 
Note: frequency is calculated each time a "chapter/chunk" from a book uses the topic most frequently, so the most frequently used topics might be frequent because of their prevalence across chapters of a particular book rather than across multiple books. This is something to fine-tune in how we build the visualization.

![image](/images/BERTopic_Topic_Usage_over_Time.png)
