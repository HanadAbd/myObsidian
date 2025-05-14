2025-05-08 16:31

Status:

Tags: [[Intelligence Interactive Systems]]

---

## Summary

AI in the case of prediction and planning, in order to aid human decision. It focuses on how humans make decisions versus mathematical models of rationality, and the implications for AI systems designed to assist human decision making.

### Computational Strengths vs. Human Decision Making

**AI has:**
- Mathematical statistics
- Access to a wide range of knowledge sources

**Where as humans:**
- Trust
- Bias
- Empathy
- Human understanding

### Mathematical Representations of Risk

Expected Value calculates the average outcome of a decision involving uncertainty by summing the products of each possible outcome and its probability.

$$\text{EV}(X) = \sum_{i=1}^{n} p_i x_i$$

(Subjective) Expected Utility accounts for subjective value (utility) that people place on outcomes, 

$$ \text{EU}(X) = \sum_{i=1}^{n} p_i U(x_i) $$

with utility function taking the form:
$$ U(x) = x^a $$
where 0 < a < 1, representing diminishing returns, joy and willingness to gain decreasing with more value.

Subjective expected utility (SEU) expands this 1 step further by considering subjective judgement of probabilities of individual.

$$ \text{SEU}(X) = \sum_{i=1}^{n} s_i U(x_i) $$


#### Axiomatic Foundations of SEU()

Axioms used to define.

1. **Completeness**: Preferences over uncertain outcomes are complete
2. **Transitivity**: If A is preferred to B and B is preferred to C, then A must be preferred to C
3. **Independence**: Preferences should not depend on irrelevant outcomes
4. **Continuity**: Preferences can be represented by a continuous utility function
5. **Monotonicity**: Adding a preferred outcome to a lottery makes that lottery more desirable
6. **Sure-Thing Principle**: If an outcome is preferred in one context, it should be preferred in all contexts regardless of probability differences
### Paradoxes Exploring Human Risk

Especially with regards to Economics, many paradoxes and games have been created to explore human's relation to risk.

- **St Petersburg Paradox or coin game** doubles pot with each coin toss starting from 1, but lose everything if you get head. You can track coin toss, to see where people starting opting out. Demonstrates inadequacy of expected value for decision-making.
- **Maurice Allais Paradox** illustrates violates the expected utility theory's axioms. With users ignoring small chance of receiving nothing for high chance of gaining significantly more.
  
### Factors Affecting Human Decision Making

People overweight outcomes that are considered certain, relative to outcomes which are merely probable.

Humans are not rational decision Making, and therefore, AI must account for our biases. Prospect Theory offers a descriptive model of decision making under risk.

- **Point of Reference** of agents is important, to see how see how important gain or loss is to them, in relation to what they already have
- **Certainty of risk** is preferred, even in the case of risk being small to great reward.
- **Endowment Effect** of people valuing things more just because they own them.
- **Framing Effect** or simply framing loss or gain in different manner to change perspective regarding that (80% fat free vs 20% fat).
- **Loss Aversion** or more pain from loss then joy of gain, for same amount.

### The Fourfold Pattern of Risk Attitudes

Prospect Theory predicts:
- **Risk aversion for gains of moderate to high probability**
- **Risk seeking for losses of moderate to high probability**
- **Risk seeking for gains of low probability**
- **Risk aversion for losses of low probability**

### Implications for AI Decision Making

Humans are not mathematically rational decision makers. If we want AI to make decisions for us or assist in our decision-making, AI systems need to account for our biases and decision-making patterns.

This creates challenges for designing AI systems that:
1. Make recommendations aligned with human preferences
2. Present information in ways that don't exploit human biases
3. Help humans overcome biases when desired
4. Respect that sometimes "irrational" preferences are genuinely held values





##### References
----
![[Human Decision Making AI.pdf]]