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

Does this via removing frequent words, and applying singular Value Decomposition (SVD)

##### Single Value Decomposition (SVD)

Reduces dimensionality to make clustering more efficient while maintain useful information

### Evaluating Unsupervised ML Algorithms


Dependent on application domain but uses similar metrics to SL

- Purity is similar to accuracy
- Homgeneity, simlar to precesiosn
- Completeness, similar to recall, 
- V-measure, similar to F-measure, harmonic mean of homogeneity and completeness


### Topic Modelling

It can be difficult to classify things; might belong to multiple classifications or new classifications.

 Topic modelling is a text-mining technique aiming to discover abstract topics from text. This can use **Latent Dirichlet Allocation** (LDA) to detect multiple topics from the input of many text documents.


### Latent Dirichlet Allocation (LDA)

Works by essentially going through each document, 



##### References
----
![[Unsupervised_learning.pdf]]