
# Exercise 08 — Face Recognition Using HOSVD

##  Overview

In this exercise, face recognition is performed using **Higher-Order Singular Value Decomposition (HOSVD)** on the **Yale Faces** dataset.

The main goal is to represent the training face images as a tensor, apply HOSVD to extract a lower-dimensional representation, and then classify unseen test images by comparing their representations with the training subjects.

The overall pipeline is:

```text
Yale Faces Dataset
        ↓
Image Vectorization
        ↓
Tensor A
        ↓
HOSVD
        ↓
Core Tensor S + Factor Matrices
        ↓
Tensor B
        ↓
QR Decomposition
        ↓
Test Image Projection
        ↓
Alpha Coefficients
        ↓
Distance-based Classification
        ↓
Prediction
        ↓
Evaluation
```

---

##  Dataset

The **Yale Faces** dataset contains grayscale facial images of **15 subjects**, with **9 different facial expressions/conditions** for each subject.

### Training data

* Subjects: `15`
* Images per subject: `9`
* Total training images: `135`
* Image size: `243 × 320`
* Flattened image size:

```text
243 × 320 = 77760
```

Therefore, each image is represented as a vector of length `77760`.

### Test data

* Total test images: `30`
* Each subject has `2` test images.

---

## 1. Preparing the Training Data

Each grayscale image is flattened into a one-dimensional vector.

Therefore:

```text
One image → (77760,)
```

After stacking all training images:

```text
train_images_matrix.shape = (135, 77760)
```

where:

* `135` → number of training images
* `77760` → number of pixels/features per image

### Important: Ordering the Training Data

The files returned by `os.listdir()` are not necessarily ordered by subject.

Therefore, before constructing the tensor, the training images are grouped according to their subject labels:

```text
Subject 1  → 9 images
Subject 2  → 9 images
...
Subject 15 → 9 images
```

After grouping:

```text
(15, 9, 77760)
```

The axes represent:

```text
Subject × Expression × Pixels
```

The axes are then transposed to construct the final tensor:

```text
A.shape = (77760, 9, 15)
```

Thus:

```text
A
│
├── Mode 1 → Pixels (77760)
├── Mode 2 → Expressions (9)
└── Mode 3 → Subjects (15)
```

---

# 2. HOSVD

The training tensor is decomposed using **Higher-Order Singular Value Decomposition (HOSVD)**.

The HOSVD of tensor `A` can be written as:

$$
A = S \times_1 U_1 \times_2 U_2 \times_3 U_3
$$

where:

* `A` → original tensor
* `S` → core tensor
* `U_1, U_2, U_3` → orthogonal factor matrices
* `×_n` → mode-n tensor-matrix multiplication

The dimensions obtained in this exercise are:

```text
A  = (77760, 9, 15)

S  = (135, 9, 15)

U1 = (77760, 135)
U2 = (9, 9)
U3 = (15, 15)
```

The first mode is reduced from `77760` to `135`.

---

# 3. Constructing Tensor B

For the classification step, the core tensor `S` is transformed using the first factor matrix.

The resulting tensor is:

```text
B.shape = (135, 9, 15)
```

The second dimension represents the `9` expressions, while the third dimension represents the `15` subjects.

For each expression `e`, we extract:

```text
B[:, e, :]
```

which has dimensions:

```text
(135, 15)
```

This matrix contains the representation of the 15 training subjects for a particular expression.

---

# 4. QR Decomposition

For each of the 9 expressions, QR decomposition is applied to the corresponding matrix:

$$
B_e = Q_e R_e
$$

where:

* `B_e` → matrix corresponding to expression `e`
* `Q_e` → orthogonal matrix
* `R_e` → upper triangular matrix

The dimensions are:

```text
Q_e = (135, 15)
R_e = (15, 15)
```

The matrices `Q_e` and `R_e` are stored for later classification.

---

# 5. Test Image Projection

Each test image is flattened into a vector:

```text
z.shape = (77760,)
```

The test image is projected into the reduced HOSVD space.

If `F` represents the transformation obtained from the HOSVD factor matrix, the projected test image is:

$$
\hat{z} = F^T z
$$

Therefore:

```text
z_hat.shape = (135,)
```

The projection is performed for all 30 test images.

---

# 6. Computing the Coefficients

For each test image and each of the 9 expressions, the coefficient vector `α_e` is obtained using:

$$
\alpha_e = R_e^{-1} Q_e^T \hat{z}
$$

