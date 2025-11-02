# Lecture 17: Orthogonal Matrices and Gram-Schmidt

**Video**: [MIT 18.06 Lecture 17](https://www.youtube.com/watch?v=0MtwqhIwdrI&list=PL221E2BBF13BECF6C&index=37)

## Orthonormal Vectors
Orthonormal vectors are perpendicular to each other and have unit length.

$$
q_i^\top q_j=\begin{cases}0 & \text{if }i\ne j,\\1&\text{if }i=j\end{cases}
$$

This means:
- $q_i \perp q_j$ if $i\neq j$ (orthogonal)
- $||q_i||^2=1 \: \forall i \in \{1,2...n\}$ (normalized)

## Orthonormal Matrices
A matrix Q with orthonormal columns satisfies $Q^\top Q=I_n$.

$$
Q^\top Q=I_n
$$

If Q is square, then $Q^\top=Q^{-1}$ (the transpose equals the inverse).

### Permutation Matrices

$$
Q=\begin{bmatrix}0&0&1\\1&0&0\\0&1&0\end{bmatrix}
$$

### Rotation Matrix

$$
Q=\begin{bmatrix}\cos\theta&-\sin\theta\\ \sin\theta&\cos\theta \end{bmatrix}
$$

### Hadamard Matrix

$$
Q=\frac{1}{\sqrt{2}}\begin{bmatrix}1&1\\1&-1\end{bmatrix}
$$

$$
Q=\frac{1}{\sqrt{4}}\begin{bmatrix}1&1&1&1\\1&-1&1&-1\\1&1&-1&-1\\1&-1&-1&1\end{bmatrix}
$$

### Projection onto Orthonormal Matrices
When Q has orthonormal columns, the projection matrix simplifies significantly.

$$
P=Q(Q^\top Q)^{-1}Q^\top=QQ^\top=\begin{cases}I \; \text{if } Q \text{ is square }\\
\end{cases}
$$

- Proof of the 2 key properties:
	- Symmetric
		- $QQ^\top$ is symmetric
	- Idempotent

$$
(QQ^\top)(QQ^\top)=QIQ^\top=QQ^\top
$$

- Least squares simplification

$$
A^\top A\hat{x}=A^\top b
$$

If A is an orthonormal matrix Q, the solution becomes trivial:

$$
Q^\top Q \hat{x}=Q^\top b \\
\hat{x}=Q^\top b \\
\hat{x_i}={Q_i}^\top b
$$

Each component is simply the projection of b onto the corresponding column of Q.

## Gram-Schmidt
The Gram-Schmidt process converts independent vectors into orthonormal vectors.

Given 2 independent vectors a and b:
- $q_1=\frac{A}{||A||}$
- $q_2=\frac{B}{||B||}$

### 2D Case

![orthonormal-gram-2d](orthonormal-gram-2d.png)

Set a as A (no change needed for the first vector).
We then remove the projection of b onto a from b, using the error component as B.
This ensures $A \perp B$.

$$
B=b-\frac{A^\top b}{A^\top A}A
$$

- Proof

$$
A^\top B=A^\top b-A^\top A\frac{A^\top b}{A^\top A}=0
$$

### 3D Case
At this point, we have orthogonal vectors A and B, and we find C by removing its projections onto both A and B.

$$
q_3=\frac{C}{||C||}
$$

$$
C=c-\frac{A^\top c}{A^\top A}A-\frac{B^\top c}{B^\top B}B
$$

$$
C \perp A \text{ and } C\perp B
$$

![orthonomal-gram-schdimt-3d](orthonomal-gram-schdimt-3d.png)

### Real Example
Given:
- $a=\begin{bmatrix}1\\1\\1\end{bmatrix}$

$$
b=\begin{bmatrix}1\\0\\2\end{bmatrix}
$$

The original matrix M is:

$$
M=\begin{bmatrix}1&1\\1&0\\1&2\end{bmatrix}
$$

Use a as A, then calculate B:

$$
B=b-\frac{A^\top b}{A^\top A}A=\\
b-\frac{3}{3}A=\\
\begin{bmatrix}0\\-1\\1\end{bmatrix}
$$

- Set up Q matrix
	- Q_1

$$
\frac{\begin{bmatrix}1\\1\\1\end{bmatrix}}{\sqrt{3}}=\begin{bmatrix}\frac{1}{\sqrt{3}}\\\frac{1}{\sqrt{3}}\\\frac{1}{\sqrt{3}}\end{bmatrix}
$$

- Q_2

$$
\frac{\begin{bmatrix}0\\-1\\1\end{bmatrix}}{\sqrt{2}}=\begin{bmatrix}0\\\frac{-1}{\sqrt{2}}\\\frac{1}{\sqrt{2}}\end{bmatrix}
$$

$$
Q=\begin{bmatrix}\frac{1}{\sqrt{3}}&0\\\frac{1}{\sqrt{3}}&\frac{-1}{\sqrt{2}}\\\frac{1}{\sqrt{3}}&\frac{1}{\sqrt{2}}\end{bmatrix}
$$

### QR Factorization
Q spans the same column space as M, so we can write $M=QR$.
- Q is m×n (orthonormal columns)
- R is n×n (upper triangular)

Because Q is orthonormal:

$$
Q^\top M=R\\
r_{ij}=Q^\top_iM_j
$$

$$
\begin{bmatrix}|&|\\a_1&a_2\\|&|\end{bmatrix}=\begin{bmatrix}q_1&q_2\end{bmatrix}\begin{bmatrix}a_1^\top q_1&*\\a_1^\top q_2 &*\end{bmatrix}
$$

Because $q_1 \perp q_2$, we have $q_1^\top a_2=0$ in the lower left position, making R upper triangular.
