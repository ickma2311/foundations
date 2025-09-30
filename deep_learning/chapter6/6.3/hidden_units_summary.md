# Chapter 6.3 – Hidden Units (Activation Functions)

## Key Idea
- Hidden units shape the non-linear transformation of inputs, letting deep networks approximate complex functions instead of collapsing into a single linear map.
- Choosing an activation function is equivalent to specifying how each layer warps its incoming representation.

---

## Covered Topics

### 1. Role of Activation Functions
- Introduce non-linearity into the network.
- Enable hierarchical composition of features across layers.

### 2. Sigmoid Units
- Formula: $\sigma(x) = 1 / (1 + e^{-x})$.
- Pros: probabilistic interpretation, smooth output in $(0,1)$.
- Cons: saturation causes vanishing gradients, not zero-centred.
- Typical use: binary classification outputs.

### 3. Hyperbolic Tangent (tanh)
- Formula: $\tanh(x) = \frac{e^{x} - e^{-x}}{e^{x} + e^{-x}}$.
- Benefit: zero-centred activations.
- Limitation: still saturates, leading to slow learning.

### 4. Rectified Linear Unit (ReLU)
- Formula: $f(x) = \max(0, x)$.
- Advantages: computationally cheap, sparse activations, mitigates vanishing gradients.
- Issue: neurons can "die" (output stuck at zero).

### 5. Softplus
- Smooth approximation to ReLU: $f(x) = \log(1 + e^{x})$.
- Retains non-linearity while avoiding hard zeroing.

### 6. Maxout Units
- Generalises ReLU/linear units: $f(x) = \max_{j \in G} (w_j^{\top} x + b_j)$.
- Learns piecewise-linear convex functions.
- Highly flexible but increases parameter count.

---

## Practical Notes
- ReLU and its variants are the default choice for hidden layers.
- Sigmoid/tanh are mainly used in output layers or specialised architectures (e.g. gating in RNNs/LSTMs).
- Maxout pairs well with dropout when extra flexibility is worth the parameter cost.

---

## Takeaway
Section 6.3 emphasises that designing hidden units means choosing an activation function, which directly controls optimisation dynamics, gradient flow, and the expressive power of the network.
