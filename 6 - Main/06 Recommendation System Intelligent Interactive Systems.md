2025-05-20 16:38

**Status:**  
- [x] Draft  
- [ ] Reviewed  
- [ ] Mastered

Tags:

---
# Summary


## List of Topics:

- Collaborative Filtering
- User based Collaborative Filtering
- Item based Collaborative Filtering
- Content Based Recommendation

---

## 📝 Notes


### Recommendation Systems

**Recommendation systems** are systems that filter information base on user or item, predicting user interest. Help's user *discover* and *make decisions*. Effectiveness or Success criteria is based on application domain and purpose.
Like functions, take user/item data as context, to return items, relevance score, ranking.

Inputs types based on different types of recommender systems can include:
- **Personal user information**
- **Product features** or information regarding item itself
- **Community Data** or collected information from relevant neighbours.
- **Knowledge Model** or information based on domain and what is needed

Applied in:
- Sales
- Personalisation
- Provide recommendations for items
- Minimise information overload

Perspectives on Recommendations Systems and it's success criteria can vary:

- **Retrieval Perspectives** - User get's what they are looking for
- **Recommendation Perspective** - User did not know and is looking for item
- **Prediction Perspective** - Predict what extent user would like an item
- **Interactive Perspective** -  Increase user interaction of recommendation systems
- **Conversion Perspective** -  Making user take the action to get item, optimising Sales

Ideally want **Long Tail**, where with more information, can recommend less popular items.

![[image-26.png]]

### Collaborative Filtering

Collaborative Filtering (CF) is a common approach for recommendation systems, using:
- Past experience of crowd
- User's explicit and implicit rating (So direct ratings like comments and reviews or implicit rating like watch time)
- **Item-based**: Users will like similar items in the future as they have in the past
- **User-based**: Users with similar preferences will like similar items 

CF has issues regarding:
- **Cold Start Problem**: No past information for new users and items
- **Data Sparsity**: User interacted with small fraction of available items, so repeat recommendations.
- **Scalability**: Computationally expensive with more users and items
- **Popularity Bias**: Only recommends most popular items
- **Demographic Bias**: Recommendations biased to certain groups
- **Rating**: User's less likely to do explicit rating, and implicit can be misinterpreted e.g. buying item as a gift for someone else, or somebody else is logged in.

Main approaches to CF are **user-based** or **item-based**.
##### User Based Collaborative Filtering

User's with similar preferences will prefer similar items. Use's set of near neighbours who've liked same items as A and liked item I, using average to weigh prediction of A like I.

Requires:
- Measuring similarities/correlations between users: Done via Pearson correlation function that takes differences in rating behaviour which works well in usual domains
- How many neighbours to choose (e.g. Top 100)
- Generate prediction from neighbour rating: Done via common prediction function


##### Item-Based Collaborative Filtering

User's who like similar items in the past, will like similar items in future.

Uses Cosine similarity for similarity and and average, as well as the same common prediction function .
### Content Based Recommendation

Expansion to CF methods, that adds **context** information about user and item, such as **content** of item and what user likes. Content Based (CB) techniques typically used for text documents.

Use's a matrix of attributes for both user and items

Term Frequency and Inverse Document frequency (TF-IDF) measures frequency of words in text and measure importance across text, in order select most relevant information.

TF uses Count frequency of terms, and IDF

![[image-27.png]]

Limitations to CB Recommendation Methods:
- Ramp up phase required
- More of the same
- Keywords done might not be good enough to cover com

##### Optimisations for Content Based Recommendation

Different ways to improve the vector space model are:
- Removing meaningless words
- Use stemming e.g. just "go" instead of "going" "gone" etc. to simplify vector space
- Size cutoff, e.g. only top 100 frequency words
- Lexical knowledge (or knowledge surrounding domain and terms.)

### Current Trends

Current trends for recommended systems include a greater focus in personalisation, more transparent and explainable AI as well as context aware recommendations that consider location, time and social context



##### Glossary

##### Questions & Clarifications (Things left to Complete if not in draft)

1. Explain more common prediction function
2. 

##### Action Items
- [ ] Complete Draft 

##### References
----
![[Recommender_Systems.pdf]]