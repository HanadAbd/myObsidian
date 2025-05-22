2025-05-19 16:21

**Status:**  
- [x] Draft  
- [ ] Reviewed  
- [ ] Mastered

Tags: [[Intelligence Interactive Systems]]

---
# Summary


## List of Topics:

- Bayesian Reasoning
- Markov Chain
- Markov Decision Processes
- Bellman Equation
- Applications of MDP Processing

---

## 📝 Notes

### Probabilistic Representations

**Bayesian Reasoning** is about how statistics is represented in order to be accurate e.g. 20% of being positive of a disease.

Used along side Bayes law:

Debate around using **Natural Frequencies** instead e.g. "2 in 1000 people" is usually preferred to typical probability to present info


### Markov Chains and Markov Decision Processing

Both are used to define problems, where Markov chains is where states are dependent on the last state to model sequence of states.

Markov decision processing expands this with **actions** in order to define problems further as:

- **S** set of **States**
- **A** set of **Actions**
- **State transition function**: $P(s′| s, a)$ is where s' is new state, 
- Scalar **reward** received depending on transition. $r = R(s',s)$

**Optimal Policy** (Path or set of transitions) is defined as $\pi*$ is the goal.

**Bellman Equation** is used to derive value of a decision problem in terms of sum of all next rewards. Essential in reinforcement learning.

![[image-25.png]]


Algorithms used in are:

- **Value Iteration**: Set of all values, propagating all nodes till settling. Expensive and inefficient for larger problems.
- **Q-Learning**:
- **Reinforcement Learning**:
### Applications of MDP Based Solutions

Different Scenarios for Application of MDP based solutions

- **Success of Liver Transport**: Measuring success of splitting and giving liver. Very complex, with their being many states/classes for livers, and different perspectives on rewards. Ultimately, not successful due to not enough data.
- **South Korean Diabetic Medicine**: For recommending diabetes treatment, balancing rewards of quality of life, vs quantity. 

Both are examples if IIS helping with decisions for health care.


Also more specific situational awareness examples:

- **Piloting Eye sight**: In order to make pilots pay attention to correct sensors/readings, a dataset of measured eye movement is used to determine what they should be looking at.

##### Glossary


##### Questions & Clarifications (Things left to Complete if not in draft)

- How does Bellman equation work?
- How does MDP work and look like, with a worked example?
- Full explanation of Value iteration
- Flesh out notes regarding 2 MDP based medical examples.

##### Action Items
- [ ] Complete Draft 
- [ ] Create Flash Cards

##### References
----

Bayes Natural Frequencies


![[Bayes_Natural Frequencies.pdf]]


MDP


![[MDP.pdf]]


MDP Application 1


![[MDP Applications.pdf]]


MDP Application 2


![[MDP Applications 2.pdf]]