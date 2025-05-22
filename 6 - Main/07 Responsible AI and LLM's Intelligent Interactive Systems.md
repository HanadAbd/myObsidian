2025-05-20 13:35

**Status:**  
- [x] Draft  
- [x] Reviewed  
- [ ] Mastered

Tags: [[Intelligence Interactive Systems]]

---
# Summary

**Responsible AI** is the process of making AI reliable and trustworthy, via increasing transparency of results, minimising bias, ensuring fairness, and reducing variations for the same input. Bias can can occur due to historical text having biases from in them base on nation, time, location or social context text is from.

## List of Topics:

- Responsible AI
- History of LLM from Neural Networks and Transformers to modern day LLM
- Limitations of LLM

---

## 📝 Notes

### LLM History and Explanation

**Large Language Models** like ChatGPT or Llama typically work via word embeddings and word vector spaces in order to predict the next likely word e.g. "I want to eat" is probably followed by food

LLM's have become the face of AI, with neural networks and transformers being the most common technology now. They had a dramatic increase performance and parameters in the 2020s to today.

LLM' have the **limitations** of:

- **Bias and fairness**:
- **Transparency** of how it get's results
- **Robustness and Reliability**
- **Environment Welfare** (Incredibly energy inefficient)
- **Machine Requirements**, requiring powerful machines with powerful GPU's

### Responsible AI

Responsible AI (RAI) is the practice of making AI handle limitations to ensure trust and reliability.
It's necessary to handle the various issues that can arise with LLM such as:

- **Hallucinations** or just making shit up without confirming.
- **Forgetting over time** (especially and issue for longer chats or if you want them to more carefully consider older content)
- **Prompt injection** to create malicious responses from LLM (such as "Do Anything Now" or DAN)
- **Different outputs for the same input**, which is incredibly unreliable and causes difficulty in tracing the results.

### Bias

**Responsible AI** must also consider Bias, or the "*unequal treatment of a specific person or group*", which can amplify or worsen inequalities, perpetuate stereo types etc.

Derived from historical test in training data

In LLM training, Bias is mitigated via:

- Pre-Processing to modify/transform data
- Manipulating outputs of a trained model
- Modify learning mechanism to incorporate constraint

### Changes to make LLM Output Better

- **Prompt- engineering**, or the changing of prompts before being passed to AI (perhaps via another layer of AI's)
- **Reinforcement Learning Human Feedback (RLHF)** or testing output with human testers (Very Expensive and Time Consuming)
- **Pre-Process training data** to remove unnecessary data

##### Glossary


##### Questions & Clarifications (Things left to Complete if not in draft)



##### Action Items
- [x] Complete Draft 
- [ ] Complete Specification
- [ ] Make Flash Cards

##### References
----


![[Responsible_AI_LLMs 1.pdf]]