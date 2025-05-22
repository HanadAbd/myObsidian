2025-05-21 19:59

**Status:**  
- [ ] Draft  
- [ ] Reviewed  
- [ ] Mastered

Tags: [[Intelligence Interactive Systems]]

---

## New Questions
---




## All Questions Before
---
**2023/24**
### **Question 1** 

**(a)**  
Consider an AI chatbot that provides medical advice on a particular disease. The probability that a person has the disease is 1%. If a person has the disease, the standard test for detecting it is correct 80% of the time. If a person does not have the disease, the probability that they nevertheless test positive is 9% (false-positive rate). A patient tests positive and seeks advice from the chatbot. Briefly discuss what advice the chatbot should give and justify your answer.

**[10 marks]**

**(b)**  
Now consider a chatbot designed for financial advising, where users are presented with choices about investments with varying levels of risk and potential returns. How might Prospect Theory be used to shape the behaviour of the chatbot. In your answer introduce and define the following terms: loss aversion and reference dependence. Illustrate your answer with specific examples of how the chatbot could influence user decisions based on the framing of its advice.

**[10 marks]**

---

### **Question 2**

**(a)**  
What is the Bellman equation? Explain the meaning of each term in the equation.
**[5 marks]**

**(b)**  
Discuss the challenges one might face while implementing Q-learning in a chatbot designed for handling customer service for an online retailer. Consider aspects such as state space size, defining rewards, and ensuring the chatbot can handle a wide range of customer interactions effectively. How can these challenges impact the learning process and the quality of the chatbot’s responses?
**[10 marks]**

**(c)**  
Consider the issues regarding chatbots handling user data to ensure privacy? What ethical considerations should be taken into account when storing and processing user interactions?
**[5 marks]**

---

### **Question 3**

**(a)**  
Consider an autonomous robot which is used to deliver cooked food in a busy city. The robot has to navigate and interact with other road users – for example, in knowing when to give way to or proceed when encountering a pedestrian. Provide a game theoretic analysis of what should be the appropriate policy of the robot. As part of your answer, provide a payoff matrix and comment briefly on whether your game theoretic analysis adequately captures the relevant issues.

**(b)** 

Consider a Movie Recommender System which uses Latent Dirichlet Allocation (LDA). What is meant by calling LDA a generative method? Explain how LDA can be applied to analyze the movie descriptions and reviews to discover latent top- ics. As part of your answer, describe how the topics discovered by LDA could be used to generate personalized movie recommendations for users. 
**[10 marks]**

-----
**2022/23**
### **Question 1**

**(a)**

What are Markov Decision Processes (MDPs)? Illustrate your answer with an example of your own invention.  
[6 marks]

**(b)**

Propose MDP-based recommender systems for one or more healthcare interventions. Describe each element of the MDP definition. Describe how the parameters of the model could be determined and how it can be tested?  
[6 marks]

**(c)**

What are the pros and cons of MDP-based recommendation? How could it improve healthcare? What are the risks?  
[8 marks]

---

### **Question 2**

**(a)**

What are the assumptions behind a Bayesian Spam Filter?  
[6 marks]

**(b)**

Illustrate a Bayesian Spam Filter using example messages/words and natural frequencies.  
[6 marks]

**(c)**

Critically analyse the role of decision theory in labelling a message as spam?  
[8 marks]

---

### **Question 3**

**(a)**

Describe two ways in which sensorimotor noise affects how people interact with computers?  
[6 marks]

**(b)**

Propose an intelligent system that models the consequences of human sensorimotor noise and uses this model to predict behaviour in pointing tasks.  
[6 marks]

**(c)**

Critically analyse the role of models of humans in intelligent interaction.  
[8 marks]

**Summer 2024**
### **Question 1 (Social Housing Case Study)**

Social housing is the provision of rental housing provided by local government (or non- profit organisations) to families who may struggle to afford rents available from the private market. A social housing company wishes to use AI to improve its service provision and ensure costs are kept as low as possible.

**(a)**

Consider the use of a Large Language Model chatbot for dealing with customer queries and complaints. Propose a possible application for the chatbot for social housing. Discuss briefly if there are any risks in terms of bias. If any risks are identified – what steps could be taken to mitigate these?  
[10 marks]

