# 📘 NumPy Linear Algebra Knowledge Points

This document covers the key linear algebra utilities available in `numpy.linalg` essential for deep learning applications.

## 1. Norms (Vector and Matrix)

### Vector Norms
A **norm** measures the "size" of a vector $x \in \mathbb{R}^n$:

- **L1 norm**: $\|x\|_1 = \sum_{i=1}^n |x_i|$ (Manhattan distance)
- **L2 norm**: $\|x\|_2 = \sqrt{\sum_{i=1}^n |x_i|^2}$ (Euclidean distance)
- **∞ norm**: $\|x\|_\infty = \max_i |x_i|$ (largest component)

### Matrix Norms
For matrix $A \in \mathbb{R}^{m \times n}$:

- **L1 norm**: $\|A\|_1 = \max_j \sum_i |a_{ij}|$ (max column sum)
- **L2 norm**: $\|A\|_2 = \sigma_{\max}(A)$ (largest singular value)
- **∞ norm**: $\|A\|_\infty = \max_i \sum_j |a_{ij}|$ (max row sum)
- **Frobenius norm**: $\|A\|_F = \sqrt{\sum_{i,j} a_{ij}^2}$ (L2 of all entries)

## 2. Determinant

**Definition**: For square matrix $A \in \mathbb{R}^{n \times n}$, the determinant $\det(A)$ is a scalar.

**Key formulas**:
- $2 \times 2$: $\det\begin{bmatrix}a & b \\ c & d\end{bmatrix} = ad - bc$
- General: Laplace expansion along any row/column

**Geometric meaning**: $|\det(A)|$ = scaling factor for area (2D) or volume (3D) under transformation $A$.

**Properties**:
- $A$ is invertible ⟺ $\det(A) \neq 0$
- $\det(AB) = \det(A) \cdot \det(B)$
- If $\det(A) = 0$, rows/columns are linearly dependent

## 3. Matrix Inverse

**Definition**: For square matrix $A$, the inverse $A^{-1}$ satisfies $A A^{-1} = A^{-1} A = I$.

**Existence**: $A^{-1}$ exists ⟺ $\det(A) \neq 0$ (non-singular matrix).

**Formula (2×2)**:
$$A = \begin{bmatrix} a & b \\ c & d \end{bmatrix} \Rightarrow A^{-1} = \frac{1}{ad-bc} \begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$$

**Properties**:
- $(AB)^{-1} = B^{-1}A^{-1}$
- $(A^T)^{-1} = (A^{-1})^T$
- If $\det(A) = 0$, matrix is singular (no inverse)

## 4. Solve Linear System

**Problem**: Solve $Ax = b$ for unknown vector $x$.

**System types**:
- **Square** ($m = n$): Unique solution if $\det(A) \neq 0$
- **Overdetermined** ($m > n$): More equations than unknowns → least squares
- **Underdetermined** ($m < n$): More unknowns than equations → infinite solutions

**Methods**:
- **Direct**: `np.linalg.solve(A, b)` (most efficient for square systems)
- **Matrix inverse**: $x = A^{-1}b$ (avoid for numerical stability)
- **Least squares**: `np.linalg.lstsq(A, b)` for overdetermined systems

## 5. Eigenvalues and Eigenvectors

**Definition**: For square matrix $A$, find $\lambda$ and $v \neq 0$ such that:
$$Av = \lambda v$$
- $\lambda$: eigenvalue (scaling factor)
- $v$: eigenvector (preserved direction)

**Geometric meaning**: Eigenvectors are special directions that $A$ only stretches/shrinks (no rotation).

**Characteristic equation**: $\det(A - \lambda I) = 0$

**Properties**:
- $n \times n$ matrix has at most $n$ eigenvalues
- $\text{trace}(A) = \sum \lambda_i$, $\det(A) = \prod \lambda_i$
- Symmetric matrices have real eigenvalues and orthogonal eigenvectors

**Applications**: PCA, stability analysis, Google PageRank, quantum mechanics

## 6. Singular Value Decomposition (SVD)

**Core idea:** Any matrix $A \in \mathbb{R}^{m \times n}$ factors as $A = U \Sigma V^T$ with orthogonal $U$ and $V$ and non-negative singular values on the diagonal of $\Sigma$.

**Geometry:** $V^T$ applies a rotation/reflection to the input, $\Sigma$ rescales coordinate axes, and $U$ applies a rotation/reflection to the output—capturing how $A$ stretches vectors.

**Useful facts:**
- Singular values equal $\sqrt{\text{eigenvalues of }A^T A}$
- The number of non-zero $\sigma_i$ gives $\operatorname{rank}(A)$
- Condition number: $\kappa(A) = \sigma_{\max}/\sigma_{\min}$
- SVD exists for every real matrix

**Applications**: PCA (principal components), low-rank approximation, and diagnosing numerical stability in deep models.

## 7. Matrix Rank

**Definition:** Rank counts the number of linearly independent rows/columns; row rank equals column rank and cannot exceed $\min(m,n)$.

**Geometry:** It is the dimension of the subspace spanned by the matrix—full-rank square matrices are invertible ($\det \neq 0$), lower rank means the map collapses dimensions.

**How to compute:** Perform Gaussian elimination, count non-zero singular values (SVD), or call `np.linalg.matrix_rank`.

**Why it matters:** Reveals independent equations in linear systems, the intrinsic dimensionality used in PCA/compression, and whether low-rank weights may restrict deep models.

## 8. Pseudoinverse

**Concept**: Moore–Penrose pseudoinverse, used in underdetermined or overdetermined systems.

**Usage**: For solving least squares problems when $A$ is not square or not invertible.

**Formula**: $A^+ = (A^T A)^{-1} A^T$ (for full-rank case)

**Properties**:
- $A^+ A x = x$ for $x$ in the row space of $A$
- Provides minimum norm solution for underdetermined systems
- Provides least squares solution for overdetermined systems

## 9. QR Decomposition

**Definition:** For $A\in\mathbb{R}^{m\times n}$ with $m\ge n$, factor $A=QR$ with column-orthonormal $Q\in\mathbb{R}^{m\times n}$ and upper-triangular $R\in\mathbb{R}^{n\times n}$.

**Geometry:** $Q$ re-expresses vectors in an orthonormal basis (rotation/reflection); $R$ applies the scaling/combination in that basis.

**Computation:** Classical Gram-Schmidt is instructive but unstable; NumPy uses Householder reflections or Givens rotations for robustness.

**Applications:**
- Solve $Ax=b$ via $QRx=b\Rightarrow Rx=Q^Tb$
- Least-squares fits when $m>n$
- Core step in QR eigenvalue algorithms and other numerically stable routines

## Deep Learning Connections

### Why Linear Algebra Matters in Deep Learning

1. **Neural Network Operations**: Matrix multiplications are fundamental
2. **Weight Matrices**: Linear transformations between layers
3. **Optimization**: Gradients, Hessians, and second-order methods
4. **Regularization**: Norms for controlling model complexity
5. **Dimensionality Reduction**: PCA for preprocessing
6. **Numerical Stability**: Understanding condition numbers and SVD