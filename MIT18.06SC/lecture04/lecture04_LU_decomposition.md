# Lecture 4: LU Decomposition (A = LU)

Gilbert Strang — MIT 18.06 Linear Algebra
**Topic:** Factoring matrices into **Lower × Upper** triangular form

---

## 🎯 What is LU Decomposition?

**Goal:** Factor any invertible matrix $A$ as the product of:
- $L$ = **Lower triangular** matrix (with 1's on diagonal)
- $U$ = **Upper triangular** matrix (the result of elimination)

$$
A = LU
$$

**Why is this useful?**
- Solving $Ax = b$ becomes two simpler triangular solves: $Lc = b$, then $Ux = c$
- When $A$ is fixed but $b$ changes, reuse $L$ and $U$ → huge savings!
- Foundational for numerical linear algebra (MATLAB, NumPy, etc.)

---

## 🔨 How Elimination Creates U

### Elimination Process

Starting with $A$, we apply elimination matrices $E_{21}, E_{31}, E_{32}, \ldots$ to get upper triangular $U$:

$$
E_{32} E_{31} E_{21} A = U
$$

**Example (3×3 case):**

$$
A = \begin{bmatrix} 2 & 1 & 1 \\ 4 & -6 & 0 \\ -2 & 7 & 2 \end{bmatrix}
$$

**Step 1:** Eliminate below first pivot (row 2 and row 3)

$$
E_{21} = \begin{bmatrix} 1 & 0 & 0 \\ -2 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}, \quad
E_{31} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 1 & 0 & 1 \end{bmatrix}
$$

**Step 2:** Eliminate below second pivot (row 3)

$$
E_{32} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & -1 & 1 \end{bmatrix}
$$

Then:

$$
E_{32} E_{31} E_{21} A = U
$$

---

## 📐 Structure of Elimination Matrices

An elimination matrix $E_{ij}$ eliminates the entry at position $(i,j)$ by subtracting a multiple of row $j$ from row $i$.

### General Form

$$
E_{ij} = I - m_{ij} \mathbf{e}_i \mathbf{e}_j^T
$$

where:
- $m_{ij}$ = multiplier = $\frac{A_{ij}}{\text{pivot at } (j,j)}$
- $\mathbf{e}_i$ = $i$-th standard basis vector
- The $(i,j)$ entry of $E_{ij}$ is $-m_{ij}$

### Properties

1. **Lower triangular** (operates below diagonal)
2. **Determinant = 1** (doesn't change volume)
3. **Inverse is simple:** $E_{ij}^{-1} = I + m_{ij} \mathbf{e}_i \mathbf{e}_j^T$ (just flip the sign!)

---

## 🔄 Inverting to Get L

From elimination, we have:

$$
E_{n,n-1} \cdots E_{32} E_{31} E_{21} A = U
$$

Multiply both sides by the inverses (in reverse order):

$$
A = E_{21}^{-1} E_{31}^{-1} E_{32}^{-1} \cdots U = LU
$$

where:

$$
L = E_{21}^{-1} E_{31}^{-1} E_{32}^{-1} \cdots
$$

### Key Insight: L is Simple!

When elimination matrices are multiplied in the right order, their **inverses combine beautifully**:

$$
L = \begin{bmatrix}
1 & 0 & 0 & \cdots \\
m_{21} & 1 & 0 & \cdots \\
m_{31} & m_{32} & 1 & \cdots \\
\vdots & \vdots & \ddots & \ddots
\end{bmatrix}
$$

The multipliers $m_{ij}$ (used during elimination) **directly fill in** the entries of $L$ below the diagonal!

**No extra computation needed** — just save the multipliers as you eliminate.

---

## 📊 Example: 3×3 LU Decomposition

### Original Matrix

$$
A = \begin{bmatrix} 2 & 1 & 1 \\ 4 & -6 & 0 \\ -2 & 7 & 2 \end{bmatrix}
$$

### Elimination Steps

**Step 1:** Eliminate column 1
- $m_{21} = \frac{4}{2} = 2$, subtract 2×(row 1) from row 2
- $m_{31} = \frac{-2}{2} = -1$, subtract -1×(row 1) from row 3

$$
A \to \begin{bmatrix} 2 & 1 & 1 \\ 0 & -8 & -2 \\ 0 & 8 & 3 \end{bmatrix}
$$

**Step 2:** Eliminate column 2
- $m_{32} = \frac{8}{-8} = -1$, subtract -1×(row 2) from row 3

$$
U = \begin{bmatrix} 2 & 1 & 1 \\ 0 & -8 & -2 \\ 0 & 0 & 1 \end{bmatrix}
$$

### Lower Triangular Matrix L

Collect the multipliers:

$$
L = \begin{bmatrix} 1 & 0 & 0 \\ 2 & 1 & 0 \\ -1 & -1 & 1 \end{bmatrix}
$$

### Verification

$$
LU = \begin{bmatrix} 1 & 0 & 0 \\ 2 & 1 & 0 \\ -1 & -1 & 1 \end{bmatrix}
\begin{bmatrix} 2 & 1 & 1 \\ 0 & -8 & -2 \\ 0 & 0 & 1 \end{bmatrix}
= \begin{bmatrix} 2 & 1 & 1 \\ 4 & -6 & 0 \\ -2 & 7 & 2 \end{bmatrix} = A \quad ✓
$$

---

## ⚡ Computational Complexity

### Operation Counts

For an $n \times n$ matrix:

| Step | Operations | Order |
|------|-----------|-------|
| **Elimination (find U)** | $\frac{n^3}{3} + O(n^2)$ | $O(n^3)$ |
| **Forward substitution** $(Lc = b)$ | $\frac{n^2}{2}$ | $O(n^2)$ |
| **Back substitution** $(Ux = c)$ | $\frac{n^2}{2}$ | $O(n^2)$ |

### Why $\frac{n^3}{3}$?

At step $k$, we update an $(n-k) \times (n-k)$ submatrix:

$$
\text{Total operations} = \sum_{k=1}^{n-1} (n-k)^2 \approx \int_0^n x^2 \, dx = \frac{n^3}{3}
$$

### When is LU Worth It?

**Single solve:** $Ax = b$ costs $O(n^3)$ either way

**Multiple solves:** If solving $Ax = b_1, Ax = b_2, \ldots, Ax = b_m$:
- **Without LU:** $m \times O(n^3)$
- **With LU:** $O(n^3)$ (once) + $m \times O(n^2)$ ✅

**Huge savings when $A$ is fixed but $b$ changes!**

---

## 🔀 Partial Pivoting: PA = LU

### When Does LU Fail?

LU decomposition **without row exchanges** fails if we encounter a **zero pivot**.

**Example:**

$$
A = \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}
$$

