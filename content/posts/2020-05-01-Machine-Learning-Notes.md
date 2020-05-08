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
* [Anatomy of a Learning Algorithm](#anatomy-of-a-learning-algorithm)
  * [Building blocks](#building-blocks)
  * [Gradient Descent](#gradient-descent)
  * [Particularities](#particularities)
* [Basic Practice](#basic-practice)
  * [Feature Engineering](#feature-engineering)
    * [One-Hot Encoding (Categorical -> Numerical)](#one-hot-encoding-categorical---numerical)
    * [Binning (Bucketing) (Numerical -> Categorical)](#binning-bucketing-numerical---categorical)
    * [Normalization](#normalization)
    * [Standardization (Z-score Normalization)](#standardization-z-score-normalization)
    * [Dealing with Missing Features](#dealing-with-missing-features)
  * [Learning Algorithm Selection](#learning-algorithm-selection)
  * [Three Sets](#three-sets)
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

## Notations and Definitions

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

### Logistic Regression

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

### Decision Tree Learning

To be filled.

### Support Vector Machine

To be filled.

#### Dealing With Noise

To be filled.

##### Dealing with Inherent Non-Linearity (Kernels)

1. The kernel trick: use a function to *implicitly* transform the original space into a higher dimensional space during the cost function optimization. (We hope that data will be linearly separable in the transformed space).

2. We use kernel functions or simply kernels to efficiently work in higher-dimensional spaces without doing this transformation explicitly.

3. By using the kernel trick, we get rid of a costly transformation to the higher dimension and avoid computing their dot-product.

4. We can use the quadratic kernel $k(x_i, x_k) = (x_ix_k)^2$ here. Another widely used kernel is the RBF (radial basis function) kernel: $k(x, x^{'}) = exp(-\frac{||x-x^{'}||^2}{2\sigma^2})$. It has infinite dimensions. We can vary the hyperparameter $\sigma$  and choose wether to get a smooth of curvy decision boundary.

### k-Nearest Neighbors (kNN)

1. kNN is a non-parametric learning algorithm. Contrary to other learning algorithms that allow discarding the training data after the model is built, kNN keeps all training examples in memory.

2. The closeness of two examples is given by a distance function. Other than the Euclidean distance, we could also use the cosine similarity function ($0^{\circ}: 1; 90^{\circ}: 0; 180^{\circ}: -1$).

## Anatomy of a Learning Algorithm

### Building blocks

1. A loss function
2. An optimization criterion based on the loss function (e.g. a cost function)
3. An optimization routine leveraging training data to find a solution to the optimization criterion.

### Gradient Descent

1. To find a local minimum, start at some random point and takes step proportional (learning rate) to the negative of the gradient.

2. The gradient is calculated by taking the partial derivative for every parameter in the loss function: (take linear regression as an example)

$$l = \frac{1}{N}\sum_{i=1}^{N}(y_i-(wx_i+b))^2$$

$$\frac{\partial l}{\partial w} = \frac{1}{N}\sum_{i=1}^{N}-2x_i(y_i-(wx_i+b))$$

$$\frac{\partial l}{\partial b} = \frac{1}{N}\sum_{i=1}^{N}-2(y_i-(wx_i+b))$$

3. An epoch consists of using the training set entirely to update each parameter. At each epoch, we update $w$ and $b$ ($\alpha$ is the learning rate):

$$w \leftarrow w - \alpha\frac{\partial l}{\partial w}$$

$$b \leftarrow b - \alpha\frac{\partial l}{\partial b}$$

4. Minibatch stochastic gradient descent is a version that speed up the computation by approximating the gradient using smaller batches.

### Particularities

1. Some algorithms, like decision tree learning, can accept categorical features while others expect numerical values. All algorithms in scikit-learn expect numerical features.

2. Some algorithms, like SVM, allow weightings for each class. If the weighting is higher, the algorithm tries not to make errors in predicting training examples of this class.

3. Some classification models, like SVM and kNN, only output the class. Others, like logistic regression or decision trees, can also return the score between 0 and 1 (can be used as a confidence score).

4. Some classification algorithms - like decision trees, logistic regression, or SVM - build the model using the whole dataset at once. Others can be trained iteratively, one batch at a time.

5. Some algorithms, like decision trees/SVM/kNN, can be used for both classification and regression, while others can only solve one type of problem.

## Basic Practice

### Feature Engineering

1. Feature engineering: the problem of transforming raw data into a dataset.

2. The role of the data analyst is to create informative features with high predictive power.

3. We say a model has a low bias when it predicts the training data well.

#### One-Hot Encoding (Categorical -> Numerical)

1. One-hot is a group of bits among which the legal combinations of values are only those with a single high (1) bit and all the others low (0). It transforms a categorical feature into several binary ones.

2. Example: red = [1,0,0]; yellow = [0,1,0]; green = [0,0,1].

3. When the ordering matters, we can just do: {poor, decent, good, excellent} -> {1, 2, 3, 4}.

#### Binning (Bucketing) (Numerical -> Categorical)

1. Binning converts a continuous feature in to multiple binary features called bins, typically based on value range.

#### Normalization

1. Normalization converts a numerical value into a value typically in the interval [-1,1] or [0,1], which increases the speed of learning:

$$\bar x^{(j)} = \frac{x^{(j)}-min^{(j)}}{max^{(j)}-min^{(j)}}$$

#### Standardization (Z-score Normalization)

1. Standardization rescales the feature values so that they have the properties of a standard normal distribution with $\mu = 0$ and  $\sigma = 1$.

2. Standard scores or z-scores can be calculated as follows:

$$\hat x^{(j)} = \frac{x^{(j)} - \mu^{(j)}}{\sigma^{(j)}}$$

3. Normalization vs Standardization:
    * Unsupervised learning - standardization.
    * The distribution is close to a normal distribution - standardization.
    * Have outliers - standardization (normalization will squeeze the normal values into a very small range).
    * Other cases - normalization.

#### Dealing with Missing Features

1. Remove the examples with missing features

2. Use a learning algorithm that can deal with missing feature values.

3. Use Data imputation (the process of replacing missing data with substituted values)
    * Replace the missing value with an average value.
    * Replace the missing value with a value outside the normal range.
    * Replace the missing value with a value in the middle of the range.
    * Use the missing value as the target for a regression problem.
    * Increase the dimensionality by adding a binary indicator feature.

### Learning Algorithm Selection

* Explainability
* In-memory vs. out-of-memory (batch or incremental/online)
* Number of features and examples (neural networks for a huge number of features)
* Categorical vs. numerical features
* Nonlinearity of the data (SVM/linear regression/linear kernel/logistic regression of lineraly separable data)
* Training speed (neural networks are slow to train)
* Prediction speed

![scikit-learn cheat sheet](/images/ml_map.png)

### Three Sets

1. Three sets:
    * Training set (95%)
    * Validation set (2.5%): choose the learning algorithm and find the best values of hyperparameters.
    * Test set (2.5%): assess the model before delivery and production.

2. The last two are also called holdout sets, which are not used to build the model.

## References

* [The Hundred-Page Machine Learning Book](https://www.goodreads.com/book/show/43190851-the-hundred-page-machine-learning-book)
