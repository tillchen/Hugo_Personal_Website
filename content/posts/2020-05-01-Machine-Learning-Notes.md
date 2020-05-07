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
* [Logistic Regression](#logistic-regression)
* [Decision Tree Learning](#decision-tree-learning)
* [Support Vector Machine](#support-vector-machine)
  * [Dealing With Noise](#dealing-with-noise)
    * [Dealing with Inherent Non-Linearity (Kernels)](#dealing-with-inherent-non-linearity-kernels)
* [k-Nearest Neighbors (kNN)](#k-nearest-neighbors-knn)
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

* It perceives the **state** of the environment as a feature vector and then execute **actions** in every state, which bring **rewards** and move the machine to another state.
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

## Logistic Regression

1. Logistic regression is not a regression, but a classification learning algorithm. The names is because the mathematical formulation is similar to linear regression.

2. The standard logistic function or the sigmoid function:

$$f(x)=\frac{1}{1+e^{-x}}$$

![Logistic Function](/images/logistic_function.png)

3. The logistic regression model:

$$f(x)=\frac{1}{1+e^{-(wx+b)}}$$

4. For binary classification, we can say the label is positive if the probability is higher than or equal to 0.5.

5. We optimize by using the maximum likelihood (the goodness of fit) ($y_i$ is either 0 or 1):

$$L_{w,b}=\prod_{i=1...N}f_{w,b}(x_i)^{y_i}(1-f_{w,b}(x_i))^{1-y_i}$$

6. In practice, it's more convenient to maximize the log-likelihood (since ln is a strictly increasing function, maximizing this is the same as maximizing its argument):

$$LogL_{w,b}=ln(L_{w,b})=\sum_{i=1}^Ny_iln(f_{w,b}(x_i)) + (1-y_i)ln(1-f_{w,b}(x_i))$$

7. Unlike linear regression, there's no closed form solution. A typical numerical optimization procedure is gradient descent.

## Decision Tree Learning

To be filled.

## Support Vector Machine

To be filled.

### Dealing With Noise

To be filled.

#### Dealing with Inherent Non-Linearity (Kernels)

1. The kernel trick: use a function to *implicitly* transform the original space into a higher dimensional space during the cost function optimization. (We hope that data will be linearly separable in the transformed space).

2. We use kernel functions or simply kernels to efficiently work in higher-dimensional spaces without doing this transformation explicitly.

3. By using the kernel trick, we get rid of a costly transformation to the higher dimension and avoid computing their dot-product.

4. We can use the quadratic kernel $k(x_i, x_k) = (x_ix_k)^2$ here. Another widely used kernel is the RBF (radial basis function) kernel: $k(x, x^{'}) = exp(-\frac{||x-x^{'}||^2}{2\sigma^2})$. It has infinite dimensions. We can vary the hyperparameter $\sigma$  and choose wether to get a smooth of curvy decision boundary.

## k-Nearest Neighbors (kNN)

1. kNN is a non-parametric learning algorithm. Contrary to other learning algorithms that allow discarding the training data after the model is built, kNN keeps all training examples in memory.

2. The closeness of two examples is given by a distance function. Other than the Euclidean distance, we could also use the cosine similarity function ($0^{\circ}: 1; 90^{\circ}: 0; 180^{\circ}: -1$).

## References

* [The Hundred-Page Machine Learning Book](https://www.goodreads.com/book/show/43190851-the-hundred-page-machine-learning-book)
