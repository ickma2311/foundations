# Chapter 6.5 - Backpropagation and the Chain Rule

## 1. Chain Rule in Vector Form
- Composite mapping $z = f(y), \; y = g(x)$ yields a gradient $\nabla_x z = \left( \frac{\partial y}{\partial x} \right)^{\top} \nabla_y z$.
- In a neural network, each layer contributes its local Jacobian; multiplying them propagates gradients backward.
- This matrix-product structure keeps the computation tractable even in high dimensions.

---

## 2. Back-Propagation Algorithm
- **Forward pass**: $h^{(l)} = f^{(l)}(W^{(l)} h^{(l-1)} + b^{(l)})$ caches activations and pre-activations.
- **Backward pass**: $\nabla_{h^{(l-1)}} L = (W^{(l)})^{\top} (\nabla_{h^{(l)}} L \odot f'^{(l)}(z^{(l)}))$.
- **Parameter gradients**: $\frac{\partial L}{\partial W^{(l)}} = (\nabla_{h^{(l)}} L \odot f'^{(l)}(z^{(l)})) (h^{(l-1)})^{\top}$.
- Key properties:
  - Reuses intermediate activations from the forward pass.
  - Avoids building full Jacobian matrices while delivering the same result.
  - Implements reverse-mode automatic differentiation.

---

## 3. Computational Graph Perspective
- Nodes represent intermediate variables and operations within a directed acyclic graph.
- Backprop traverses this graph in reverse topological order to accumulate gradients.
- Each node aggregates incoming influence: $\bar{x}_i = \sum_{j \in \text{children}(i)} \bar{x}_j \frac{\partial x_j}{\partial x_i}$.
- This view extends seamlessly to MLPs, CNNs, RNNs, residual links, and shared-weight architectures.

---

## Clarifying the Intuition
- **Optimization target**: training seeks the loss minimum, not zero network outputs.
- **Parameter space**: each weight is a dimension on a high-dimensional error surface, and gradient descent steers movement along that surface.
- **Coupled updates**: the global gradient step updates all parameters simultaneously based on their individual partial derivatives.
- **Local-to-global chain**: every parameter’s gradient equals its local derivative multiplied by accumulated downstream gradients.
