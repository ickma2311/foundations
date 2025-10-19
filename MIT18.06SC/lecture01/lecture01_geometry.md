# MIT 18.06 Lecture 1: The Geometry of Linear Equations

**Video Lecture**: [MIT 18.06 Lecture 1 - The Geometry of Linear Equations](https://www.youtube.com/watch?v=J7DzL2_Na80&list=PL221E2BBF13BECF6C&index=3)

This document covers the fundamental geometric interpretation of linear algebra, introducing the row picture and column picture perspectives of linear systems.

## Key Concepts

Let's explore the same linear system from two different geometric perspectives using a concrete example.

### Linear Algebra Introduction
- Linear algebra studies systems of linear equations and matrices.
- The central object: the matrix, representing both equations (rows) and vectors (columns).

### Row Picture
- Each equation is a line (in 2D) or plane (in higher dimensions).
- The solution corresponds to the intersection point(s) of those lines/planes.

**Example**: Consider the system:
$$\begin{align}
x + 2y &= 5 \\
3x + 4y &= 6
\end{align}$$

**Row Picture Interpretation**:
- Equation 1: Line $x + 2y = 5$ (slope = -1/2, y-intercept = 5/2)
- Equation 2: Line $3x + 4y = 6$ (slope = -3/4, y-intercept = 3/2)
- Solution: Intersection point where both equations are satisfied

### Column Picture
- Rewrite the system as a linear combination of columns:
$$A \cdot x = b \quad \Leftrightarrow \quad x_1 \cdot a_1 + x_2 \cdot a_2 = b$$
- A solution exists if and only if $b$ lies in the column space (span of columns).

**Example**: Same system rewritten:
$$x \begin{bmatrix}1 \\ 3\end{bmatrix} + y \begin{bmatrix}2 \\ 4\end{bmatrix} = \begin{bmatrix}5 \\ 6\end{bmatrix}$$

**Column Picture Interpretation**:
- Column 1: Vector $\begin{bmatrix}1 \\ 3\end{bmatrix}$ scaled by $x$
- Column 2: Vector $\begin{bmatrix}2 \\ 4\end{bmatrix}$ scaled by $y$
- Question: Can we combine these vectors to reach $\begin{bmatrix}5 \\ 6\end{bmatrix}$?
- Solution: Find coefficients $x, y$ such that the linear combination equals $b$

### Possible Outcomes of a Linear System
- **Unique solution**: intersection at one point.
- **No solution**: parallel lines (inconsistent system).
- **Infinitely many solutions**: overlapping lines (dependent equations).

### Matrix Notation
- Compact representation:
$$A \begin{bmatrix}x \\ y\end{bmatrix} = b$$
- Bridges algebraic computation with geometric interpretation.