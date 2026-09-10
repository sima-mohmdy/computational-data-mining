# Computational Data Mining — Exercise 10

## Multidimensional Scaling (MDS) and Isomap

### Objective

The goal of this exercise is to study and implement two dimensionality reduction techniques:

* Multidimensional Scaling (MDS)
* Isomap

The main purpose is to reduce high-dimensional data to a 2D space while preserving the important structure and relationships between data points.

---

## 1. Multidimensional Scaling (MDS)

MDS is a dimensionality reduction technique that attempts to preserve the pairwise distances between data points after mapping them to a lower-dimensional space.

In this exercise, a distance matrix between cities was used as the input. MDS was applied to obtain 2D coordinates for the cities and visualize their relative positions.

### Classical MDS

Classical MDS was also implemented from scratch using the mathematical formulation of the algorithm.

The main steps were:

1. Check that the distance matrix is symmetric.
2. Construct the centering matrix.
3. Compute the matrix \(B\).
4. Perform eigenvalue decomposition.
5. Sort the eigenvalues and eigenvectors.
6. Select the largest eigenvalues.
7. Construct the final low-dimensional coordinates.

### Important Observation

The orientation of an MDS solution is not unique. The resulting configuration can be translated, rotated, or reflected without changing the pairwise distances.

Therefore, the resulting 2D map may not have exactly the same orientation as the real geographical map.

---

## 2. Isomap

Isomap is a nonlinear dimensionality reduction technique that attempts to preserve the geodesic distances between data points.

Unlike MDS, which directly works with pairwise distances, Isomap first constructs a neighborhood graph and then estimates distances along this graph.

In this exercise, Isomap was applied to a face image dataset.

### Dataset

The dataset was provided as a `.mat` file and contained 698 face images.

Each image has a size of:

```text
64 × 64 = 4096 pixels
```

The original image matrix had the shape:

```text
(4096, 698)
```

After transposing, the data was represented as:

```text
(698, 4096)
```

where:

* Each row represents one image.
* Each column represents one pixel feature.

Isomap was then used to reduce the 4096-dimensional image data to two dimensions.

The resulting 2D representation was visualized together with randomly selected face images.

---

## Comparison

| Method        | Main Idea                                                      | Dataset              |
| ------------- | -------------------------------------------------------------- | -------------------- |
| MDS           | Preserve pairwise distances                                    | City distance matrix |
| Classical MDS | Mathematical formulation of MDS using eigenvalue decomposition | City distance matrix |
| Isomap        | Preserve geodesic distances through a neighborhood graph       | Face images          |

---

## Key Concepts

* Dimensionality Reduction
* Pairwise Distance
* Geodesic Distance
* Neighborhood Graph
* Eigenvalue Decomposition
* Classical MDS
* Nonlinear Dimensionality Reduction
* Manifold Learning
* 2D Data Visualization

---

## Libraries

* NumPy
* Pandas
* SciPy
* Matplotlib
* Scikit-learn

---

## Conclusion

In this exercise, MDS and Isomap were used to obtain 2D representations of different types of data.

MDS was used to visualize cities based on their pairwise distances, while Isomap was applied to high-dimensional face images to explore their underlying structure in a two-dimensional space.

Classical MDS was also implemented from scratch to understand the mathematical steps behind the method.
