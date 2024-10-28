---
title: "Analysis"
description: Word2Vec Modeling
cascade:
  featured_image: '/images/word_similarities.png'
menu:
  main:
    weight: 6
---
## Word2Vec Modeling

By Dez Miller

Code for this article is available on Dez Miller’s Github: https://github.com/dezmediah/wordembeddings

## Background
Word2Vec is a Gensim word embedding algorithm that uses shallow, two-layer neural networks to place each word in a corpus within a vector space model. For digital humanists who use word embedding models, a word’s connotative meaning can be represented by the nearest neighbors to the seed word in vector space. These spatial relationships are determined by the context of a word across a particular corpus as well as by the context of related words. This
means, effectively, that even if “river” very rarely appears within the direct context of a particular word, for example “forest,” it may still be considered by the Word2Vec algorithm to be highly semantically close to the word “forest” as long as another closely related word, for example, “stream,” appears frequently in the context of “forest.”

The idea that the meaning of a word is represented well by its context has been explored by language theorists of the past several centuries. Two such examples are the maxim attributed to John Rupert Firth, “you shall know a word by the company it keeps!” and Jacques Derrida’s refutation, in Of Grammatology, of the structuralist idea of the signified, arguing that behind every signifier is a chain of signifiers which constitutes the meaning of the word.

A common operator with Word2Vec is getting cosine similarity results between two words. These results are, theoretically, both physically closer in vector space and semantically closer in meaning. 

## Models
Our project, conceived for DH 2023, was interested in how the Temple Sci-Fi corpus conceptualized various ecological concepts, in particular water, and how those associations compared to other corpora housed within the HathiTrust Digital Library. As a dataset in which proto climate-fiction (or cli-fi) dominated, we wanted to know whether water and water-related words would be more associated with pollution and toxicity than in a broader sci-fi corpus or in a broad literary fiction corpus.

Four Word2Vec models were produced, depicting word similarity for the following corpora: 
A) the Temple SF Corpus, housed within Hathi Trust
B) A subset of the Temple SF Corpus identified as being particularly water-focused through LDA Topic Modeling
C) Kimutis, Underwood, and Witte’s 1,501-Volume NovelTM Gender-Balanced Workset housed within the HathiTrust Digital Library
D) Thompson and Mimno’s 5,164-Volume SF Workset housed within the HathiTrust Digital Library

To visualize how water concepts related to toxicity concepts in a general way in these four corpora, the following seed words were chosen through a subjective process: 1) river, 2) water, 3) pollution, and 4) toxic. 

Following are two-dimensional graphs of the three-dimensional vector space for the seed words and their five most related words for Corpora A, C, and D. In these graphs, water and water-related words are blue, pollution and pollution-related words are red, toxic and toxicity-related words are yellow, and river and river-related words are gray.

![image](/images/NovelGB_chart.png)

![image](/images/Temple_word2vec_chart.png)

![image](/images/SF_word2vec_chart.png)

We wanted to know whether the TempleU SF Corpus, given the predominance of proto-cli-fi in it, would represent certain bodies of water as dirtier, more toxic, or more polluted than the comparison corpora. Following is a matrix with cosine similarity values between words representing bodies of water and those toxicity related words. This method is heuristic, given that within each corpus, words might be generally more or less related to one another. Therefore, the most useful comparisons are within each corpus rather than across corpora. 

![image](/images/word_similarities.png)

In combining this approach with close reading, we came to realize that competing narrative dynamics might be influencing these cosine similarity results. For example, we can see in the following quotes from Ursula K. Le Guin’s The Dispossessed (1974), which is in the TempleU SF Corpus and in the Mimno and Thompson comparison SF corpus, that water is discussed more positively (i.e. more in association with cleanliness or purity) in the context of a metaphor, and less positively (i.e. more in association with dirtiness, toxicity, and sewage) in the context of a world-building description. 

Water as metaphor: "His eyes were light, and the light from the window filled them so they seemed clear as water." (56)

Water in SF world-building: "The surface of Urras was five-sixths water. Even its deserts were deserts of ice, at the poles. No need to economize; no drought…  But what became of the shit? He brooded over this, kneeling by the stool after investigating its mechanism. They must filter it out of the water at a manure plant. There were seaside communities on Anarres that used such a system for reclamation. He intended to ask about this, but never got around to it." (64)

## Conclusions
Surprisingly, using our heuristic method of comparing the average cosine similarity values, the NovelTM GB corpus had higher average cosine similarity associations between water-related and toxicity-related words than did the broader Mimno/Thompson SF corpus or the Temple SF corpus. This ran counter to our hypothesis that given the predominance of proto cli-fi in the Temple SF corpus, there would be a particularly high association in the Temple SF Corpus between water-related words and toxicity-related words. Without fitting the vector spaces to each other, however, we were unable to say conclusively whether water-related words were more associated with toxicity-related words in particular corpora. A more accurate method of comparison could be used to determine whether this proves true. However, it did open up the possibility of an ecological streak within the NovelTM GB corpus that could be explored in future research.
	
Using an LDA and Bert Topic Modeling to Word2Vec pipeline proved a fruitful approach to narrowing in on sub-corpora that were rich with ecocritical thought with respect to water. A similar approach could be applied to the NovelTM GB corpus to determine sub-corpora relevant to a variety of ecocritical inquiries, whether they’re focused on water, forest, urban ecology, or other subject matter. By creating a sub-corpus of water-themed novels within the Temple Corpus we were able to begin to see how this proto cli-fi conceptualized water in relation to pollution and toxicity, particularly with regard to building worlds that featured water pollution. Further reading within this sub-corpus would be an interesting next step. While we also noted a high degree of cosine similarity between water-related and toxicity-related words for that sub-corpus, this may be influenced by a higher degree of relatedness overall between all words in the sub-corpus.

Given the difficulty of comparing values across corpora, we paid attention to similarity values within each corpus, and noted that within the TempleU SF Corpus and the Mimno/Thompson SF Corpus, oceans were depicted as more polluted, toxic, and associated with sewage than were lakes or rivers. We also compared similar words in each corpus, and found that while the most similar words to water and river in each corpus didn’t differ drastically in a thematic way, the words associated with pollution and toxicity were more revealing. The NovelTM GB corpus pollution/toxic words tended to have a moral connotation (corruption, filth, taint), whereas the Mimno/Thompson SF corpus showed a marked concern with nuclear activity, with words like fallout, depletion, shortages, and radioactivity. The Temple corpus also associated pollution/toxicity with nuclear activity, but in addition, it showed a concern with human-activity, like DNA and warfare. We thought this could speak to a possible association in the proto cli-fi of the Temple Corpus between human responsibility and pollutive activity. 

Altogether, while exploratory in nature, our methodology opened up possible pathways for narrowing in on environmental questions within particular genres and subgenres. The models opened up new questions for us around how ecological meaning is created within specific genres, and whether particular sub-corpora can have outsized impact on that meaning creation. Finally the fruitfulness of pairing this research with close reading was revealed in our reading of The Dispossessed, where we saw competing associations between water as pure in a metaphorical plane, and polluted when narrativized through science fiction worldbuilding.