- First pivot is 0 → cannot divide!
- Need to **swap rows**

### Solution: Permutation Matrix

Introduce a **permutation matrix** $P$ that records row swaps:

$$
PA = LU
$$

where:
- $P$ = product of row exchange matrices
- $L$ = lower triangular (with 1's on diagonal)
- $U$ = upper triangular

### Properties of P

- $P$ is an **identity matrix with rows permuted**
- $P^T P = I$ (orthogonal)
- $P^{-1} = P^T$

### Partial Pivoting Strategy

At each step, choose the **largest available pivot** (in absolute value) to minimize numerical errors.

**Example:**

$$
A = \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}
\quad \Rightarrow \quad
P = \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}, \quad
PA = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = LU
$$

---

## 🧮 Solving $Ax = b$ Using LU

### Two-Step Process

Given $A = LU$ and $Ax = b$:

**Step 1:** Forward substitution — solve $Lc = b$ for $c$

$$
\begin{bmatrix}
1 & 0 & 0 \\
m_{21} & 1 & 0 \\
m_{31} & m_{32} & 1
\end{bmatrix}
\begin{bmatrix} c_1 \\ c_2 \\ c_3 \end{bmatrix}
= \begin{bmatrix} b_1 \\ b_2 \\ b_3 \end{bmatrix}
$$

Solve top to bottom:
- $c_1 = b_1$
- $c_2 = b_2 - m_{21}c_1$
- $c_3 = b_3 - m_{31}c_1 - m_{32}c_2$

**Step 2:** Back substitution — solve $Ux = c$ for $x$

$$
\begin{bmatrix}
u_{11} & u_{12} & u_{13} \\
0 & u_{22} & u_{23} \\
0 & 0 & u_{33}
\end{bmatrix}
\begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix}
= \begin{bmatrix} c_1 \\ c_2 \\ c_3 \end{bmatrix}
$$

Solve bottom to top:
- $x_3 = c_3 / u_{33}$
- $x_2 = (c_2 - u_{23}x_3) / u_{22}$
- $x_1 = (c_1 - u_{12}x_2 - u_{13}x_3) / u_{11}$

---

## 🎓 Key Takeaways

### Main Ideas

1. **LU decomposition factors $A = LU$** where:
   - $L$ = lower triangular (multipliers from elimination)
   - $U$ = upper triangular (result of elimination)

2. **L is "free"** — just save the multipliers during elimination

3. **Complexity is $O(n^3/3)$** for factorization, but only $O(n^2)$ to solve once factored

4. **Reusable:** When $A$ stays constant but $b$ changes, LU saves enormous time

5. **Partial pivoting ($PA = LU$)** ensures numerical stability

### Practical Use

```python
# In NumPy/SciPy:
from scipy.linalg import lu

P, L, U = lu(A)  # Get P, L, U such that A = P @ L @ U
```

---

## 📝 Practice Problems

1. Compute the LU decomposition of $\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}$ by hand

2. For $A = \begin{bmatrix} 2 & 1 & 1 \\ 4 & -6 & 0 \\ -2 & 7 & 2 \end{bmatrix}$, verify $A = LU$ with the matrices from the example

3. Explain why LU fails for $\begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}$ and show how $PA = LU$ fixes it

4. Count the operations for solving 10 systems $Ax = b_i$ ($i = 1, \ldots, 10$) with and without LU

5. Given $L = \begin{bmatrix} 1 & 0 \\ 2 & 1 \end{bmatrix}$ and $U = \begin{bmatrix} 3 & 1 \\ 0 & 2 \end{bmatrix}$, solve $LUx = \begin{bmatrix} 7 \\ 10 \end{bmatrix}$

---

**Next:** Lecture 5 — Permutations, Transposes, and Vector Spaces
