# Human & AI Decision Making

## Introduction

This document summarizes lecture materials on decision making principles, focusing on how humans make decisions versus mathematical models of rationality, and the implications for AI systems designed to assist human decision making.

## Computational Strengths vs. Human Decision Making

### AI Computational Strengths
- Mathematical statistics
- Access to a wide range of knowledge sources

### Human Decision Challenges
- Trust
- Bias
- Empathy
- Human understanding

## Mathematical Representations of Risk

### Expected Value (EV)

Expected Value calculates the average outcome of a decision involving uncertainty by summing the products of each possible outcome and its probability.

$$ \text{EV}(X) = \sum_{i=1}^{n} p_i x_i $$

**Example: Lottery Ticket Decision**
- **Bet 1:** Each lottery ticket costs £5 with a 1% chance to win £1000.
  - EV = 0.01 × £1000 - £5 = £10 - £5 = £5 (positive expected value)
  
- **Bet 2:** Lottery tickets cost £10 with:
  - 50% chance to win £6
  - 40% chance to win £8
  - 10% chance to win £50
  - EV = 0.5 × £6 + 0.4 × £8 + 0.1 × £50 - £10 = £3 + £3.2 + £5 - £10 = £1.2 (positive expected value)

### Utility and Expected Utility

Expected Utility extends the concept of Expected Value by accounting for the subjective value (utility) that people place on outcomes rather than just the monetary value.

$$ \text{EU}(X) = \sum_{i=1}^{n} p_i U(x_i) $$

**Diminishing Marginal Utility**

The utility function often takes the form:
$$ U(x) = x^a $$
where 0 < a < 1, representing diminishing returns—the principle that each additional unit of gain leads to an ever-smaller increase in subjective value.

### Subjective Expected Utility (SEU)

Developed in the 1940s by Von Neumann, Morgenstern, and later Savage, SEU incorporates subjective probability judgments:

$$ \text{SEU}(X) = \sum_{i=1}^{n} s_i U(x_i) $$

where s = subjective judgment of probabilities.

#### Axiomatic Foundations of SEU

1. **Completeness**: Preferences over uncertain outcomes are complete
2. **Transitivity**: If A is preferred to B and B is preferred to C, then A must be preferred to C
3. **Independence**: Preferences should not depend on irrelevant outcomes
4. **Continuity**: Preferences can be represented by a continuous utility function
5. **Monotonicity**: Adding a preferred outcome to a lottery makes that lottery more desirable
6. **Sure-Thing Principle**: If an outcome is preferred in one context, it should be preferred in all contexts regardless of probability differences

## Paradoxes in Decision Making

### St Petersburg Paradox (1713)

A game where:
- Coin toss: if heads win £1, game ends; if tails continue
- Coin toss: if heads win £2, game ends; if tails continue
- Coin toss: if heads win £4, game ends; if tails continue
- And so on...

The expected value is infinite, but most people would pay only a small amount to play this game, demonstrating the inadequacy of expected value for decision-making.

### Allais Paradox (1953)

Illustrates violations of the independence axiom:

**First Choice:**
- **Bet A**: 33% chance of receiving £2500, 66% chance of receiving £2400, 1% chance of receiving £0
- **Bet B**: 100% chance of receiving £2400

**Second Choice:**
- **Bet C**: 33% chance of receiving £2500, 67% chance of receiving £0
- **Bet D**: 34% chance of receiving £2400, 66% of receiving £0

Most people choose B over A, but C over D, which violates the expected utility theory's axioms.

## Human Decision Biases

Research by Tversky and Kahneman identified several systematic biases in human decision-making:

### Certainty Effect

People overweight outcomes that are considered certain, relative to outcomes which are merely probable.

**Example:**
- Would you choose:
  a) 80% chance to win £100 and 20% to win £10, or
  b) £80 guaranteed?

Most people choose the certain option (b) even when the expected value of option (a) is higher.

### Reference Point Dependence

People evaluate outcomes relative to a reference point, not in absolute terms.

**Example:**
- Jack had £1 million yesterday and now has £5 million
- Jill had £9 million yesterday and now has £5 million
- Despite having identical current wealth, Jill feels like she has lost while Jack feels like he has gained

### Loss Aversion

Losses loom larger than equivalent gains—people feel more pain from losses than pleasure from equivalent gains.

### Endowment Effect

People value things more just because they own them.

Reference: Kahneman, Knetsch, & Thaler (1990), "Experimental Tests of the Endowment Effect and the Coase Theorem"

### Framing Effect

How a choice is presented (framed) affects the decision, even when the underlying facts are identical.

**Example:** Describing a food product as "80% fat-free" versus "20% fat"

## Prospect Theory

Developed by Kahneman and Tversky as a response to choice anomalies, Prospect Theory offers a descriptive model of decision making under risk.

### Key Innovations

- **Pre-decision editing**: Simplification of prospects before evaluation
- **Reference dependence**: Outcomes evaluated as gains or losses from a reference point
- **Differential treatment of gains versus losses**: Different risk attitudes for gains and losses
- **Loss aversion**: Losses hurt more than equivalent gains feel good

### The Fourfold Pattern of Risk Attitudes

Prospect Theory predicts:
- **Risk aversion for gains of moderate to high probability**
- **Risk seeking for losses of moderate to high probability**
- **Risk seeking for gains of low probability**
- **Risk aversion for losses of low probability**

## Implications for AI Decision Making

Humans are not mathematically rational decision makers. If we want AI to make decisions for us or assist in our decision-making, AI systems need to account for our biases and decision-making patterns.

This creates challenges for designing AI systems that:
1. Make recommendations aligned with human preferences
2. Present information in ways that don't exploit human biases
3. Help humans overcome biases when desired
4. Respect that sometimes "irrational" preferences are genuinely held values

## Further Reading

Kahneman, D. (2011) "Thinking Fast and Slow" - Available in the main library