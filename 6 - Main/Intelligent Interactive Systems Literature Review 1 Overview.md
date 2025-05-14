#### **Summary:**

Around 1500 word literature review going over an area of Artificial Intelligence and discussing issues caused by and solutions for biases.

Only consider data published from within the last 3 years.

We'll do: **Large Language Models** with a focus on handling "truthful" representations of real events. Especially when it comes to the context of censoring, controversial topics and historical accuracy.

Research Questions
- How accurately do LLM's reflect inherent human perspectives and of which cultures are more represented?
- How do LLM's attempt to give effective and reliable single answers for issues with various respected differing perspectives?

Structure:
- **Introduction**
- **Research Questions** 1-3 Research Questions which your paper will answer
- **Search Strategy** (detailing which literature database used, what search terms, what range of publication dates considered)
- **Summary of Research** (i.e. summarise the papers you've read organised in a sensible way, so the actual literature review) 
- **Conclusions**
- **References**

Title: **Fairness and Bias in Intelligent Interactive Systems**

With the explosive release of GPT-3 in 2021, LLM's have played a huge role in many sectors, including research, education, analysis, engineering, manufacturing amongst many others. It has become a big part in our lives but even early on, there was worry about how accurate and "honest" it is. If these models cannot be fully trusted, does relying on them pose a risk?

Controversies have appeared with Open AI not being open source as originally intended and hallucinations of AI making up fake information. More recently ,LLM's such as deep seek have allegedly censored controversial Chinese history, fear of censorship, propaganda and misinformation has increase. As a result, many have begun to ask for stricter standards for training data , greater feedback handling and requirements for AI-generated responses to include references and supporting evidence.

With this literature review, I wanted to explore bias in LLM through the context of social, historical accuracy. Specifically, the research questions:

**RQ 1**: How far do LLM's reflect human perspectives and of which cultures are more represented?
**RQ 2**: How do LLM's attempt to give effective and reliable single answers for issues with various respected differing perspectives?


Methodology (100 words):

### 2.1 Search Strategy

Search for reviews were carried out on multiple research databases, including Google Scholar, IEEE Xplore, and ACM Digital Library. The search terms used were:

- "Large Language Models" OR "LLM's"  AND "truthfulness"
- "Controversial topics" AND "bias in AI"
- "Historical accuracy" AND "machine learning" OR "training data"
- "Social" OR "Historical" OR "Censorship" AND "LLM's"

### 2.2 Inclusion and Exclusion Criteria

Inclusion Criteria:

- Peer-reviewed articles, conference papers, and quality white papers published within the last 3 years.
- Research studies that review bias, censorship, or historical accuracy in current day LLMs.
- Studies suggesting or testing mitigation approaches to enhance truthfulness and accuracy.

Exclusion Criteria:

- Research addressing broad AI ethics with no particular relevance to LLMs.
- Opinion or non-peer-reviewed pieces without empirical support.
- Papers or research theorising "future" of AI accuracy and performance.


---

Findings (700 words):

- A comprehensive overview and summary in relation to the findings of the literature review
- Break down into 2 sections in order answer both research questions
- Just going over what has been learnt, no further analysis then that

### Social and historical Bias in LLM

Many sources argue it's the training data itself that causes significant issue's with biases with LLM's. They are trained on decades and centuries worth of text and human information which inherently have social and historical prejudices which make it to the final model.  Just like traditional historical narratives that have primarily focused Western perspectives, LLMs replicate these dominant cultural perspectives.  According to Navigli, R (2023)[1] through a study,  it  found how different LLM models such as GPT and Bloom, when asking for stereotypes it found semantic relationships in which traits such as freedom for Americans, or "poor English" for Chinese people. Chu, Z (2024) [2] mentions significant disparities in datasets like IJB-A and Adience (popular image datasets for training) where predominantly light-skinned individuals make up 79.6% of the data , therefore underrepresenting dark-skinned groups. Navigli, R adds that dealing with this ratio over and under represented cultures is difficult do to excluding over-represented domain might remove high-quality information, but increasing under-represented data may be harder to find.

Expanding on more sensitive and significant areas is the issue of religion and gender, the biases of text in training data is more prominent. Prompts related to "Islam", "Muslims" and events related to them were found to have more negative connotations, of violence , with high correlations to terms such as "terrorist" (Abid, A,2021 [3]). In regards to gender, Kotek, H(2023)[4] identified that  men that were predominantly hired for technical and managerial positions while hiring women into ancillary or motherly responsibilities by recycling traditional gender biases. The most vivid example is the use of "her"/"she" for job opportunities such as secretary and nurse and "he" for professions such as doctor and in general, responses with men have much more varied occupations. All the while, the frequency of these responses do not align with real world statistics of women in workforce, indicating LLM results favour social biases then a accurate representation.


### Mitigation of Bias in LLM's


As opposed to google or traditional search engines, LLM's like GPT or Gemini typically only return 1 or 2 answers, as opposed to showing a wide list of sites that may answer your query. There are various strategies to combine these various viewpoints and answers to one comprehensive answer such as advanced prompt engineering. Simply put, LLM's will weigh heavily prompts given over training data, so detailed prompts with context of what it's for, give's more successful responses. In "Deus Ex Machina and Personas from Large Language Models" (2024) [5], for instance, researchers illustrate how "persona creation" techniques encourage the model to come up with more varied narratives instead of using generic answers by adding real statistics or specifically asking for non-US personas.

Standardization and diversification of training data is also important.  Lee, D. (2024)[6] explains that LLM's have to be trained on accurate and diverse data sets and relevant procedures to insure it's not propagating social inequalities. Trimming data sets that are comprised of a broad cross-section of viewpoints aids builders in levelling the impact of any single particular narrative. Recent models of LLM also have the options of referencing the exact sources used, again adding more trust worthiness, but also reducing the chance of hallucination. Tools such HILL by Leiser, F (2024)[7] help by being an addition on top of LLM's. HILL cross-verification with authentic sources of data is used to flag unsupported or unsubstantiated statements and enhance factualness of the output.

A simple but effective mitigation to bias is simply, creating your own LLM for your specified purpose via using any of the open source solutions such Deep seek and Alpaca. This allows for better and closer calibrations to training data and context, allowing it to better recognize and value regional linguistic and cultural variations (Dorn, R. 2024)[8]. This allows for more control on the "personality" of LLM's allowing it to stop making confident assertions where it is certain of it's answer.


Discusison 

Through the evidence, it's clear that despite the advances of LLM referencing sources for data, allowing you to provide wide ranges of documents and text yourself,  they still mirror human biases and promote misinformation. Regarding **RQ 1** and accurate representation of human perspectives, it's seen with LLM's, by virtue of their training on predominantly Western and historically skewed datasets, tend to replicate established cultural hierarchies. Navigli, R (2023)[1] and Chu, Z (2024) [2] demonstrate how it stems from the nature of the data and those who wrote it. Negative biases such as is found with religion and sexist prejudices are heavily weighed and most importantly, it's incredibly confident. Kotek, H(2023) [4] adds in the discussion of his paper "In general, in their current state, LLMs produce convincingly coherent text, which is often complex and conversational", which when combined with LLM's providing few responses and processing times for queries, people are quick to accept and move on. 

Although when it comes to **RQ 2** and how LLM's can come up with successful single answers for nuanced issues, some solutions include advanced prompt engineering, or simply just adding as much context as you need in order to get better and more accurate response. This helps to steer from it's default USA and stereotypical weighted responses. Additionally, rigorous data standardization and the integration of verification tools such as HILL (Leiser, F ,2024)[7] work well to ensure that the generated content is not only balanced but also factual. But again, it's important to know, these just reduce the likelihood of false responses, and even then, requires the end user to have higher standards for data they accept which can be difficult for unfamiliar areas in knowledge or simply wanting to deal with more manual and time expensive research.

The main channel comes down to, providers of popular LLM need to tackle the bias built into LLMs, which stems from the data they're trained on. That means creating more diverse and representative training sets, audits and transparency of how results are generated. Although there are many successful mitigation methods to reduce the chance of biases and inaccuracy, it's still has far too many issues to compare traditional research methods.


---
Conclusions (100 words):

This systematic review has shown how bias stemming from training data with biases inherently in their text are amplified in the final results, spreading both harmful and misleading information. This combined with hallucinations, confident responses and training data being invisible to end user further aid this misrepresentation. Although there are techniques such as advanced prompt engineering, standards for training data and recent LLM's showing references for results, the fundamental issue of accuracy is far from resolved, which makes our increasing reliance a point of consideration.



---
References:

[1] Navigli, R., Conia, S., & Ross, B. (2023). Biases in Large Language Models: Origins, Inventory, and Discussion. _J. Data and Information Quality_, _15_(2). https://doi.org/10.1145/3597307

[2] Chu, Z., Wang, Z., & Zhang, W. (2024). Fairness in Large Language Models: A Taxonomic Survey. _SIGKDD Explor. Newsl._, _26_(1), 34–48. https://doi.org/10.1145/3682112.3682117

[3] Abid, A., Farooqi, M., & Zou, J. (2021). Persistent Anti-Muslim Bias in Large Language Models. _Proceedings of the 2021 AAAI/ACM Conference on AI, Ethics, and Society_, 298–306. https://doi.org/10.1145/3461702.3462624

[4] Kotek, H., Dockum, R., & Sun, D. (2023). Gender bias and stereotypes in Large Language Models. _Proceedings of The ACM Collective Intelligence Conference_, 12–24. https://doi.org/10.1145/3582269.3615599

[5] Salminen, J., Liu, C., Pian, W., Chi, J., Häyhänen, E., & Jansen, B. J. (2024). Deus Ex Machina and Personas from Large Language Models: Investigating the Composition of AI-Generated Persona Descriptions. _Proceedings of the 2024 CHI Conference on Human Factors in Computing Systems_. https://doi.org/10.1145/3613904.3642036

[6] Lee, D., Todorova, C., & Dehghani, A. (2024). Ethical Risks and Future Direction in Building Trust for Large Language Models Application under the EU AI Act. _Proceedings of the 2024 Conference on Human Centred Artificial Intelligence - Education and Practice_, 41–46. https://doi.org/10.1145/3701268.3701272

[7] Leiser, F., Eckhardt, S., Leuthe, V., Knaeble, M., Mädche, A., Schwabe, G., & Sunyaev, A. (2024). HILL: A Hallucination Identifier for Large Language Models. _Proceedings of the 2024 CHI Conference on Human Factors in Computing Systems_. https://doi.org/10.1145/3613904.3642428

[8] Dorn, R., Kezar, L., Morstatter, F., & Lerman, K. (2024). Harmful Speech Detection by Language Models Exhibits Gender-Queer Dialect Bias. _Proceedings of the 4th ACM Conference on Equity and Access in Algorithms, Mechanisms, and Optimization_. https://doi.org/10.1145/3689904.3694704


