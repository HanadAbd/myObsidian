2025-05-08 16:32

Status:

Tags: [[Intelligence Interactive Systems]]

---
## Summary

##### Topics Included:
- Clustering
- Topic Analysis
- K-means Clustering
- Topic modelling with Latent Dirichlet Allocation (LDA)

### Unsupervised Learning

Learning patterns from datasets with no labels, so interpreting data sets. Within this, there is:

- **Clustering**: Algorithms to detect similar groups
- **Dimensionality Reduction**: Simplify the data without losing too much information

**Applications**:
- NLP
- Game AI
- Anomaly Detection
- Pattern recognition in images


##### Comparison between supervised and unsupervised for labelling

Supervised approach requires labels, which may have cost associated with it, debatable annotations, different worldviews bias.

Unsupervised doesn't have this due to having no label



### Clustering

Groups date into sets, with respect to a given application e.g. topic analysis or human activity recognition.

Insuring **high intra-class** similarity and **Low inter-class** similarity
### K-Means Clustering

Algorithm for clustering. Works by:

1. Place K points to be centroid, randomly across dimension graph e.g. K = 3
2. Calculate distance for point closest to centroid based on some distance calculation (Euclidean distance)
3. Move centroid to centre of all points
4. Repeat until position of each centroid is stalled.

Challenge comes from how many centroids to use.

- **Elbow Method**: Simply increments K and waits for average sum of node distances to plateau for all clusters (so defined groups possible found)
- **Silhouette Score** uses *cohesion* and *separation* to give score between 0 and 1. Between 0.5 and 1 is ideal.

### Dimensionality Reduction for Clustering

Necessary since with unsupervised ML:
1. Calculating distance from each dock to each centroid for x iterations in topical analysis can be costly
2. Even short documents can have large feature space

Feature selection for unsupervised ML is similar to supervised ML:
- Words
- Filter stop words
- Apply weighting

Does this via removing frequent words due to lack of informativeness, and applying Singular Value Decomposition (SVD)


##### Single Value Decomposition (SVD)

Reduces dimensionality to make clustering more efficient while maintain useful information. SVD tries to distil and summarize the information contained in the original huge matrix down to much smaller dimensions (e.g., 30,000 to 300 dimensions).

![[image-30.png|916x309]]

Done via decomposing 1 matrix into 3 smaller ones, and multiplying the 3 to get back the original.

Each original word represents its own dimension (separate column in original n dimensional matrix)
- Words might represent the same 'concept' so if merged into a single concept this would help reduce the word space
- m x k matrix is reduced document-by-latent factors matrix for k most salient factors
- k x k matrix encodes how latent factors correspond to each other
- k x n matrix tells you how to interpret the relations between factors and original words


### Evaluating Unsupervised ML Algorithms


Dependent on application domain but uses similar metrics to SL

- **Purity**: Similar to accuracy, range from 0 to 1. Assign class to each cluster based on majority of instances in cluster, then estimate accuracy by counting number of correctly assigned documents divided by total number of documents.
- **Homogeneity**: Similar to precision, measures extent to which each cluster contains only members of a single class.
- **Completeness**: Similar to recall, estimates extent to which all members of a class are assigned to same cluster.
- **V-measure**: Similar to F-measure, harmonic mean of homogeneity and completeness.


### Topic Modelling

It can be difficult to classify things; might belong to multiple classifications or new classifications.

 Topic modelling is a text-mining technique aiming to discover abstract topics from text. Unlike hard clustering, topic modelling assumes the presence of multiple topics per document, in different proportions. This can use **Latent Dirichlet Allocation** (LDA) to detect multiple topics from the input of many text documents.


### Latent Dirichlet Allocation (LDA)

Works by essentially going through each document, finding short descriptions of members of a collection e.g. finding as many topics are within by grouping them. All the while preserving statistical relationships.

It doesn't capture semantics, just reoccurring of words. First document is it's own topic, look at 2nd document, if similar to first, join send topic other wise new topic. Done for each document


LDA works as a generative process:

1. Imaginary random process by which the model assumes the documents arose or were created
2. Topic = distribution over fixed vocabulary
3. Model assumes that the topics are generated first, before the documents
4. For each document in collection:
   - Randomly choose a distribution over topics
   - For each word in the document:
     - Randomly choose a topic from the distribution over topics
     - Randomly choose a word from the corresponding distribution over the vocabulary

This model reflects the intuition that:
- Documents exhibit multiple topics
- Each document exhibits the topics in different proportions
- Each word in each document is drawn from one of the topics
- Selected topic is chosen from the per-document distribution over topics

LDA gets its name from the per-document topic distribution that is called the Dirichlet distribution. In the generative process for LDA, the Dirichlet is used to allocate the words of the document.

#### Hidden Structures in LDA

The central problem for topic modelling is to use the observed documents to infer the hidden structure. It is unlabelled and algorithms have no information about subjects of documents, with topics and keywords with topic distributions arising by computing hidden structure.
#### Formal Definition of LDA

LDA is part of a larger field of probabilistic modelling that treats data as arising from a generative process including hidden variables. The generative process defines a joint probability distribution over both the observed and hidden random variables.


##### References
----
![[Unsupervised_learning.pdf]]