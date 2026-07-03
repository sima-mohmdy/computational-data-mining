
# Computational Data Mining

Welcome to my **Computational Data Mining** learning repository.

This repository is more than a collection of assignment solutions. It is a record of my learning journey throughout the Computational Data Mining course.

The purpose of this repository is to document:

* The concepts I learned.
* The mathematical ideas behind each algorithm.
* The implementation process.
* The challenges I encountered.
* The lessons I learned while solving each assignment.

My goal is not only to complete the assignments, but to truly understand the algorithms and be able to implement them from scratch.

---

# Learning Progress

* ✅ Assignment 01
* ✅ Assignment 02
* ✅ Assignment 03
* ⏳ Assignment 04
* ⏳ Assignment 05
* ⏳ Assignment 06
* ⏳ Assignment 07
* ⏳ Assignment 08
* ⏳ Assignment 09
* ⏳ Assignment 10

---

# Assignment 01

## Goal

Become familiar with the computational data mining environment and prepare the foundation for future assignments.

## What I Learned

* How course assignments are organized.
* How to work with notebooks and computational experiments.
* The importance of documenting every step of an implementation.
* Building a workflow that can be extended throughout the course.

## Challenges

* Understanding how to organize the project before starting future implementations.
* Building a clean workflow that can be reused in later assignments.

## Reflection

Although this assignment was relatively simple, it established the workflow that will be used throughout the rest of the course.

---

# Assignment 02

## Goal

Learn how image data can be represented numerically and prepared for machine learning algorithms.

## What I Learned

* Images are matrices of pixel values.
* Before applying many algorithms, images are converted into vectors.
* A 28×28 image becomes a 784-dimensional vector.
* Working with NumPy arrays and matrix representations.
* Building reusable functions instead of repeating code.
* Understanding the importance of matrix dimensions in numerical computing.

## Challenges

* Understanding the difference between Python lists and NumPy arrays.
* Correctly managing matrix dimensions.
* Writing reusable functions while keeping the implementation understandable.

## Reflection

This assignment helped me understand that many machine learning algorithms operate on vectors and matrices rather than raw images.

---

# Assignment 03

## Goal

Implement an image classifier using QR Decomposition and Least Squares.

## Mathematical Concepts

During this assignment I learned several important linear algebra concepts.

### Building the Data Matrix

Each training image is first converted into a vector.

For each digit (0–9), all training vectors are placed as columns of a matrix A.

Each matrix therefore represents the subspace of one digit class.

---

### QR Decomposition

Each matrix A is decomposed as

A = QR

where:

* Q contains orthonormal basis vectors.
* R is an upper triangular matrix.

I learned that although the decomposition produces both matrices, the classifier mainly uses **Q**, because Q represents the subspace spanned by the training images.

---

### Projection

One of the most important concepts I learned was **projection**.

Instead of directly comparing a test image with every training image, the test image is projected onto the subspace of each digit.

The projected image represents the closest reconstruction of the test image inside that class.

---

### Reconstruction Error

After projection, I compute the reconstruction error

‖x − x̂‖

where

* x is the original test image.
* x̂ is its reconstructed (projected) version.

The smaller this error is, the better that digit class represents the test image.

Finally, the predicted digit is the class with the minimum reconstruction error.

---

## Implementation Steps

1. Load the image dataset.
2. Convert every image into a vector.
3. Build one matrix A for each digit.
4. Perform QR decomposition.
5. Project every test image onto every class subspace.
6. Compute reconstruction errors.
7. Choose the class with minimum error.
8. Compute the final classification accuracy.

---

## Challenges

This assignment was much more conceptual than previous ones.

Some of the difficulties I encountered were:

* Understanding why QR decomposition is useful.
* Understanding the role of Q and R.
* Understanding why only Q is required during classification.
* Understanding what projection actually means geometrically.
* Distinguishing between the original image and its reconstructed image.
* Understanding why reconstruction error determines the predicted class.
* Translating mathematical equations into Python code.
* Correctly handling matrix dimensions during implementation.

---

## Reflection

This assignment changed the way I think about linear algebra.

Instead of seeing QR decomposition as only a mathematical technique, I learned how it can be used to build a practical image classifier.

I also realized that understanding the mathematical intuition behind an algorithm makes implementing it much easier than simply translating formulas into code.

---

# Personal Learning Strategy

Throughout this course, I intentionally prioritize understanding over optimization.

My approach is:

1. Understand the mathematical idea.
2. Implement it using my own coding style.
3. Verify that the implementation works correctly.
4. After completing all assignments, revisit every project.
5. Improve the code quality by learning more Pythonic programming techniques while preserving the original understanding.

I believe that writing my own implementations first helps me develop stronger problem-solving skills before focusing on code optimization.
