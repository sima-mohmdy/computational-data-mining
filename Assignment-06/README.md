
# Assignment 06 — Document Clustering using NMF and K-Means

## Overview

In this assignment, document clustering is performed using two different clustering algorithms:

- Non-negative Matrix Factorization (NMF)
- K-Means

The performance of both algorithms is evaluated using:

- Purity
- Entropy

The experiments are performed on four datasets derived from **TDT2** and **Reuters21578**.

---

## Datasets

Four datasets were constructed from the original datasets:

1. **TDT2 Top 10** — the 10 categories with the highest number of documents
2. **TDT2 Last 10** — the 10 categories with the lowest number of documents
3. **Reuters21578 Top 10** — the 10 categories with the highest number of documents
4. **Reuters21578 Top 20** — the 20 categories with the highest number of documents

The resulting feature matrix shapes were:

| Dataset | Samples | Features |
|---|---:|---:|
| TDT2 Top 10 | 7456 | 36771 |
| TDT2 Last 10 | 653 | 36771 |
| Reuters21578 Top 10 | 7285 | 18933 |
| Reuters21578 Top 20 | 7800 | 18933 |

---

## Evaluation Metrics

### Purity

Purity measures how well each cluster corresponds to a single ground-truth class.

Higher Purity indicates better clustering performance.

The Purity score was implemented using the contingency matrix.

### Entropy

Entropy measures the degree of class mixing within the clusters.

Lower Entropy indicates better clustering performance.

The Entropy implementation follows the formula specified in the assignment.

Zero elements of the contingency matrix are ignored to avoid computing `log(0)`.

---

## Non-negative Matrix Factorization (NMF)

NMF factorizes the non-negative document-term matrix as:

$$
X \approx WH
$$

where:

- `X` is the original document-term matrix
- `W` represents the relationship between documents and clusters
- `H` represents the relationship between clusters and features

The number of components was set to 10 for the experiments.

After obtaining `W`, each document was assigned to the cluster corresponding to the maximum value in its row:

```python
y_pred = np.argmax(W, axis=1)
```

---

## K-Means

K-Means was also applied to the same four datasets.

The number of clusters was set to 10 to make the comparison with NMF consistent.

```python
KMeans(
    n_clusters=10,
    random_state=0,
    n_init="auto"
)
```

---

## Results

### NMF

| Dataset | Purity | Entropy |
|---|---:|---:|
| TDT2 Top 10 | ≈ 0.80 | ≈ 0.26 |
| TDT2 Last 10 | ≈ 0.75 | ≈ 0.27 |
| Reuters21578 Top 10 | ≈ 0.75 | ≈ 0.30 |
| Reuters21578 Top 20 | ≈ 0.69 | ≈ 0.32 |

### K-Means

| Dataset | Purity | Entropy |
|---|---:|---:|
| TDT2 Top 10 | ≈ 0.44 | ≈ 0.64 |
| TDT2 Last 10 | ≈ 0.44 | ≈ 0.54 |
| Reuters21578 Top 10 | ≈ 0.72 | ≈ 0.40 |
| Reuters21578 Top 20 | ≈ 0.56 | ≈ 0.45 |

---

## Comparison

The results show that **NMF achieved better clustering performance than K-Means on all four datasets**.

In particular, the difference between the two methods is much more noticeable on the TDT2 datasets.

For example, on TDT2 Top 10:

- NMF Purity ≈ 0.80
- K-Means Purity ≈ 0.44

NMF also obtained lower Entropy values across all datasets, indicating less class mixing within the resulting clusters.

---

## Conclusion

In this experiment, NMF generally outperformed K-Means for document clustering on the TDT2 and Reuters21578 datasets.

The results suggest that the non-negative factorization approach was better able to capture meaningful latent structures in these sparse document-feature matrices.

---

## Libraries

- Python
- NumPy
- Scikit-learn
- SciPy
- Pandas


  ## Dataset Source

The TDT2 and Reuters21578 datasets used in this assignment were obtained from the Text Data collection provided by Deng Cai:

[Text Data — Deng Cai](http://www.cad.zju.edu.cn/home/dengcai/Data/TextData.html)
