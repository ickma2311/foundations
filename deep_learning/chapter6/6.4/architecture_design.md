# Chapter 6.4 — Architecture Design

## 🎯 Main Idea
- Choosing the right architecture (depth, width, connectivity) is a crucial part of designing feedforward networks.
- There is no universal rule; instead, design depends on task, data, and computational constraints.

---

## 🧱 Key Knowledge Points

### 1. Depth vs. Width
- Depth allows networks to reuse features hierarchically.
- Width can also increase capacity, but often inefficient compared to depth.
- Excessive depth may cause optimization difficulties (vanishing/exploding gradients).

---

### 2. Expressive Power
- Deep networks can represent functions with exponentially fewer units than shallow ones.
- ReLU/Maxout networks partition the input into many piecewise linear regions, growing exponentially with depth.
- Shallow networks require exponential growth in width to match the expressive power of deep architectures.

#### Why It Matters
- ReLU and Maxout networks compute piecewise-linear functions of their inputs.
- Every ReLU introduces a hyperplane that partitions the input space into regions with different linear maps.
- Increasing depth compounds these partitions, producing exponentially many regions that expand expressivity.

#### Region Counts by Depth
- Deep network with width $n$ and depth $L$: $\mathcal{O}(n^{L})$ distinct linear regions.
- Shallow network with a single hidden layer needs $\mathcal{O}(n^{L})$ units to match that expressivity.
- Depth enables feature reuse, while a flat architecture must allocate a separate unit for each region it wishes to carve out.

#### Theoretical Support
- **Universal Approximation Theorem**: even a single hidden layer can approximate any continuous function on a compact set.
- **Limitation**: the unit count for shallow nets grows exponentially with input dimensionality or target complexity.
- **Deep Advantage**: layered compositions realise the same functions with polynomially many units by reusing intermediate features.

#### Intuitive Picture
- Shallow network: few linear regions; partitions resemble simple, axis-aligned cuts across the input.
- Deep network: successive splits yield complex boundaries that bend and fold space, knitting many small linear maps together.
- 1D viewpoint: stacking layers creates finely segmented piecewise-linear curves versus the coarse segments from a single hidden layer.
- 2D viewpoint: deep models tile the plane with numerous interlocking polytopes, whereas shallow models span only a handful of broad cells.

#### Analogy
- Deep network: writing a program with well-structured functions that reuse computations.
- Shallow network: expressing the same logic in one line, which works but bloats the code size (model parameters).

---

### 3. Practical Design Guidelines
- Start with architectures known to work well (e.g., convolutional nets for images, recurrent nets for sequences).
- Use domain knowledge (translation invariance, locality, sequential structure) to guide architecture choice.
- Often, it is better to rely on empirical search (hyperparameter tuning, validation performance) than pure theory.

---

### 4. Trade-offs
- More depth → higher expressive power, but harder to train.
- More width → easier optimization but may require more units/parameters.
- Computational cost, training stability, and generalization must all be considered.
