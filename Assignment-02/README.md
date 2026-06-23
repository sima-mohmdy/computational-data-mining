🟢 Assignment 02 - TinyMNIST Classification (Mean Image + Euclidean Distance)
📌 Problem Description

In this assignment, we work with the TinyMNIST dataset which contains images of handwritten digits (0–9).
Each image is classified based on a simple nearest-mean approach.

⚙️ Method
1. Data Preparation
Images are loaded from folders (train/test)
Each image is converted to a NumPy array
Each image is flattened from 28×28 to a 784-dimensional vector
2. Class Mean Computation

For each digit class (0 to 9):

Mean image is computed using training samples
These mean images represent each class prototype
3. Classification

For each test image:

Compute Euclidean distance to all class mean vectors
Assign the label of the nearest mean (minimum distance)
📊 Evaluation

Accuracy is computed using:

True labels from test labels.csv
Predicted labels from the model
Final Accuracy:

79.5%

📁 Dataset Structure
TinyMNIST/
├── train/
│   ├── 0 ... 9 (class folders)
├── test/
├── train labels.csv
└── test labels.csv
🧠 Key Concepts Learned
Image preprocessing
NumPy array manipulation
Flattening images
Mean image computation
Euclidean distance
Basic classification without ML libraries
🚀 Author

Student Project - Computational Data Mining Course
