# MIT 18.06SC — Lecture 2: Elimination (Gaussian Elimination)

## 📚 Key Concepts

### 1. Goal of Elimination
- Solve the linear system $Ax = b$.
- Transform $A$ into an upper triangular matrix $U$ by forward elimination.
- Solve unknowns with back substitution.

---

### 2. Steps of Elimination
1. Choose a pivot (usually a diagonal entry).
2. Eliminate entries below the pivot using row operations.
   - Formula:
     $$\text{Row}_i \;\;\leftarrow\;\; \text{Row}_i - m_{ij} \cdot \text{Row}_j$$
   - Multiplier:
     $$m_{ij} = \frac{a_{ij}}{\text{pivot}}$$
3. Repeat for the next column.
4. Back substitution: solve from the last row upward.

---

### 3. Example

System:
$$\begin{cases}
2u + v + w = 5 \\
4u - 6v = -2 \\
-2u + 7v + 2w = 9
\end{cases}$$

- Pivot: $a_{11} = 2$.
- Eliminate $a_{21} = 4$:
  $$m_{21} = \frac{4}{2} = 2$$
  Row operation:
  $$\text{Row}_2 \;\;\leftarrow\;\; \text{Row}_2 - 2\cdot \text{Row}_1$$
- Continue until upper triangular system:
  $$\begin{cases}
  2u + v + w = 5 \\
  -8v - 2w = -12 \\
  w = 2
  \end{cases}$$
- Back substitution: $w = 2$, $v = 1$, $u = 1$.

---

### 4. Elementary Elimination Matrices
- Each row operation can be written as multiplication by an elementary elimination matrix $E_{ij}$.
- General form:
  $$E_{ij} = I - m_{ij} e_{ij}$$
  where:
  - $m_{ij} = \dfrac{a_{ij}}{\text{pivot}}$
  - $e_{ij}$: matrix with 1 at position $(i,j)$, 0 elsewhere.

#### Example

Matrix:
$$A =
\begin{bmatrix}
2 & 1 \\
4 & -6
\end{bmatrix}$$

- Pivot: $a_{11} = 2$, entry to eliminate: $a_{21} = 4$.
- Multiplier: $m_{21} = \frac{4}{2} = 2$.
- Elimination matrix:
  $$E_{21} =
  \begin{bmatrix}
  1 & 0 \\
  -2 & 1
  \end{bmatrix}$$
  (Note: the entry is $-m_{21}$ because the row operation is $\text{Row}_2 - m_{21}\cdot \text{Row}_1$.)

Check:
$$E_{21} A =
\begin{bmatrix}
2 & 1 \\
0 & -8
\end{bmatrix}$$

✅ The element $a_{21}$ is eliminated.
