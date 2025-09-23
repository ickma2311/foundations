# Deep Learning — Chapter 6.1: Example: Learning XOR

## Key Takeaways

1. **Non-linear transformations are essential**
   - Many problems, such as the XOR function, cannot be solved with a purely linear model.
   - Non-linear activation functions (e.g., sigmoid, tanh, ReLU) provide the flexibility to capture non-linear decision boundaries.

2. **Stacking linear layers is still linear**
   - A composition of multiple linear transformations is mathematically equivalent to a single linear transformation.
   - Therefore, even with more layers, a network without non-linear activations cannot solve tasks like XOR.

3. **Complex functions arise from chaining simple rules**
   - By introducing non-linear activations between layers, neural networks can combine simple linear operations into powerful function approximators.
   - This shows how deep networks, built from simple building blocks, can represent highly complex decision functions.

---

✅ **Summary:**
Section 6.1 illustrates with the XOR problem that **non-linearity is the key ingredient** enabling neural networks to model functions that are impossible for linear models. This motivates the use of activation functions and highlights the expressive power of deep architectures.