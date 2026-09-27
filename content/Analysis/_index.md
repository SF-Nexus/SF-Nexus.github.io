---
title: "Word Embeddings"
description: "Word2Vec models of water, pollution, and toxicity in climate fiction, compared across four corpora."
featured_image: '/images/word_similarities.png'
stage: analyze
---
*By Dez Miller*

Code for this study is on [Dez Miller's GitHub](https://github.com/dezmediah/wordembeddings). It was presented at DH2023, the conference of the Alliance of Digital Humanities Organizations, in Graz ([abstract](https://doi.org/10.5281/zenodo.10065276); [slides](https://zenodo.org/records/8107505)). Notebooks for running Word2Vec on the SF Nexus data are in our repository:

{{< notebook path="notebooks/Analyzing_Extracted_Features/Gensim Word2Vec (Jupyter Notebook).ipynb" title="Word2Vec with Gensim" >}}

{{< notebook path="notebooks/Analyzing_Extracted_Features/Advanced Word2Vec (Jupyter Notebook).ipynb" title="Advanced Word2Vec" >}}

{{< notebook path="notebooks/R_scripts/Word2Vec (R).R" title="Word2Vec in R" >}}

## Background

Word2Vec is a word embedding algorithm, implemented here in Gensim, that uses a shallow, two-layer neural network to place each word of a corpus in a vector space. For digital humanists who use word embeddings, a word's connotative meaning can be represented by its nearest neighbors in that space. These spatial relationships depend on a word's contexts across a particular corpus, and on the contexts of related words. So even if "river" rarely appears right next to "forest," Word2Vec may still place the two close together, as long as a closely related word such as "stream" often appears near "forest."

Language theorists have explored the idea that a word's meaning is represented by its contexts for a long time. Two examples are the maxim attributed to John Rupert Firth, "You shall know a word by the company it keeps!", and Jacques Derrida's argument in *Of Grammatology* against the structuralist idea of the signified: behind every signifier is a chain of signifiers that makes up the word's meaning.

A common Word2Vec operation is measuring the cosine similarity between two words. Words with high cosine similarity are, in theory, both closer in vector space and closer in meaning.

## Models

Our project, conceived for DH2023, involved myself, Alex Wermer-Colan, Megan Kane, and SaraGrace Stefan. We studied how the Temple SF corpus conceptualized ecological concepts, particularly water, and how those associations compared with other corpora in the HathiTrust Digital Library. Proto-climate fiction (or cli-fi) dominates Temple's dataset. We wanted to know whether water and water-related words would be more closely associated with pollution and toxicity there than in a broader SF corpus or a broad literary fiction corpus.

We built four Word2Vec models, one for each of these corpora:

* **A.** The Temple SF corpus, in HathiTrust
* **B.** A subset of the Temple SF corpus identified as especially water-focused through [LDA topic modeling](/models/#lda-topic-modeling)
* **C.** Underwood, Kimutis, and Witte's 1,501-volume gender-balanced workset from the [NovelTM Datasets for English-Language Fiction](https://doi.org/10.22148/001c.13147), in HathiTrust
* **D.** Thompson and Mimno's 5,164-volume science fiction workset, from their work on [finding speculative fiction in HathiTrust](https://github.com/laurejt/sf-in-hathitrust)

To see how water concepts related to toxicity concepts across the four corpora, we chose four seed words through a subjective process: *river*, *water*, *pollution*, and *toxic*.

The graphs below project the three-dimensional vector space into two dimensions. Each shows the seed words and their five most similar words for Corpora C, A, and D. Water and water-related words are blue, pollution and pollution-related words are red, toxic and toxicity-related words are yellow, and river and river-related words are gray.

![Word2Vec plot for the NovelTM gender-balanced corpus showing the seed words and their nearest neighbors, color-coded by seed word](/images/NovelGB_chart.png "Corpus C: the NovelTM gender-balanced workset.")

![Word2Vec plot for the Temple SF corpus showing the seed words and their nearest neighbors, color-coded by seed word](/images/Temple_word2vec_chart.png "Corpus A: the Temple SF corpus.")

![Word2Vec plot for the Thompson and Mimno SF workset showing the seed words and their nearest neighbors, color-coded by seed word](/images/SF_word2vec_chart.png "Corpus D: the Thompson and Mimno SF workset.")

We asked whether the Temple SF corpus, dominated by proto-cli-fi, would present certain bodies of water as dirtier, more toxic, or more polluted than the comparison corpora. Below is a matrix of cosine similarities between words for bodies of water and toxicity-related words. The method is heuristic: within each corpus, words may be generally more or less related to one another. So the most useful comparisons are within each corpus, not across corpora.

![A matrix of cosine similarity values between body-of-water words and toxicity-related words for each of the four corpora](/images/word_similarities.png "Cosine similarities between bodies of water and toxicity-related words, by corpus.")

Combining this approach with close reading, we realized that competing narrative dynamics might be shaping the cosine similarity results. Ursula K. Le Guin's *The Dispossessed* (1974) is in both the Temple SF corpus and the Thompson and Mimno SF corpus. In the passages below, water is described more positively (associated with cleanliness or purity) in a metaphor. It is described less positively (associated with dirt, toxicity, and sewage) in world-building description.

Water as metaphor:

> "His eyes were light, and the light from the window filled them so they seemed clear as water." (56)

Water in SF world-building:

> "The surface of Urras was five-sixths water. Even its deserts were deserts of ice, at the poles. No need to economize; no drought… But what became of the shit? He brooded over this, kneeling by the stool after investigating its mechanism. They must filter it out of the water at a manure plant. There were seaside communities on Anarres that used such a system for reclamation. He intended to ask about this, but never got around to it." (64)

## Conclusions

Surprisingly, by our heuristic of comparing average cosine similarity values, the NovelTM gender-balanced corpus showed higher average similarity between water-related and toxicity-related words than either the broader Thompson and Mimno SF corpus or the Temple SF corpus. This ran counter to our hypothesis that the predominance of proto-cli-fi in the Temple corpus would produce an especially strong association between water and toxicity there. Without aligning the vector spaces to one another, however, we could not say conclusively whether water-related words were more associated with toxicity-related words in any particular corpus. A more rigorous method of comparison could test this. The result did suggest an ecological streak in the NovelTM gender-balanced corpus that future research could explore.

A pipeline from LDA and BERTopic topic modeling to Word2Vec proved a fruitful way to narrow in on sub-corpora rich in ecocritical thought about water. The same approach could find sub-corpora in the NovelTM gender-balanced corpus for other ecocritical questions, whether about water, forests, urban ecology, or something else. Building a water-themed sub-corpus from the Temple corpus let us begin to see how this proto-cli-fi conceptualized water in relation to pollution and toxicity, especially in worlds built around water pollution. Reading further within this sub-corpus would be an interesting next step. We also noted high cosine similarity between water-related and toxicity-related words in that sub-corpus, though this may reflect a higher overall relatedness among all words in the sub-corpus.

Because values are hard to compare across corpora, we focused on similarity values within each corpus. Within both the Temple SF corpus and the Thompson and Mimno SF corpus, oceans were depicted as more polluted and toxic, and more associated with sewage, than lakes or rivers. We also compared the most similar words in each corpus. The words most similar to *water* and *river* did not differ much thematically between corpora, but the words associated with pollution and toxicity were more revealing:

* The NovelTM corpus's pollution and toxicity words tended to carry moral connotations: *corruption*, *filth*, *taint*.
* The Thompson and Mimno SF corpus showed a marked concern with nuclear activity: *fallout*, *depletion*, *shortages*, *radioactivity*.
* The Temple corpus also linked pollution and toxicity with nuclear activity, but it additionally showed a concern with human activity such as *DNA* and *warfare*. This could reflect an association, in the proto-cli-fi of the Temple corpus, between human responsibility and polluting activity.

Although exploratory, our methodology opened pathways for narrowing in on environmental questions within particular genres and subgenres. The models raised new questions about how ecological meaning is created within specific genres, and whether particular sub-corpora can have an outsized effect on that meaning. Finally, pairing this research with close reading proved fruitful. In *The Dispossessed* we found competing associations: water as pure on the metaphorical plane, and polluted when narrativized through science fiction world-building.
