# pyLDAVis User Guide (DRAFT)

This report represents a short summary of the theory and implementation of pyLDAvis, along with guidelines for using it in WE1S topic model interpretation.

pyLDAvis is the Python implementation of LDAvis, originally written in R. The published paper on LDAvis is Carson Sievert and Kenneth E. Shirley, ["LDAvis: A method for visualizing and interpreting topics"](https://nlp.stanford.edu/events/illvi2014/papers/sievert-illvi2014.pdf), presented at the 2014 ACL Workshop on Interactive Language Learning, Visualization, and Interfaces. The [code and documentation](https://github.com/bmabey/pyLDAvis) for pyLDAvis is available on GitHub.

## The Basic Theory of LDAVis

A topic in LDA typically consists of thousands of terms in the vocabulary of the corpus. To interpret a topic, one typically examines a ranked list of the most probable (highly-weighted) terms in that topic. The problem with interpreting topics this way is that common terms in the corpus often appear near the top of such lists for multiple topics, making it hard to differentiate the meanings of these topics. Ranking terms _purely_ by their probability (weight) under a topic is suboptimal for interpretation of the topic. Interpretation of a topic is improved by knowing the "relevance" of a term to a topic. This allows us to better answer three questions:

1. What is the meaning of each topic?
2. How prevalent is each topic in the corpus?
3. How do the topics in the corpus relate to each other?

## The Visualisation

The left panel answers questions 2 and 3 by plotting the topics as circles in the two-dimensional plane whose centers are determined by computing the distance between topics. Multidimensional scaling is used to project the intertopic distances onto two dimensions. Each topic’s overall prevalence is encoded in the areas of the circles.

Question 1 is addressed in the right panel, which depicts a barchart representing the individual terms that are the most useful for interpreting the currently selected topic on the left. A pair of overlaid bars represent both the corpus-wide frequency of a given term as well as the frequency of the term within the topic.

The left and right panels of the visualization are linked such that selecting a topic on the left reveals the most useful terms for interpreting the selected topic on the right. In addition, selecting a term on the right reveals the conditional distribution over topics on the left for the selected term. A weakness of the visualisation is that only the top 30 terms can be examined at a time. This weakness is partially addressed in the notes below.

## Adjusting the Relevance of Terms to Topics

Taddy (2011) proposed "lift", defined as the ratio of a term’s probability within a topic to its marginal probability across the entire corpus, as a way to (generally) decrease the rankings of globally frequent terms. However, this can generate noise by giving high rankings to very rare terms that occur in only a single topic, which can make the topic difficult to interpret. Bischof and Airoldi (2012) proposed using both a term’s frequency and as its exclusivity – the degree to which its occurrences are limited to only a few topics. LDAvis uses a similar method that is a weighted average of the logarithms of a term’s probability and its lift.

LDAvis defines the relevance of a term to a topic given a weight parameter λ, where λ determines the weight given to the probability of the term within the topic relative to its lift. (Both are measured on the log scale). Setting λ = 1 results in the familiar ranking of terms in decreasing order of their topic-specific probability. Terms should be listed in the same order as in dfr-browser. Setting λ = 0 ranks terms solely by their lift. LDAvis allows you to set λ to whatever value is “optimal” for topic interpretation.

It follows that a topic that is difficult to interpret based on probability alone (the default Mallet term ranking) may become more interpretable if the λ bar is adjusted to bring more "relevant" terms to the top of the ranking list.

## Best Practices for Interpretation

These have yet to be established by the project, but some general guidelines are worth noting.

1. An "interesting" topic in dfr-browser may be easier to interpret or label by examining the more "relevant", rather than the more "probable" terms in the topic. Switching to pyLDAvis to examine the topic with different λ settings may be useful in learning more about the topic.
2. Selecting individual terms in the topic will reveal other topics where that term is highly relevant. This is an alternative approach to the display of other topics where the term is highly weighted in dfr-browser.
3. Overlapping topics, or topics in the same quadrant on the left side of the pyLDAvis, can show topics that are closely related. Observing clusters of topics may help to identify split or merged topics that would potentially suggest re-running the model with a different number of topics. It may also suggest topics that should be related in any application based on an interpretation of the model.

## Notes

1. By default, pyLDAvis sorts topics in decreasing order of prevalence. The WE1S workflow disables sorting so that topic ids are consistent between all tools.
1. In the Workspace, the Jupyter notebook calls `scripts/pyldavis/pyldavis.py` to do most of the work. Within `pyldavis.py`, it is possible to change the `R=30` parameter to adjust the number of terms displayed. The documentation recommends no more than `R=50`.
1. In `pyldavis.py`, it is possible to change the parameters to adjust the intertopic distance measurement and multidimensional scaling algorithms. In the R implementation, it is possible to apply k-means clustering to the topics, but this function does not appear to be available in pyLDAvis.
1. It would be extremely useful to be able to export topic terms ranks based on a λ configuration less than 1. This would allow for import into other tools like dfr-browser and topic bubbles. However, I believe that dynamic term ranking is calculated by D3 in the browser. It may be possible to configure pyLDAvis with a starting λ value. pyLDAvis does possess a `save_json()` function to save data in json format, but I have not inspected to see what data is available.
1. pyLDAvis also has an `enable_notebook()` function to display visualisations inline in Jupyter notebooks. Because the visualisation benefits from the full screen, I am not sure if we would ever want to implement this display.
