2025-05-19 16:17

**Status:**  
- [x] Draft  
- [ ] Reviewed  
- [ ] Mastered

Tags:

---
# Summary


## List of Topics:

- Reinforcement  Learning
- Markov Decision Process
- Static Value and Q-Value
- Bellman Equation
- Q-Learning Algorithm
- Q-Learning 

---

## 📝 Notes

### Reinforcement Learning

**Reinforcement learning** is where an agent (ML system) learns to make decisions by interacting with environment using actions to maximise rewards. Useful for complex, uncertain and dynamic environments e.g. autonomous vehicle ,stock market and Healthcare domain.

Applied for:
- Games
- NLP
- Finance


Works via **Agents** and **Environments** which interact with each other. With agent using actions to interact with environment, causing change is state and gaining reward.

**Environment** is adaptive problems space with attributes, boundaries etc.
**Agents** use unlabelled data, using experience and environment to maximise rewards.

### Markov Decision Process

Markov Decision Process (MDP) is technique to describe Regression Learning problems. Comprised of:

- Set S of States
- Set A of Actions
- Initial State S0
- Transition Model P(s,a,s')
- Reward Function (and discount $\gamma$)


Policies $\pi$ are what's used to define "path" or process used to interact with environment. Optimal polices maximise reward

Rewards Can either be **additive** rewards, which is sum of all rewards, or **discounted** rewards: that add a fall of constant called "discount" that decrease longer sequences, so favour shorter sequences, and immediate goals.

### Static value and Q-value

**Static Value Function** $V\pi (s)$ estimates sum of reward from state S onwards for given $\pi$

**State Action Value** $Q\pi (s,a)$ Function estimates sum of reward by taking action A in state S following a given $\pi$

### Bellman Equation

Bellman Equation (V(S)) calculates value at given state
$$V(s) = max[R(s,a) + \gamma V(s')]$$
$V(s)$ is the estimated cost for state
$R(s,a)$ is reward at S by performing action A
$\gamma$ is discount factor
$V(s')$ is value at previous state


### Q-Learning Algorithm

**Q-Learning** or **Quality Learning** is an algorithm that will find the best series of A for given S. It is:

- **Model-Free**: Doesn't require knowledge of undelaying dynamics or transition probabilities of environment
- **Value-based**: Focuses on learning value function Q(s,a) to estimate sum reward taking action A in state S following optimal policy.
- **Off-Policy**: Updates it's Q-values using data followed by different policy, typically exploratory ones.
$$Q(s,a) = r(s,a) + \gamma maxQ(s',a)$$


![[image-28.png]]


Q-Learning algorithm works via:

1. For each s, a initialize the table entry. (s, a) to zero.
2. Observe the current state s 
3. Do forever: 
	1. Select an action a and execute it
	2. Receive immediate reward r
	3. Observe the new state s'
	4. Update the table entry for (s, a) as follows

### Q-Learning Worked example




##### Glossary

- **Agents**: Value 
- State Function:
- 
##### Questions & Clarifications (Things left to Complete if not in draft)

1. 

##### Action Items
- [ ] Complete Draft 

##### References
----

![[Reinforcement-Learning.pdf]]