# Image Compression using SVD

## Introduction

In this project, image compression is performed using **Singular Value Decomposition (SVD)**.

SVD is a matrix decomposition method that factorizes a matrix into three matrices:

A = UΣVᵀ

where:

- U contains the left singular vectors
- Σ contains the singular values
- Vᵀ contains the right singular vectors

The main idea of compression is to keep only the largest singular values because they contain the most important information of the image. By removing smaller singular values, the storage size is reduced while the main structure of the image is preserved.

---

## Steps

### 1. Loading Images

Two types of images are considered:

- A grayscale image
- A color RGB image


A grayscale image is represented as a 2D matrix:

(height × width)

A color image is represented as three separate 2D matrices:

- Red channel
- Green channel
- Blue channel


---

## 2. Applying SVD

For a grayscale image, SVD decomposition is applied:

A = UΣVᵀ


For a color image, SVD is applied separately to each RGB channel:

R = UᵣΣᵣVᵣᵀ

G = U₍g₎Σ₍g₎V₍g₎ᵀ

B = UᵦΣᵦVᵦᵀ


---

## 3. Low Rank Approximation

Instead of using all singular values, only the first k singular values are kept.

The compressed image is reconstructed as:

Aₖ = UₖΣₖVₖᵀ


Different values of k are tested:

- k = 2
- k = 5
- k = 10
- k = 25
- k = 50


A smaller k results in:

- More compression
- Less storage
- Lower image quality


A larger k results in:

- Better reconstruction quality
- More storage usage


---

## 4. Memory Reduction

The original image requires storing:

m × n values


After compression, instead of storing the whole matrix, only these matrices are stored:

- Uₖ : (m × k)
- Σₖ : (k × k)
- Vₖᵀ : (k × n)


Therefore, the required storage is reduced.

The memory saving is calculated by comparing the original image size with the compressed representation.


---

## 5. Singular Values Analysis

The singular values represent the importance of different components of the image.

The first singular values usually contain the main structure and important information, while smaller singular values represent less important details and possible noise.


A logarithmic plot of singular values is used to analyze their contribution.


---

## 6. Explained Variance

The contribution of each singular value is calculated using:

σᵢ² / Σσ²


The relationship between singular values and eigenvalues is:

λᵢ = σᵢ²


Therefore, this concept is related to explained variance in PCA.

The cumulative explained variance shows how much information is preserved when keeping the first k singular values.


---

## Results

The results show that:

- A small number of singular values can preserve most important image information.
- SVD can significantly reduce storage requirements.
- Low-rank approximation can reconstruct images with acceptable quality.


---

## Libraries

- NumPy
- SciPy
- Matplotlib
- Image Processing tools


---

## Conclusion

This project demonstrates the application of Singular Value Decomposition for image compression.

SVD provides a connection between linear algebra concepts and practical applications such as:

- Image compression
- Dimensionality reduction
- Data representation
