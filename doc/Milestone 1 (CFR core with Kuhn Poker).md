# Mathematical Foundations for Milestone 1: CFR Core with Kuhn Poker

This document summarizes the key mathematical concepts required to implement **Milestone 1** of the project: *Counterfactual Regret Minimization (CFR) with Kuhn Poker*.

---

## 1. Information Set (Infoset)

- **Definition**: An *infoset* represents all game states that are indistinguishable to a player, given their observations (own cards, betting history, etc.).
- **Purpose**: CFR does not track regrets for each full state, but rather for each infoset.  
- **Example in Kuhn Poker**:  
  - State = `(my card = Q, betting history = "bet")`  
  - Two global states (opponent has J or K) look identical to me → they belong to the same infoset.

---

## 2. Payoff Function

- **Terminal state payoff**: For each player, the payoff is computed at the end of the game.  
- **In Kuhn Poker**: The winner receives the pot; the loser pays their contribution.  
- Payoffs are typically expressed from the perspective of one player (e.g., Player 0).

---

## 3. Regret

- **Instant regret at iteration t** for infoset \(I\) and action \(a\):  

  \[
  r^t(I, a) = v^t(I, a) - v^t(I)
  \]

  where:  
  - \(v^t(I, a)\): counterfactual value if action \(a\) is always chosen at \(I\).  
  - \(v^t(I)\): counterfactual value under the current strategy at \(I\).  

- **Intuition**:  
  - Positive regret → "I would have done better if I had chosen this action."  
  - Negative regret → "Not choosing this action saved me from loss."

---

## 4. Cumulative Regret

- CFR is iterative. Regret is accumulated across iterations:  

  \[
  R^T(I, a) = \sum_{t=1}^T r^t(I, a)
  \]

- These cumulative regrets drive the adjustment of strategy over time.

---

## 5. Regret Matching

- Strategy for infoset \(I\) at iteration \(T+1\):  

  \[
  \sigma^{T+1}(I, a) =
  \begin{cases}
  \frac{\max(R^T(I, a), 0)}{\sum_{a'} \max(R^T(I, a'), 0)} & \text{if denominator > 0} \\
  \frac{1}{|A(I)|} & \text{otherwise (uniform distribution)}
  \end{cases}
  \]

- **Interpretation**:  
  - Actions with larger positive regrets are given higher probability.  
  - If all regrets are ≤ 0, fallback to a uniform random strategy.

---

## 6. Average Strategy

- The convergence guarantee of CFR is not on the *current strategy* but on the **average strategy** across iterations.  
- Accumulate strategies during training:  

  \[
  \bar{\sigma}^T(I, a) = \frac{\sum_{t=1}^T \pi^t(I) \cdot \sigma^t(I, a)}{\sum_{t=1}^T \pi^t(I)}
  \]

  where \(\pi^t(I)\) is the reach probability of infoset \(I\) under iteration \(t\).  

- This average strategy converges to a Nash equilibrium in two-player zero-sum games.

---

## 7. Kuhn Poker Recap

- **Deck**: {J, Q, K} (3 cards). Each player receives 1 card.  
- **Betting**: One round, single bet size.  
  - Actions: *Check*, *Bet*, *Call*, *Fold*.  
- **Payoffs**: Winner gains 1 chip (or 2 if a bet/call occurred).  
- **Why Kuhn?**  
  - Simple yet non-trivial imperfect-information game.  
  - Common benchmark for CFR implementations.

---

## References

- Martin Zinkevich et al., *Regret Minimization in Games with Incomplete Information* (2007).  
- Kevin Waugh, *A Practical Introduction to Regret Minimization in Games* (2015).  
- [CFR explanation on Wikipedia](https://en.wikipedia.org/wiki/Counterfactual_regret_minimization)

---

**Summary**:  
To complete Milestone 1, you must understand how to compute regrets for each infoset, accumulate them across iterations, and update strategies via regret matching. Kuhn Poker provides the smallest useful testbed to validate your CFR engine.
