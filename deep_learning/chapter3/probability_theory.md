# 📘 Probability and Information Theory — Knowledge Points

Use this chapter to review core probability tools that appear throughout modern deep learning. Concepts are paired with exercises so you can implement the ideas in code.

## 1. Probability Basics

- Random variables: discrete vs. continuous
- Probability distributions:
  - Probability Mass Function (PMF)
  - Probability Density Function (PDF)
- Key rules:
  - Joint probability $P(X, Y)$
  - Marginal probability $P(X)$
  - Conditional probability $P(X\mid Y)$
  - Independence and conditional independence

## 2. Common Distributions

- **Bernoulli**: binary outcomes
- **Binomial**: number of successes in fixed trials
- **Multinomial**: multi-class outcomes
- **Gaussian (Normal)**: continuous, bell-shaped
- **Poisson** and **Exponential**: rare events, waiting times

## 3. Expectation and Variance

- **Expectation** (mean): average value of a random variable
  $\displaystyle \mathbb{E}[X] = \sum_x x P(x)$ (discrete),
  $\displaystyle \mathbb{E}[X] = \int x p(x)\,dx$ (continuous)
- **Variance**: measure of spread around the mean
  $\displaystyle \text{Var}(X) = \mathbb{E}[(X - \mathbb{E}[X])^2]$
- **Covariance and correlation**: measure linear relationships between two variables

## 4. Bayes' Theorem

$\displaystyle P(A\mid B) = \frac{P(B\mid A)P(A)}{P(B)}$

- Updates belief about event $A$ given evidence $B$
- Foundation of Bayesian inference

## 5. Information Theory

- Information content: $I(x) = -\log P(x)$
- Entropy: $H(X) = -\sum_x P(x)\log P(x)$
- Conditional entropy: $H(X\mid Y)$
- Cross-entropy: $H(P, Q) = -\sum_x P(x)\log Q(x)$
- KL divergence: $D_{KL}(P\Vert Q) = \sum_x P(x) \log \frac{P(x)}{Q(x)}$

## 6. Applications in Machine Learning

- Maximum Likelihood Estimation (MLE)
- Bayesian inference
- Loss functions based on information theory:
  - Cross-entropy loss
  - KL divergence (e.g., in variational inference)
- Probabilistic modeling of uncertainty