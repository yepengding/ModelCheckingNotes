# Model Checking Notes

Notes in fundamentals of model checking.

[https://yepengding.github.io/ModelCheckingNotes/](https://yepengding.github.io/ModelCheckingNotes/)

# System

## Correctness

A system satisfies its specifications.

## Properties

- Safety
    - Nothing bad should happen.
    - Delcare what should not happen or what should always happen.
    - Counterexample: a trace of states, where the last state contradicts the property.

- Liveness
    - Something bad never happens.
    - Declare what should eventually happen.
    - Counterexample: an infinite path (e.g., a loop) that never reaches the specified state.

# Model Checking

## Features

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

## Main Challenge

State explosion problem.

# Structures

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

> Labels can represent different things depending on the language of interest, such as input expected, conditions that must be true to trigger the transition, or actions performed during the transition.

### Kripke Structure

$\mathfrak{K} \triangleq (S, I, {\to}, \mathcal{L})$

- $S$ is a set of states,
- $I \subseteq S$ is a set of initial states,
- ${\to} \subseteq S \times S$ is a transition relation, and
- $\mathcal{L}: S \mapsto \wp(P)$ is a labeling function, where $P$ is a set of atomic propositions and $\wp(P)$ denotes
  the powerset over $P$.

> Labeling is a function to attach observations (atomic propositions) to a system.

### Labeled Kripke Structure

$\mathfrak{S} \triangleq (S, I, A, {\to}, \mathcal{L})$

- $S$ is a set of states,
- $I \subseteq S$ is a set of initial states,
- $A$ is a set of actions,
- ${\to} \subseteq S \times S$ is a transition relation, and
- $\mathcal{L}: S \mapsto \wp(P)$ is a labeling function.

> Clarification: the label set $L$ of a $\mathfrak{L}$ has no direct relation to the labeling function $\mathcal{L}$ of a $\mathfrak{K}$. Therefore, I use the name **Labeled Kripke Structure** for the variation defined above by using the semantics of the word **labeled** in **Labeled Transition System** to introduce labels (e.g., actions) into *Kripke Structure*.

> In the rest of the notes, we mainly take $\mathfrak{S}$ for example.

## Predecessor and Successor

Given a $\mathfrak{S}$, the set of successors of $s \in S$ is defined as:

$\textit{Succ}(s) = \bigcup\limits_{a \in A} \{ s' \in S \mid s \xrightarrow{a} s' \}$

The set of predecessors is defined as:

$\textit{Pred}(s) = \bigcup\limits_{a \in A} \{ s' \in S \mid s' \xrightarrow{a} s \}$

## Terminal State

State $s$ in $\mathfrak{S}$ is called `terminal` if and only if $\textit{Succ}(s)=\emptyset$.

## Deterministic Structure

A $\mathfrak{S}$ can be `action-deterministic` and `AP-deterministic`.

### Action-Deterministic

- $\lvert I \rvert \leq 1$, and
- $\forall s \in S, a \in A: \lvert \textit{Succ}(s, a) \rvert \leq 1$.

### AP-deterministic

$\forall p \in \wp(P):$

- $\lvert\{ s \in I \mid \mathcal{L}(s) = p \} \rvert \leq 1$, and
- $\forall s \in S: \lvert\textit{Succ}(s) \cap \{ s' \in S \mid \mathcal{L}(s') = p \}\rvert \leq 1$.

# Behaviors

## Path

A `path` of $\mathfrak{S}$ is an initial, maximal path fragment.

### Path Fragment

A `finite path fragment` $\hat{\pi}$ of $\mathfrak{S}$ is a finite state sequence $(s_0, s_1, \dots, s_n)$ such that

$\forall i \in (0, n]: s_i \in \textit{Post}(s_{i-1})$ where $n \geq 0$.

An `infinite path fragment` $\pi$ is an infinite state sequence $(s_0, s_1, s_2, \dots)$ such that

$\forall i > 0: s_i \in \textit{Post}(s_{i-1})$.

### Initial Path Fragment

A path fragment $(s_0, s_1, s_2, \dots)$ is called `initial` if $s_0 \in I$.

### Maximal Path Fragment

A `maximal` path fragment is either a finite path fragment that ends in a terminal state, or an infinite path fragment.


---

# References

- Biere, A., Cimatti, A., Clarke, E. M., Strichman, O., & Zhu, Y. (2003). Bounded model checking.
- Baier, C., & Katoen, J. P. (2008). Principles of model checking. MIT press.