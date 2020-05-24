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

### Reducibility

## Complexity Theory

### Time Complexity

### Space Complexity

## References

* [Introduction to the Theory of Computation](https://www.goodreads.com/book/show/400716.Introduction_to_the_Theory_of_Computation) by Michael Sipser

* Course slides/notes from Prof. Dr. Peter Zaspel at Jacobs University Bremen.