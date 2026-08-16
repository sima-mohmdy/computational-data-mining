# Image Denoising using SVD

## Introduction

In this project, image denoising is performed using **Singular Value Decomposition (SVD)**.

The main idea is to add Gaussian noise to an image and then use SVD with different values of k to reconstruct the image.

Since the largest singular values usually contain the main structure and important information of the image, keeping only the first k singular values can remove a significant amount of noise while preserving the important features of the image.

---

## Steps

### 1. Loading the Image

A color RGB image is selected as the input image.

The image has three color channels:

- Red
- Green
- Blue


Each channel is represented as a 2D matrix.


---

## 2. Adding Gaussian Noise

Gaussian noise is added to the original image using a normal distribution.

The noise is generated using:

mu = 0

sigma = 100


The noisy image is then used as the input for the SVD decomposition.


---

## 3. Applying SVD

Since the image is RGB, SVD is applied separately to each color channel.

For each channel:

A = UΣVᵀ


The singular values represent the importance of different components of the image.


---

## 4. Low Rank Approximation

The noisy image is reconstructed using different values of k.

The approximation is calculated as:

Aₖ = UₖΣₖVₖᵀ


The following values of k are tested:

- k = 50
- k = 100
- k = 150
- ...
- k = 500


A smaller k keeps fewer components and therefore removes more information, including noise.

A larger k preserves more details but can also preserve more noise.


---

## 5. Singular Values Analysis

The singular values of the noisy image are plotted separately for the Red, Green and Blue channels.

The plots are used to analyze how the singular values decrease as the number of components increases.


A significant drop in the singular values can be observed around k ≈ 10.

After this point, the singular values become much smaller and their changes become less significant.


---

## 6. Selecting an Appropriate k

Based on the Singular Values plots, k ≈ 10 can be considered a suitable value for the low-rank approximation.

The reason is that the first few singular values contain most of the important information of the image, while the much smaller singular values after this point contribute less to the main structure and may contain fine details and noise.


Therefore, choosing a relatively small k can provide a balance between:

- Removing noise
- Preserving important image structures
- Maintaining acceptable image quality


---

## Results

The reconstructed images for different values of k demonstrate the effect of the rank of the approximation on image quality and noise reduction.

The results show that SVD can be used to reduce noise by keeping only the most significant singular components.


---

## Concepts Covered

- Singular Value Decomposition (SVD)
- Gaussian Noise
- Image Denoising
- Low-Rank Approximation
- Singular Values
- Rank-k Approximation
- RGB Image Processing
- Noise Reduction


---

## Libraries

- NumPy
- Matplotlib
- ImageIO


---

## Conclusion

This project demonstrates how Singular Value Decomposition can be used for image denoising.

By keeping only the most significant singular values, the noisy image can be approximated using a lower-rank representation. This can reduce noise while preserving the main structure of the image.

The experiment also shows how Singular Values can be analyzed to select an appropriate value of k for the reconstruction.
