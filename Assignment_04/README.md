
# Assignment 04 - Singular Value Decomposition (SVD) for Image Compression

## Goal
The goal of this assignment is to explore **Singular Value Decomposition (SVD)** as a method for image compression and to understand how low-rank approximation can reduce storage while preserving important visual information.

This assignment demonstrates how images can be compressed by keeping only the most important singular values.

---

## What I Learned

- Images can be represented as matrices (grayscale) or multiple matrices (RGB channels).
- SVD decomposes a matrix into three components:
  - U: left singular vectors (row features)
  - Σ (Sigma): singular values (importance of components)
  - Vᵀ: right singular vectors (column features)
- Singular values are ordered from most important to least important.
- Keeping only the top `k` singular values results in a **low-rank approximation** of the image.
- This approximation reduces storage while preserving the main structure of the image.

---

## Methodology

### 1. Image Representation
- A grayscale image is represented as a 2D matrix.
- A color image is split into 3 matrices:
  - Red channel (R)
  - Green channel (G)
  - Blue channel (B)

---

### 2. SVD Decomposition
For each channel:

\[
A = U \Sigma V^T
\]

Where:
- U contains left singular vectors
- Σ contains singular values
- Vᵀ contains right singular vectors

---

### 3. Low-Rank Approximation

To compress the image, only the first `k` singular values are kept:

\[
A_k = U_k \Sigma_k V_k^T
\]

Different values of `k` were tested to observe the trade-off between compression and quality.

---

### 4. RGB Reconstruction
Each channel is reconstructed separately and then combined:

- R_k
- G_k
- B_k

Final image:

\[
Image_k = stack(R_k, G_k, B_k)
\]

---

## Compression Ratio

The compression size is calculated as:

\[
3 \times k \times (1 + m + n)
\]

Where:
- `m × n` is image size
- `k` is number of singular values used
- Factor 3 is for RGB channels

---

## Observations

- Small `k` → high compression but low quality
- Large `k` → better quality but less compression
- Singular values contain most of the important image information
- Most image information is concentrated in a few singular values

---

## Challenges

- Understanding how SVD relates to image structure
- Choosing the appropriate value of `k`
- Handling RGB images correctly
- Debugging dimension mismatches during matrix multiplication
- Understanding reconstruction and compression trade-off

---

## Reflection

This assignment helped me understand that images are not just visual objects but mathematical structures.

SVD showed that most of the important information in an image can be captured using a small number of components, which is the core idea behind many compression and machine learning techniques like PCA.

---

## Files
- `svd.ipynb` → Implementation of SVD image compression
- `README.md` → Explanation of the assignment
