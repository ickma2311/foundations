# 🧮 PCA and Linear Algebra (Deep Learning Book - Chapter 2)

## Background
Chapter 2 of *Deep Learning* (Goodfellow, Bengio, Courville) emphasizes the role of **linear algebra** in machine learning. One important application is **Principal Component Analysis (PCA)**, which relies on **eigenvalues/eigenvectors** or **singular value decomposition (SVD)** to reduce dimensionality while preserving as much variance as possible.

## Key Concepts

### What is PCA?
Principal Component Analysis (PCA) is a dimensionality reduction technique that:
- Finds the directions (principal components) of maximum variance in data
- Projects data onto a lower-dimensional subspace
- Preserves as much information as possible while reducing dimensions

### Mathematical Foundation

#### 1. Data Centering
First, center the data by subtracting the mean:
$$X_{\text{centered}} = X - \mu$$
where $\mu$ is the mean of each feature.

#### 2. Covariance Matrix
Compute the covariance matrix of the centered data:
$$C = \frac{1}{n-1} X_{\text{centered}}^T X_{\text{centered}}$$

#### 3. Eigendecomposition
Find eigenvalues and eigenvectors of the covariance matrix:
$$C v_i = \lambda_i v_i$$
where:
- $\lambda_i$ are eigenvalues (variance along each principal component)
- $v_i$ are eigenvectors (directions of principal components)

#### 4. Principal Components
- **First Principal Component**: Eigenvector with largest eigenvalue (direction of maximum variance)
- **Second Principal Component**: Eigenvector with second largest eigenvalue, orthogonal to first
- And so on...

#### 5. Dimensionality Reduction
Project data onto top $k$ principal components:
$$X_{\text{reduced}} = X_{\text{centered}} \cdot V_k$$
where $V_k$ contains the top $k$ eigenvectors.

### Interpretation

#### Geometric View
- PCA finds a new coordinate system where data variance is maximized
- Principal components are orthogonal axes in this new system
- First component captures most variance, second captures most remaining variance, etc.

#### Variance Explained
The fraction of total variance explained by component $i$:
$$\text{Explained Variance}_i = \frac{\lambda_i}{\sum_{j=1}^d \lambda_j}$$

### Connection to Deep Learning

#### Linear Transformations
- PCA learns a linear transformation that creates a new basis
- Similar to how linear layers in neural networks learn transformations
- Both find useful representations of data

#### Feature Learning
- PCA: Unsupervised feature extraction based on variance
- Neural Networks: Supervised feature learning based on task objective
- Both compress information while preserving important patterns

#### Dimensionality Reduction
- Preprocessing step before feeding data to neural networks
- Reduces computational complexity
- Can help prevent overfitting by removing noise

### Practical Considerations

#### When to Use PCA
- High-dimensional data with correlated features
- Need to visualize high-dimensional data (reduce to 2D/3D)
- Computational efficiency requirements
- Remove noise and redundant information

#### Limitations
- Linear transformation only (can't capture nonlinear relationships)
- Components may not be interpretable
- Assumes variance equals importance
- Sensitive to feature scaling

### Implementation Steps
1. **Standardize data** (if features have different scales)
2. **Center the data** (subtract mean)
3. **Compute covariance matrix**
4. **Find eigenvalues and eigenvectors**
5. **Sort by eigenvalue magnitude**
6. **Select top k components**
7. **Project data onto selected components**
8. **Analyze variance explained**