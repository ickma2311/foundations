# Chapter 6.4 - Expressive Power of Deep Networks

## Why It Matters
- ReLU and Maxout networks compute piecewise-linear functions of their inputs.
- Every ReLU introduces a hyperplane that partitions the input space into regions with different linear maps.
- Increasing depth compounds these partitions, producing exponentially many regions that expand expressivity.

---

## Region Counts by Depth
- Deep network with width \(n\) and depth \(L\): \(\mathcal{O}(n^{L})\) distinct linear regions.
- Shallow network with a single hidden layer needs \(\mathcal{O}(n^{L})\) units to match that expressivity.
- Depth enables feature reuse, while a flat architecture must allocate a separate unit for each region it wishes to carve out.

---

## Theoretical Support
- **Universal Approximation Theorem**: even a single hidden layer can approximate any continuous function on a compact set.
- **Limitation**: the unit count for shallow nets grows exponentially with input dimensionality or target complexity.
- **Deep Advantage**: layered compositions realise the same functions with polynomially many units by reusing intermediate features.

---

## Intuitive Picture
- Shallow network: few linear regions; partitions resemble simple, axis-aligned cuts across the input.
- Deep network: successive splits yield complex boundaries that bend and fold space, knitting many small linear maps together.
- 1D viewpoint: stacking layers creates finely segmented piecewise-linear curves versus the coarse segments from a single hidden layer.
- 2D viewpoint: deep models tile the plane with numerous interlocking polytopes, whereas shallow models span only a handful of broad cells.

---

## Analogy
- Deep network: writing a program with well-structured functions that reuse computations.
- Shallow network: expressing the same logic in one line, which works but bloats the code size (model parameters).
