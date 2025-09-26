# Chapter 6.2 – Likelihood-Based Losses

## Core Principles
- **Loss mirrors likelihood.** Choose the negative log-likelihood (NLL) of an observation model so that training solves
  $$
  \theta^{\star} = \arg\min_\theta \; \mathbb{E}_{(x,y)}\big[-\log p_\theta(y \mid x)\big],
  $$
  aligning optimisation with probabilistic assumptions.
- **Regression ↔ Gaussian noise.** Linear outputs with fixed-variance Gaussian likelihood recover mean-squared error:
  $$
  p(y \mid x) = \mathcal{N}(y; \hat{y}, \sigma^2 I) \quad \Rightarrow \quad -\log p(y \mid x) = \frac{1}{2\sigma^2}\|y-\hat{y}\|_2^2 + \text{const}.
  $$
  Allowing the network to predict \(\sigma^2(x)\) yields heteroscedastic regression.
- **Binary classification ↔ Bernoulli.** A sigmoid converts logits \(z\) to probabilities \(\sigma(z)\), and the Bernoulli NLL becomes binary cross-entropy:
  $$
  p(y \mid x) = \operatorname{Bernoulli}(y; \sigma(z)) \Rightarrow -\log p(y \mid x) = -y\log\sigma(z) -(1-y)\log\big(1-\sigma(z)\big).
  $$
- **Multiclass classification ↔ categorical.** Softmax converts logits to class probabilities and the NLL is the usual cross-entropy:
  $$
  p(y=i \mid x) = \frac{e^{z_i}}{\sum_j e^{z_j}} \Rightarrow -\log p(y \mid x) = -\log \frac{e^{z_y}}{\sum_j e^{z_j}}.
  $$

## Activation–Likelihood Matching
| Task | Observation model | Output activation | Loss (NLL) |
|------|-------------------|-------------------|------------|
| Regression | Gaussian $\mathcal{N}(\hat{y}, \sigma^2 I)$ | Linear $f(z)=z$ | Mean-squared error |
| Binary classification | Bernoulli $\operatorname{Bern}(\sigma(z))$ | Sigmoid $\sigma(z)=1/(1+e^{-z})$ | Binary cross-entropy |
| Multiclass classification | Categorical / softmax $\operatorname{Cat}(\text{softmax}(z))$ | Softmax $\text{softmax}(z)_i = e^{z_i}/\sum_j e^{z_j}$ | Cross-entropy |

## Common Activation Functions
- **Sigmoid** $\sigma(z) = 1 / (1 + e^{-z})$: squashes to $(0,1)$, interpretable as probabilities.
- **Hyperbolic tangent** $\tanh(z) = \frac{e^{z} - e^{-z}}{e^{z} + e^{-z}}$: zero-centred range $(-1,1)$, useful for symmetric outputs.
- **Rectified Linear Unit (ReLU)** $\operatorname{ReLU}(z) = \max(0, z)$: piecewise-linear, alleviates vanishing gradients.
- **Softmax** $\text{softmax}(z)_i = e^{z_i}/\sum_j e^{z_j}$: converts logits into a categorical distribution.
- **Linear** $f(z) = z$: identity activation for unconstrained regression targets.

## Mental Model
Think of the network as learning sufficient statistics for the chosen distribution. Swapping the observation model swaps only the final activation and loss, while earlier layers remain reusable feature extractors.
