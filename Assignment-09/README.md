
# Assignment 9 — Automatic Keyword & Key Sentence Extraction

## Overview

In this assignment, the goal is to extract **keywords** and **key sentences** from a relatively long text using matrix-based methods.

The main steps are:

1. Text preprocessing
2. Constructing a Term-Sentence Matrix
3. Extracting keywords and key sentences using SVD
4. Extracting key sentences using NMF
5. Reducing redundancy between similar sentences using the Householder transformation
6. Analyzing the results

---

## Dataset

The **Disaster Tweets** dataset was used for this assignment.

The `text` column contains the sentences/tweets that were used for keyword and key sentence extraction.

After preprocessing and removing duplicate sentences, the dataset contained approximately **6,860 sentences** and **13,729 terms**.

---

## 1. Text Preprocessing

The following preprocessing steps were applied:

* Removing URLs
* Removing emojis and HTML elements
* Removing punctuation
* Converting text to lowercase
* Removing English stopwords and additional unwanted words
* Removing numeric characters
* Applying **Porter Stemming**
* Removing duplicate sentences

---

## 2. Term-Sentence Matrix

A **TF-IDF** representation was used to construct the Term-Sentence Matrix.

The resulting TF-IDF matrix initially had the shape:

```text
(6860, 13729)
```

Since the required matrix is in **Term × Sentence** form, the matrix was transposed:

```text
A = tfidf.transpose()
```

Therefore:

```text
A.shape = (13729, 6860)
```

where:

* Rows → terms
* Columns → sentences

---

## 3. Algorithm 1 — SVD

SVD was applied to the Term-Sentence Matrix to determine the importance of words and sentences.

The first singular vectors were used to calculate importance scores:

* Absolute values of the first left singular vector → **word importance**
* Absolute values of the first right singular vector → **sentence importance**

The words and sentences were then sorted according to their importance scores.

### Limitation

A problem with this approach is that **similar or redundant sentences can receive high scores simultaneously**.

---

## 4. Algorithm 2 — NMF

To address the redundancy problem, **Non-negative Matrix Factorization (NMF)** was used.

The matrix was factorized as:

```text
A ≈ C × D
```

where:

* `C` represents the basis matrix
* `D` contains the coefficients associated with the sentences

The importance of each sentence was determined using the **Euclidean norm of the corresponding column of `D`**.

---

## 5. Redundancy Reduction with Householder Transformation

Simply selecting sentences based on their column norms can still result in similar sentences being selected.

To reduce this redundancy, a **Householder transformation** was applied iteratively.

At each iteration:

1. The most important remaining sentence is selected.
2. Its column is moved to the current position.
3. A Householder vector is constructed.
4. A Householder matrix `Q` is created.
5. `C` and `D` are updated using the orthogonal transformation.
6. The process is repeated until the desired number of sentences is selected.

The transformation helps modify the remaining coefficients so that sentences similar to already selected sentences become less likely to dominate subsequent selections.

In this implementation, **15 key sentences** were extracted.

---

## Libraries Used

```python
numpy
pandas
scikit-learn
nltk
scipy
```

Main techniques:

* TF-IDF
* SVD
* NMF
* Householder Transformation

---

## Conclusion

This assignment demonstrates how **linear algebra and matrix factorization techniques** can be applied to text summarization.

SVD provides a simple way to identify important words and sentences, but it may select redundant sentences. NMF combined with an iterative Householder transformation provides a way to reduce this redundancy and obtain a more diverse set of key sentences.