**(b)**

Consider the use of Computer Vision to monitor the occupancy of the houses and thereby control energy usage. Discuss whether this is a good idea. What risks are there? For any risk – discuss whether there is a mitigation.  
[10 marks]

---

### **Question 2 (Rock, Paper, Scissors & Prospect Theory)**

In the popular game called Rock, Paper, Scissors, each of the two players’ objectives is to choose the option, out of rock, paper, and scissors, that beats his opponent’s option, rock beating scissors, paper beating rock, and scissors beating paper.

**(a)**

Draw a payoff matrix for playing Rock, Paper, Scissors. Identify any Nash equilibria which exist. If no Nash equilibria exists, briefly explain why not.  
[5 marks]

Imagine a scenario where a cooperative AI, in the form of a chatbot, is designed to assist users in making investment decisions. The chatbot’s algorithm integrates Prospect Theory to better predict and influence user decisions under uncertainty.

**(b)**

Describe how the chatbot might utilize Prospect Theory to influence users’ investment choices. Provide an example of how it could frame investment options to either minimize loss aversion or exploit it to guide users towards more rational long-term investment strategies. As part of your answer describe what is meant by loss aversion.  
[10 marks]

**(c)**

Evaluate the ethical considerations of implementing Prospect Theory within the AI’s decision-making framework. Discuss the potential benefits and risks associated with this approach, especially in terms of user autonomy and decision-making quality.  
[5 marks]

---

### **Question 3 (Cyberbullying Detection)**

You are a part of a big social media company, and your task is to detect cyberbullying messages based on the text they contain. You have access to a large number of messages, which have been manually labelled as “OK” and “bullying”

**(a)**

How can you apply a CNN classifier to the task and evaluate it? Describe the approach, including how you would estimate the model parameters.  
[5 marks]

**(b)**

You decide to use precision and recall instead of accuracy as the evaluation metric for this task. Why does this decision make sense, and how are the metrics calculated?  
[5 marks]

**(c)**

The company decided to hire more human annotators to re-label your training data. Why might this be a good idea, and do you think this would improve your classifier in any way?  
[5 marks]

**(d)**

Due to repeated media coverage of cyberbullying, your company introduces a new policy stating that as many cyberbullying messages as possible are to be found and deleted, while still making sure the number of non-filtered messages remains high. Some additional manual labour is made available for this change. How does this affect your evaluation strategy, and how can you adapt the classifier to comply better with the new strategy? (Tip: a development corpus could be of use.)  
[5 marks]

---

### **Question 4 (Autonomous Vehicles & Reinforcement Learning)**

You work as AI researcher at an autonomous vehicle company, and your task is to develop a reinforcement learning algorithm for safe and efficient navigation of self-driving car. Your goal is to design an intelligent agent that has an ability to navigate through complex urban environments while following traffic rules and minimizing travel time.

**(a)**

Discuss the components of the reinforcement learning problem in the context of autonomous driving and formulize the problem with the help of Markov Decision process.  
[10 marks]

**(b)**

Outline the training process of the intelligent agent to learn optimal policy, and discuss how you will collect historical data, pre-process it and update the agent policy using a suitable reinforcement learning algorithm. As part of your answer, discuss the potential challenges during the training process.  
[10 marks]

### Essay Question

AI-powered recruitment tools are increasingly used by employers to screen résumés, assess candidates, and predict job performance. While these systems promise efficiency and objectivity, they also raise significant ethical concerns.

**Task:** Critically analyze the ethical implications of using AI in recruitment. In your response, discuss:

1. The privacy concerns surrounding the collection and use of candidate data.
2. How algorithmic bias might impact hiring decisions and workplace diversity.
3. Whether AI-based hiring tools could mitigate or exacerbate existing inequalities in employment.
4. The tension between automated decision-making and human oversight in recruitment.
5. Possible safeguards or regulatory approaches to ensure fair and ethical use of AI in hiring.

Your response should demonstrate clear argumentation, ethical reasoning, and real-world examples where applicable.  
**[15 Marks]**