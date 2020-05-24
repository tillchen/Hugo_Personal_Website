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

#### Turing Machines

1. Formal definition of a TM:
    * A Turing machine is a 7-tuple, $M=(Q,\Sigma,\Gamma,\delta,q_0,q_{accept},q_{reject})$, where $Q,\Sigma,\Gamma$ are all finite sets and
      1. $Q$ is the set of states
      2. $\Sigma$ is the input alphabet not containing the blank symbol $\sqcup$
      3. $\Gamma$ is the tape alphabet, where $\sqcup \in \Gamma$ and $\Sigma \subseteq \Gamma$
      4. $\delta :Q\times \Gamma \rightarrow Q\times \Gamma \times \\{L,R\\}$ is the transition function
      5. $q_0 \in Q$ is the start state
      6. $q_{accept} \in Q$ is the accept state, where $q_{accept} \neq q{reject}$
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

#### Variants of Turing Machines

### Decidability

### Reducibility

## Complexity Theory

### Time Complexity

### Space Complexity

## References

* [Introduction to the Theory of Computation](https://www.goodreads.com/book/show/400716.Introduction_to_the_Theory_of_Computation) by Michael Sipser

* Course slides/notes from Prof. Dr. Peter Zaspel at Jacobs University Bremen.
