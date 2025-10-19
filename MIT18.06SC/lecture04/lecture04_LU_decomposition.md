# Lecture 4: LU Decomposition (A = LU)

**Video Lecture**: [MIT 18.06 Lecture 4 - Factorization into A = LU](https://www.youtube.com/watch?v=MsIvs_6vC38&list=PL221E2BBF13BECF6C&index=11)

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

## 🎓 Key Takeaways

1. **Multiplying a matrix by elimination matrices yields an upper-triangular $U$**,
   hence $A = LU$, where $L = (\text{product of elimination matrices})^{-1}$.

2. **Practice small casses (2×2, 3×3)** to build intuition for how $L$ and $U$ form.

3. **Each elimination keeps the pivot row fixed** and modifies rows below it:
   - $E_{ij} = I - m_{ij} \mathbf{e}_i \mathbf{e}_j^T$
   - $(i,j)$ element of $E_{ij}$ is $-m_{ij}$.

4. **Complexity ≈ $\frac{n^3}{3}$** because each step updates a smaller submatrix.

5. **LU is valuable when $A$ stays constant but $b$ changes** — reuse saves cost:
   - Decomposition: $O(n^3)$
   - Solving $(LU)x = b$: $O(n^2)$
