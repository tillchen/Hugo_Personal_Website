+++
draft = false
date = 2020-05-24T08:45:46+02:00
title = "Computability and Complexity Notes"
description = "Course notes for Computability and Complexity at Jacobs University Bremen"
tags = ["Computer Science"]
+++

* [Introduction](#introduction)
* [Computability Theory](#computability-theory)
  * [The Church-Turing Thesis](#the-church-turing-thesis)
    * [Turing Machines](#turing-machines)
    * [Variants of Turing Machines](#variants-of-turing-machines)
      * [Mutlitape TM](#mutlitape-tm)
      * [Nondeterministic TM](#nondeterministic-tm)
      * [Random Access Machine](#random-access-machine)
  * [Decidability](#decidability)
    * [Decidable Languages](#decidable-languages)
    * [Undecidability of $A_{TM}$](#undecidability-of-math-xmlns%22httpwwww3org1998mathmathml%22semanticsmrowmsubmiamimrowmitmimimmimrowmsubmrowannotation-encoding%22applicationx-tex%22atmannotationsemanticsmathatm%e2%80%8b)
    * [A Turing-Unrecognizable Language](#a-turing-unrecognizable-language)
  * [Reducibility](#reducibility)
* [Complexity Theory](#complexity-theory)
  * [Time Complexity](#time-complexity)
  * [Space Complexity](#space-complexity)
* [References](#references)

## Introduction

This is the course notes for Computability and Complexity by Prof. Dr. Peter Zaspel at Jacobs University Bremen.

## Computability Theory

### The Church-Turing Thesis

There exists

1. an intuitive idea of an algorithm and
2. a formalization via DTM/NTM/RAM

The hypothesis that both are equal is called Church-Turing Thesis.

#### Turing Machines

1. Formal definition of a TM:
    * A Turing machine is a 7-tuple, $M=(Q,\Sigma,\Gamma,\delta,q_0,q_{accept},q_{reject})$, where $Q,\Sigma,\Gamma$ are all finite sets and
      1. $Q$ is the set of states
      2. $\Sigma$ is the input alphabet not containing the blank symbol $\sqcup$
      3. $\Gamma$ is the tape alphabet, where $\sqcup \in \Gamma$ and $\Sigma \subseteq \Gamma$
      4. $\delta :Q\times \Gamma \rightarrow Q\times \Gamma \times \\{L,R\\}$ is the transition function
      5. $q_0 \in Q$ is the start state
      6. $q_{accept} \in Q$ is the accept state, where $q_{accept} \neq q_{reject}$
      7. $q_{reject} \in Q$ is the reject state.

2. Configuration of a TM:
    * Let M be a TM, $u,v \in \Gamma^*$ and $q \in Q$. The setting $uqv$ is a configuration of the TM, where
      * $u$ is the current tape content to the left of the head
      * $q$ is the current state
      * $v$ is the current tape content **below** ($v_1$) **and to the right** of the head (being terminated by blanks $\sqcup$)

3. A configuration $C_1$ **yields** a configuration $C_2$ if M can legally from $C_1$ to $C_2$ in a single step.
    * Leftward move: $uaq_i bv$ yields $uq_j acv$ iff $\delta(q_i, b) = (q_j, c, L)$
    * Rightward move: $uaq_i bv$ yields $uacq_j v$ iff $\delta(q_i, b) = (q_j, c, R)$
    * L-move, left tape end: $q_i bv$ yields $q_j cv$ iff $\delta(q_i, b) = (q_j, c, L)$
    * R-move, left tape end: $q_i bv$ yields $cq_j v$ iff $\delta(q_i, b) = (q_j, c, R)$

4. Characterization of configuration:
    * Start configuration: $u = \epsilon$, i.e. head is at leftmost end of tape
    * Accepting configuration: $q=q_{accept}$
    * Rejecting configuration: $q=q_{reject}$
    * Halting configuration: accepting or rejecting configuration
    * Remark: there's exactly one accepting/rejecting state, but there can be many accepting/rejecting configurations.

5. Accepted input and recognized language:
    * M accepts $w$ if a sequence of configurations $C_1 , C_2 , ..., C_k$ exists, such that
      1. $C_1$ is the start configuration
      2. $C_i$ yields $C_{i+1}$
      3. $C_k$ is the accepting configuration
    * The language of M is $L(M) = \\{w \in \Sigma^* | M \ \text{accepts} \ w\\}$. We say L is recognized by M.

6. Turing-recognizable or recursively enumerable language, if some TM recognizes it.

7. M halts on $w$ if a sequence of configurations $C_1 , C_2 , ..., C_k$ exists, such that
    1. $C_1$ is the start configuration
    2. $C_i$ yields $C_{i+1}$
    3. $C_k$ is the halting configuration

8. Decider: if it halts on all inputs $w \in \Sigma^*$. A decider M that recognizes L is said to decide L.

9. Decidable/Recursive/Turing-decidable language: if there exists a TM (i.e. a decider) that decides it.

#### Variants of Turing Machines

1. All variants have the same power as a standard TM.

##### Mutlitape TM

1. The definition differs from the standard TM that: $\delta :Q\times \Gamma^k \rightarrow Q\times \Gamma^k \times \\{L,R\\}^k$

2. For every multitape TM M, there exits a single-tape TM S that recognizes the same language.

3. Turing-recognizable iff some multitape TM recognizes it.

##### Nondeterministic TM

1. The definition differs from the standard TM that: $\delta :Q\times \Gamma \rightarrow \mathcal{P}(Q\times \Gamma \times \\{L,R\\})$

2. For definition of yielding configurations, it differs from the standard TM that we need to change from $=$ to $\in$. (One config can yield several or no config.)

3. Exactly the same definition for accepted input and recognized language.

4. For every NTM N, there exists a deterministic (single-tape) TM S that recognizes the same language.

5. Turing-recognizable iff some NTM recognizes it.

6. Nondeterministic decider: if all branches halt on all inputs.

##### Random Access Machine

1. k - command counter; a - accumulator; c - register; x - input; $h_r$ - position on input; y - output.

2. Some commands:
    * read: $a = x_{h_r}; \ h_r = h_r + 1; k = k + 1$
    * print a: $y=ay; k = k + 1$

3. Input tape: read-only and read once, can only move to the right

4. Program: finite sequence of commands.

5. There exists a RAM that terminates and outputs 1 whenever a TM M accepts. The RAM terminates and outputs 0 whenever M rejects.

6. Let R be an RAM. For an arbitrary input x it outputs y(x). There exists a multi-tape TM that accepts the input x after writing y(x) on one of its tapes.

7. TMs and RAMs have the same expressive power.

### Decidability

#### Decidable Languages

1. The language $A_{DFA}=\\{\langle B,w \rangle| \text{B is a DFA that accepts input string } w \\}$ is decidable. (The problem of testing whether a given DFA accepts a given string is decidable.)

2. The language $A_{NFA}=\\{\langle B,w \rangle| \text{B is a NFA that accepts input string } w \\}$ is decidable. (Convert to NFA to DFA.)

3. The language $A_{REX}=\\{\langle B,w \rangle| \text{B is a regular expression that generates string } w \\}$ is decidable. (Convert R to DFA.)

4. The language $E_{DFA}=\\{\langle A \rangle| \text{A is a DFA and L(A) = } \emptyset \\}$ is decidable. (No accept states are marked.)

5. The language $EQ_{DFA}=\\{\langle A,B \rangle| \text{A and B are DFAs and L(A)=L(B) } \\}$ is decidable. (Build C that's empty iff A=B. Use $E_{DFA}$ on C.)

6. The language $A_{CFG}=\\{\langle G,w \rangle| \text{A is a CFG that generates string } w \\}$ is decidable. (Convert G to CFG in Chomsky Normal Form; enumerate all derivations within 2n-1 steps.)

7. The language $E_{CFG}=\\{\langle A \rangle| \text{A is a CFG and L(G) = } \emptyset \\}$ is decidable. (Mark all terminal symbols. Follow the rules until no new variables are marked. If the start symbol is not marked, accept.)

8. But $EQ_{CFG}$ is not decidable.

9. Every context-free language L is decidable. (Build a TM with CFG G with $A_{CFG}$)

#### Undecidability of $A_{TM}$

1. The language $A_{TM}=\\{\langle M,w \rangle| \text{M is a TM and M accepts } w \\}$ is undecidable. (Proof by diagonalization. A TM D($\langle M\rangle$) that accept if M doesn't accept $\langle M\rangle$, which leads to contradiction.)

2. The language $A_{TM}=\\{\langle M,w \rangle| \text{M is a TM and M accepts } w \\}$ is Turing-recognizable. (Build TM U. Simulate M on w. If M accepts, U accepts. If M rejects, U rejects.) (U is an instance of Universal TM) (U can run forever.)

3. Sets:
    * A and B have the same size/cardinality if there exists a bijective function f with $f: A \rightarrow B$.
    * A is countable if it's either finite or has the same size as $\mathbb{N}$. Otherwise it's uncountable.
      * The set $\mathbb{Q}$ of rational numbers is countable.
      * The set $\mathbb{R}$ of real numbers is uncountable. (Proof by diagnolization.)

4. There exist languages that are not Turing-recognizable.
    * Fixing a non empty alphabet $\Sigma$, the set of all TMs over $\Sigma$ is countable. (M can be mapped to binary strings, which are countable (enumerate).)
    * The set $\mathcal{B}$ of all infinite binary sequences is uncountable. (Proof by diagnolization.)
    * Fixing a non-empty alphabet $\Sigma$, the set of all languages over $\Sigma$ is uncountable. (Construct a bijection between the set of all languages of $\Sigma$ and $\mathcal{B}$ to have the characteristic string. The latter is uncountable, the former is also uncountable.)
    * The set of TMs is countable but the set of languages is uncountable. So there are languages not described by TMs.

#### A Turing-Unrecognizable Language

1. L is co-Turing-recognizable if $\bar L$ is Turing-recognizable.

2. A language is decidable iff it's Turing-recognizable and co-Turing-recognizable. (Run two TMs in parallel.)

3. The language $\bar{A_{TM}}$ is not Turing recognizable. (L is undecidable $\Rightarrow$ L not Turing recognizable $\vee$ $\bar L$ not Turing recognizable $\Rightarrow$ $\bar L$ not Turing recognizable)

### Reducibility

1. The language $HALT_{TM}=\\{\langle M,w \rangle| \text{M is a TM and M halts on input} w \\}$ is undecidable. (Proof by contradiction. Assume there's a decider R for $HALT_{TM}$. Construct a decider for $A_{TM}$ ("R rejects, reject" eliminates the loop case.))

2. A Computable function f $\Rightarrow$ there exists some TM M, on every input w, halts with just f(w) on its tape.

3. A is mapping reducible to B ($A \leq_{m} B$) if there's a computable function f between them. f is called a reduction from A to B.

4. If $A \leq_{m} B$ and B is decidable, A is decidable.

5. If $A \leq_{m} B$ and A is undecidable, B is undecidable.

6. We can also prove $HALT_{TM}$ to be undecidable by finding a reduction from $A_{TM}$. ($w \in A_{TM} \Leftrightarrow f(w) \in HALT_{TM}$)

7. The language $REGULAR_{TM}=\\{\langle M \rangle| \text{M is a TM and L(M) is a regular language} \\}$ is undecidable.

## Complexity Theory

### Time Complexity

### Space Complexity

## References

* [Introduction to the Theory of Computation](https://www.goodreads.com/book/show/400716.Introduction_to_the_Theory_of_Computation) by Michael Sipser

* Course slides/notes from Prof. Dr. Peter Zaspel at Jacobs University Bremen.
