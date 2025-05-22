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
- Human activity recognition
- Smart home automation
- Customer segmentation
- Financial market analysis

##### Comparison between supervised and unsupervised for labelling

Supervised approach requires labels, which may have cost associated with it, debatable annotations, different worldviews bias.

Unsupervised doesn't have this due to having no label:
- No pre-assigned labels
- Discovers classes based on features
- Lets the composition of the data drive classification
- Useful when labels are expensive, annotators disagree, or there are different worldviews/unconscious biases

### Clustering

Groups data into sets, with respect to a given application e.g. topic analysis or human activity recognition.

Ensuring **high intra-class** similarity and **Low inter-class** similarity

The mental model for applying unsupervised approaches is similar to supervised approaches, with the key difference being that the algorithm identifies groups of similar texts without linking them to predefined classes.

### K-Means Clustering

Algorithm for clustering. Works by:

1. Place K points to be centroid, randomly across dimension graph e.g. K = 3
2. Calculate distance for point closest to centroid based on some distance calculation (Euclidean distance)
3. Move centroid to centre of all points
4. Repeat until position of each centroid is stalled.

More formally:
1. Randomly select centroids μ1 and μ2 for K=2
2. For each object in the dataset, estimate its distance from each centroid (μ1 and μ2) and link it to the cluster with nearest centroid (⍵1 or ⍵2)
3. Based on cluster allocation, re-estimate centroids
4. Re-allocated object with respect to new centroids; re-estimate centroids
5. Continue till no further movement or max iteration reached (stopping criteria)

Challenge comes from how many centroids to use.

- **Elbow Method**: Simply increments K and waits for average sum of node distances to plateau for all clusters (so defined groups possible found)
- **Silhouette Score** uses *cohesion* and *separation* to give score between 0 and 1. Between 0.5 and 1 is ideal.

### Dimensionality Reduction for Clustering

Necessary since with unsupervised ML:
1. Calculating distance from each document to each centroid for x iterations in topical analysis can be costly
2. Even short documents can have large feature space

Feature selection for unsupervised ML is similar to supervised ML:
- Words
- Filter stopwords
- Apply weighting

Does this via removing frequent words due to lack of informativeness, and applying Singular Value Decomposition (SVD)

##### Single Value Decomposition (SVD)

Reduces dimensionality to make clustering more efficient while maintaining useful information. SVD tries to distill and summarize the information contained in the original huge matrix down to much smaller dimensions (e.g., 30,000 to 300 dimensions).

Simplification via decomposition from one matrix to 3 smaller ones:
- When multiplying the 3, you get back the original
- First encodes m texts in terms of smaller k features (concepts, or latent factors)
- Second describes relations between the k concepts
- Third encodes the relation between the k concepts and the original n word features

Interpretation of SVD:
- Each original word represents its own dimension (separate column in original n dimensional matrix)
- Words might represent the same 'concept' so if merged into a single concept this would help reduce the word space
- m x k matrix is reduced document-by-latent factors matrix for k most salient factors
- k x k matrix encodes how latent factors correspond to each other
- k x n matrix tells you how to interpret the relations between factors and original words

### Evaluating Unsupervised ML Algorithms

Dependent on application domain but uses similar metrics to supervised learning:

- **Purity**: Similar to accuracy, range from 0 to 1. Assign class to each cluster based on majority of instances in cluster, then estimate accuracy by counting number of correctly assigned documents divided by total number of documents.
- **Homogeneity**: Similar to precision, measures extent to which each cluster contains only members of a single class.
- **Completeness**: Similar to recall, estimates extent to which all members of a class are assigned to same cluster.
- **V-measure**: Similar to F-measure, harmonic mean of homogeneity and completeness.

### Topic Modelling

It can be difficult to classify things; items might belong to multiple classifications or new classifications.

Topic modelling is a text-mining technique aiming to discover abstract topics from text. It relies on documents on a particular topic using a particular vocabulary. Unlike hard clustering, topic modelling assumes the presence of multiple topics per document, in different proportions.

This can use **Latent Dirichlet Allocation** (LDA) to detect multiple topics from the input of many text documents.

### Latent Dirichlet Allocation (LDA)

LDA was introduced by David M. Blei, Andrew Y. Ng, and Michael I. Jordan in 2003. It tackles the problem of modeling text corpora and other collections of discrete data with the goal of finding short descriptions of members of a collection to enable efficient processing of large collections while preserving statistical relationships.

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

The central computational problem for topic modelling is to use the observed documents to infer the hidden structure:
- Documents are observed
- Topics, per-document topic distributions, and the per-document per-word topic assignments are hidden structure

Algorithms have no information about the subjects of the documents. The articles are not labeled with the topics or keywords. Interpretable topic distributions arise by computing the hidden structure that most likely generated the observed documents.

#### Formal Definition of LDA

- β1:k are the topics where each βk is a distribution over the vocabulary
- Topic proportions for the dth document are θd, where θd,k is the topic proportion for topic k in document d
- z1:D are the topic assignments where zd,n is the topic assignment for the nth word in document d
- W1:D is the set of words where wd,n is the nth word in document d

LDA is part of a larger field of probabilistic modeling that treats data as arising from a generative process including hidden variables. The generative process defines a joint probability distribution over both the observed and hidden random variables.

In the plate notation for LDA:
- Each node is a random variable
- Hidden nodes (topic proportions, assignment, and topics) are unshaded
- Observed node (the words of the documents) is shaded
- Rectangles are the plate notation which denotes replication: N plate is the collection of words in the documents, D plate is the collection of documents


##### References
----
![[Unsupervised_learning.pdf]]