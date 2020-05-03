+++
draft = false
date = 2020-05-01T09:25:01+02:00
title = "Machine Learning Notes"
description = "Some notes for basic machine learning concepts."
tags = ["Machine Learning", "AI"]
+++

* [Introduction](#introduction)
  * [Types of Learning](#types-of-learning)
    * [Supervised learning](#supervised-learning)
    * [Unsupervised learning](#unsupervised-learning)
    * [Semi-supervised learning](#semi-supervised-learning)
    * [Reinforcement learning](#reinforcement-learning)
  * [Notations and Definitions](#notations-and-definitions)
* [Fundamental Algorithms](#fundamental-algorithms)
  * [Linear Regression](#linear-regression)
* [References](#references)

## Introduction

This post is about some basic machine learning concepts.

### Types of Learning

#### Supervised learning

* In a feature vector $x_i$ (i=1...N), a single feature is denoted by $x^j$ (j=1...D). And $y_i$ is the label.
* The goal is to produce a model that takes a feature vector x as input and outputs the label.

#### Unsupervised learning

* The goal is either to transform the input feature vector into another vector (dimensionality reduction) or into a value (clustering, outlier detection).

#### Semi-supervised learning

* The dataset has both labeled and unlabeled (much higher quantity) data.
* The same goal as supervised learning.
* The hope is that the unlabeled data can help produce a better model. This is because a larger sample reflects better the probability distribution of the source of the labeled data.

#### Reinforcement learning

* It perceives the **state** of the environment as a feature vector adn the execute **actions** in every state, which bring **rewards** and move the machine to another state.
* The goal is to learn a **policy**: a function that takes the feature vector as input and outputs an optimal action that maximizes the expected average reward.
* It's suited for problems whose decision making is sequential and the goal is long-term.

### Notations and Definitions

1. $x_{l,u}^{(j)}$ in a neural net means the feature j of unit u in layer l.

2. $x$ is by default a column vector and $x^T$ a row vector. Then vector is on the left side of a matrix, we usually do $x^TA$.

3. $arg max_{a \in A}f(a)$ returns the element a of the set A that maximizes f(a).

4. $\mathbb{E}[\hat\theta(S_X) = \theta]$, where $\hat\theta(S_X)$ is the unbiased estimator of some statistic $\theta$ (e.g. $\mu$) calculated using a sample $S_X$.

5. A hyperparameter is a parameter whose value is set before the learning process begins. By contrast, the values of other parameters are derived via training.

6. Model-based learning vs instance-based learning:
    * Model-based: creates a model with parameters learned from the data. (Most supervised learning algorithms)
    * Instance-based: uses the whole dataset as the model. Instead of performing explicit generalization, it compares new problem instances with instances seen in training (e.g. kNN).

7. Shallow vs deep learning:
    * Shallow learning: learns the parameters of the model directly from the features of the training examples.
    * Deep (neural network) learning: uses neural nets with more than one layer and learns the parameters from the outputs of the preceding layers instead.

## Fundamental Algorithms

### Linear Regression

1. We want a model as a linear combination of features of example x ($w$ is a D-dimensional vector of parameters and b is a real number.):

$$f_{w,b}(x) = wx+b$$

2. We find the optimal values $w^{\*}$ and $b^{\*}$ by minimizing the cost function below (the empirical risk - the average loss):

$$\frac{1}{N}\sum_{i=1...N}(f_{w,b}(x_i)-y_i)^2$$

3. Overfitting: a model that predicts well for the training data but not for data unseen during training. Linear regression rarely overfits.

4. The squared loss is used since it's convinent. The absolute loss function doesn't have a continuous derivative, which makes it not smooth. Unsmooth functions create difficulties for optimization problems in linear algebra.

5. To find the extrema (minima or maxima), we can simply set the gradient to zero.

## References

* [The Hundred-Page Machine Learning Book](https://www.goodreads.com/book/show/43190851-the-hundred-page-machine-learning-book)
