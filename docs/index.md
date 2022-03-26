# Model Checking Notes

## Correct System

A system satisfies its specifications.

## System Properties

- Safety
    - Nothing bad should happen.
    - Delcare what should not happen or what should always happen.
    - Counterexample: a trace of states, where the last state contradicts the property.

- Liveness
    - Something bad never happens.
    - Declare what should eventually happen.
    - Counterexample: an infinite path (e.g., a loop) that never reaches the specified state.

## Model Checking Features

1. Automatic verification (falsification)
2. Finite systems (extensible to infinite systems)
3. Temporal logic

## Common Techniques

- Enumeration
    - Check properties by explicitly enumerating reachable states.
- Symbolic model checking
    - Sets of states are represented implicitly by Boolean functions. Check a property with Reduced Ordered Binary
      Decision Diagrams.
- Bounded model checking
    - Check a property by searching for a counterexample in executions whose length is bounded by some integer k with
      SAT techniques.

## Transition System

$\mathfrak{T} \triangleq (S, {\to})$

- $S$ is a set of states, and
- ${\to} \subseteq S \times S$ is a transition relation.

## Transition System Variations

### Labeled Transition System

$\mathfrak{L} \triangleq (S, L, {\to})$

- $S$ is a set of states,
- $L$ is a set of labels, and
- ${\to} \subseteq S \times L \times S$ is a transition relation.

### Kripke Structure

$\mathfrak{K} \triangleq (S, I, {\to}, \mathcal{L})$

- $S$ is a set of states,
- $I \subseteq S$ is a set of initial states,
- ${\to} \subseteq S \times S$ is a transition relation, and
- $\mathcal{L}: S \mapsto \wp(P)$ is a labeling function, where $P$ is a set of atomic propositions and $\wp(P)$ denotes
  the powerset over $P$.

> Clarification: the label set $L$ of a $\mathfrak{L}$ has no direct relation to the labeling function $\mathcal{L}$ of a $\mathfrak{K}$. Therefore, I use the name `Labeled Kripke Structure` for a variation defined below by using the semantics of the word `labeled` in `Labeled Transition System` to introduce labels (i.e., actions) into `Kripke Structure`.

### Labeled Kripke Structure

$\mathfrak{K}' \triangleq (S, I, A, {\to}, \mathcal{L})$

- $S$ is a set of states,
- $I \subseteq S$ is a set of initial states,
- $A$ is a set of actions,
- ${\to} \subseteq S \times S$ is a transition relation, and
- $\mathcal{L}: S \mapsto \wp(P)$ is a labeling function.

---

# References

- Biere, A., Cimatti, A., Clarke, E. M., Strichman, O., & Zhu, Y. (2003). Bounded model checking.
- Baier, C., & Katoen, J. P. (2008). Principles of model checking. MIT press.