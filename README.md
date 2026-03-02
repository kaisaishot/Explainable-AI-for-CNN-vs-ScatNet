# Explainable AI Analysis of CNN vs ScatNet for Image Classification

This project investigates the interpretability and feature learning behavior of Convolutional Neural Networks (CNN) and Scattering Networks (ScatNet) using multiple Explainable AI (XAI) methods. The goal is to understand how learned vs fixed feature extractors influence classification performance and model attribution.

## Overview

Two models were implemented and compared:

- **CNN** – Trainable convolutional neural network implemented in PyTorch
- **ScatNet** – Fixed wavelet-based feature extractor implemented using Kymatio

Both models share a common classifier architecture and were evaluated on a binary subset of the Intel Image Classification dataset.

Six XAI methods were applied to analyze and interpret model decisions.

---

## Objectives

- Compare learned feature extraction (CNN) vs fixed feature extraction (ScatNet)
- Apply and evaluate multiple Explainable AI methods
- Analyze attribution maps to understand model decision behavior
- Compare gradient-based vs perturbation-based interpretability methods
- Visualize and interpret learned filters and attribution patterns

---

## Models

### CNN
- 3 convolutional layers
- Global Average Pooling
- Dropout regularization
- Fully connected classifier
- Trainable feature extractor

### ScatNet
- Wavelet-based scattering transform (Kymatio)
- Fixed filters across multiple orientations and scales
- Batch normalization and Global Average Pooling
- Fully connected classifier
- Non-trainable feature extractor

---

## Dataset

**Intel Image Classification Dataset**

- Classes used: `Street` and `Building`
- Binary classification task
- Dataset split into:
  - Training set
  - Validation set
  - Test set

Data augmentation and preprocessing were applied to improve robustness.

---

## Explainable AI Methods

The following attribution methods were implemented using Captum and custom code:

| Method | Type | Description |
|------|------|-------------|
| Saliency | Gradient-based | Highlights pixels with strongest gradient influence |
| Input × Gradient | Gradient-based | Enhances saliency by scaling gradients with input |
| Integrated Gradients | Gradient-based | Reduces noise using baseline integration |
| SmoothGrad | Gradient-based | Improves stability by averaging noisy gradients |
| GradientSHAP | Gradient-based | Approximates SHAP values efficiently |
| Occlusion | Perturbation-based | Identifies important image regions by masking patches |

Saliency was implemented from scratch to demonstrate low-level gradient attribution.

---

## Training Details

- Framework: PyTorch
- Optimizer: Adam
- Loss function: Cross-Entropy Loss
- Cross-validation: 5-fold cross-validation
- Regularization:
  - Dropout
  - Data augmentation
  - Early stopping

---

## Results

| Model | Test Accuracy | Test F1 Score |
|------|---------------|---------------|
| CNN | 86.3% | 0.8619 |
| ScatNet | 76.3% | 0.7581 |

### Key Findings

- CNN significantly outperformed ScatNet due to learnable filters
- ScatNet showed stable but less accurate performance
- CNN learned task-specific features while ScatNet used fixed filters

---

## Interpretability Analysis

### CNN

- Learned meaningful spatial features
- Focused on relevant structures such as edges and object boundaries
- Ignored irrelevant regions effectively
- Produced cleaner attribution maps

### ScatNet

- Attribution maps were noisier and less localized
- Fixed filters extracted general features without task adaptation
- Less precise attribution patterns

---

## Comparison of XAI Methods

### Gradient-based methods

- Integrated Gradients produced stable and meaningful attribution maps
- SmoothGrad reduced gradient noise
- Input × Gradient improved attribution clarity

### Perturbation-based methods

- Occlusion provided the clearest interpretation
- Successfully identified image regions driving predictions
- Most robust method overall

---

## Filter Analysis

CNN filters:
- Learned edge detectors and spatial feature extractors
- Adapted specifically to the dataset

ScatNet filters:
- Fixed wavelet filters
- Extract frequency and orientation features
- Not adapted to specific task

---

## Technologies Used

- Python
- PyTorch
- Captum
- Kymatio
- NumPy
- Matplotlib

---

## Key Takeaways

- Learnable CNN filters outperform fixed ScatNet filters for classification tasks
- Explainable AI methods provide valuable insight into model behavior
- Integrated Gradients and Occlusion are highly effective attribution methods
- CNNs learn task-specific features that improve both accuracy and interpretability

---