In the implementation, the linear system is solved directly instead of explicitly computing the inverse:

```text
R_e α_e = Q_e^T z_hat
```

The resulting coefficient vector has dimension:

```text
alpha_e.shape = (15,)
```

---

# 7. Distance-Based Classification

For each expression, the obtained coefficient vector is compared with the coefficient representation of each of the 15 subjects.

The Euclidean distance is used:

$$
d_j = \|\alpha_e - H_j\|_2
$$

where:

* `α_e` → coefficient vector of the test image for expression `e`
* `H_j` → coefficient representation of subject `j`
* `d_j` → Euclidean distance

For each expression, the subject with the smallest distance is selected:

$$
j^* = \arg\min_j d_j
$$

---

# 8. Tolerance

A tolerance value is used to determine whether the minimum distance is sufficiently small:

```text
tol = 0.7
```

If:

$$
d_{j^*} < 0.7
$$

the predicted subject for that expression is stored.

If no expression satisfies the tolerance condition, the prediction is set to:

```text
-1
```

which means that no sufficiently close subject was found.

---

# 9. Final Prediction

Each test image is evaluated using all 9 expressions.

Therefore, one test image may produce several candidate subject predictions.

The final subject is selected using the **most frequent predicted subject** among the valid expression predictions.

If no valid prediction exists:

```text
final prediction = -1
```

Because the subjects are internally represented using zero-based indices:

```text
0 → Subject 1
1 → Subject 2
...
14 → Subject 15
```

the final predictions are shifted by `+1` before evaluation.

---

# 10. Evaluation

The predictions are evaluated using:

* Accuracy
* Classification Report
* Confusion Matrix

## Accuracy

The accuracy is calculated as:

$$
Accuracy =
\frac{\text{Number of Correct Predictions}}
{\text{Total Number of Predictions}}
$$

The obtained accuracy is:

```text
Accuracy = 0.7333
```

or approximately:

```text
73.33%
```

With 30 test images:

```text
22 correct predictions
8 incorrect predictions
```

---

# 11. Classification Report

The classification report provides:

* Precision
* Recall
* F1-score
* Support

The final accuracy is approximately:

```text
73.33%
```

The warning related to class `0` occurs because the actual dataset labels correspond to subjects `1–15`, while `0` can appear when the classifier returns `-1` and the prediction is shifted by `+1`.

For the final report, only the actual classes `1–15` are considered.

---

# 12. Confusion Matrix

The confusion matrix is used to visualize the classification results.

Rows represent:

```text
True Labels
```

Columns represent:

```text
Predicted Labels
```

Therefore:

* Values on the main diagonal → correct predictions
* Values outside the diagonal → misclassifications

Since the test set contains only 30 images, most cells of the `15 × 15` confusion matrix are expected to be zero.

This is normal because each subject has only two test images.

---

#  Final Result

```text
Number of subjects       : 15
Training images          : 135
Test images              : 30
Expressions per subject : 9
Image size               : 243 × 320
Flattened image size     : 77760
Tolerance                : 0.7

Accuracy                 : 73.33%
Correct predictions      : 22 / 30
Incorrect predictions    : 8 / 30
```

---

#  Key Concepts

This exercise combines several important concepts:

### Tensor Representation

Instead of representing the training dataset only as a 2D matrix, the images are organized as a third-order tensor:

```text
Pixels × Expressions × Subjects
```

### HOSVD

HOSVD decomposes the tensor into:

```text
Core Tensor + Orthogonal Factor Matrices
```

and provides a lower-dimensional representation of the image data.

### QR Decomposition

QR decomposition is used to obtain an orthogonal basis `Q` and an upper triangular matrix `R` for each expression.

### Projection

Test images are projected into the reduced HOSVD space before classification.

### Distance-Based Classification

The projected representation of a test image is compared with the training subjects using Euclidean distance.

### Majority Voting

The predictions obtained from the different expressions are combined, and the most frequent valid subject is selected as the final prediction.

---

#  Conclusion

In this exercise, the Yale Faces dataset was represented as a third-order tensor and processed using HOSVD.

The most important preprocessing step was organizing the training images by subject before constructing the tensor. This ensures that the tensor dimensions correctly represent:

```text
Pixels × Expressions × Subjects
```

After HOSVD, QR decomposition, projection, and distance-based classification, the method achieved an accuracy of approximately:

```text
73.33%
```

on the 30 test images.
