
# Computational Data Mining - Assignment 5  
## Image Denoising using SVD (Singular Value Decomposition)

---

## 📌 Overview

In this assignment, we explore the application of **Singular Value Decomposition (SVD)** for **image denoising**.

Unlike the previous assignment (where SVD was used for image compression), here we intentionally add noise to an image and then use SVD to reduce it and reconstruct a cleaner version.

---

## 🎯 Objective

The main goals of this assignment are:

- Add artificial noise (Gaussian noise) to an image
- Apply SVD on the noisy image
- Reconstruct the image using different values of rank \(k\)
- Analyze the effect of \(k\) on image quality
- Determine an optimal value of \(k\) for denoising
- Visualize singular values to understand data structure

---

## 🧪 Methodology

### 1. Image Preparation
- Load an RGB image
- Convert it to grayscale for analysis (mean over channels)
- Keep RGB version for color reconstruction

### 2. Noise Addition
- Gaussian noise is added to the image
- Image is converted to `float32` to avoid overflow issues
- Values are clipped to the range [0, 255]

---

### 3. SVD Decomposition
For both grayscale and each RGB channel:

\[
A = U \Sigma V^T
\]

---

### 4. Image Reconstruction

The image is reconstructed using different ranks \(k\):

\[
A_k = U_k \Sigma_k V_k^T
\]

Different values of \(k\) are tested to observe quality changes.

---

### 5. Singular Value Analysis
- Singular values are plotted using a logarithmic scale
- This helps identify the "elbow point"
- The elbow point is used to estimate the optimal \(k\)

---

## 📊 Results

- Small \(k\): Over-smoothing, loss of details
- Large \(k\): More details but noise remains
- Optimal \(k\): Balanced trade-off between denoising and detail preservation

For this experiment, the best results were observed around:


k ≈ 50 (approximately, depending on the image)



---

## 🧠 Key Insight

SVD separates:
- **Large singular values → important image structure**
- **Small singular values → noise and fine details**

By removing small singular values, noise can be effectively reduced.

---

## 🖼️ Visualizations

- Original Image
- Noisy Image
- Reconstructed images for different values of \(k\)
- Singular value distribution plot

---

## 🛠️ Tools Used

- Python
- NumPy
- Matplotlib
- OpenCV (for noise generation and image processing)

---

## 📌 Conclusion

This assignment demonstrates that SVD is not only useful for compression but also for **image denoising**. By selecting an appropriate rank \(k\), we can effectively reduce noise while preserving important image structures.

---

## 👨‍💻 Author

Computational Data Mining Course – Assignment 5
