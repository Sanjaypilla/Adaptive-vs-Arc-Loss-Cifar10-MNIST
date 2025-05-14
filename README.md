# Adaptive Loss vs ArcFace Loss on MNIST and CIFAR-10

## Overview

This project presents an in-depth comparative analysis of two angular margin-based loss functions — **ArcFace Loss** and the proposed **Adaptive Loss (AdaLoss)** — applied to image classification tasks on the **MNIST** and **CIFAR-10** datasets.

AdaLoss improves upon ArcFace by introducing an **adaptive angular margin** that dynamically adjusts based on training feedback. This adaptation allows better generalization and faster convergence, especially on complex datasets like CIFAR-10.



## Table of Contents

- [Introduction](#introduction)
- [Loss Functions](#loss-functions)
  - [ArcFace Loss](#arcface-loss)
  - [Adaptive Loss (AdaLoss)](#adaptive-loss-adaloss)
- [Implementation Details](#implementation-details)
- [Results](#results)
- [Visual Analysis](#visual-analysis)
- [Conclusion](#conclusion)
- [Future Work](#future-work)



## Introduction

ArcFace Loss is a widely-used angular margin-based loss function that improves class separability in angular space, especially for face recognition. However, it uses a **fixed margin**, which can limit performance on datasets with **high intra-class variability**, such as CIFAR-10.

To overcome this, **AdaLoss** was introduced. It dynamically adjusts the margin during training, based on dataset complexity and model progress. This allows improved generalization and faster convergence.


## Loss Functions

### ArcFace Loss

- Adds a **fixed angular margin** to increase class separation.
- Uses **cosine similarity** between features and class weights.
- Applies a **scaling factor** to logits for sharper decision boundaries.

**Limitations:**

- Fixed margin may not suit all datasets.
- Sensitive to hyperparameters (margin, scale).
- Lacks flexibility for diverse tasks.

### Adaptive Loss (AdaLoss)

- Uses an **adaptive margin** that evolves during training.
- **Increases margin** when classes are hard to separate.
- **Reduces margin** when separation is easy.
- Allows better generalization and faster convergence.


## Implementation Details

### Dataset Preparation

- **MNIST**: Grayscale images of handwritten digits.
- **CIFAR-10**: RGB images from 10 object categories.
- Both datasets are loaded using PyTorch’s `DataLoader` and normalized.

### Model Architectures

- `ArcFaceCNN` (for MNIST)
- `ArcFaceCNN_CIFAR10` (for CIFAR-10)

Each model uses convolutional layers to extract features, followed by fully connected layers. These features are passed to either the ArcFace or AdaLoss function.

### ArcFace Loss Function

- Computes cosine similarity between features and class weights.
- Applies fixed angular margin.
- Scales logits before applying softmax.

### AdaLoss Function

- Same base computation as ArcFace.
- Dynamically adjusts margin during training.
- Margin increases when model struggles, decreases when classes are separable.

### Training and Evaluation

- Forward Pass → Loss Computation → Backward Pass → Parameter Update.
- Evaluation on test data after each epoch.


## Results

### MNIST Dataset

- **ArcFace Accuracy**: 97.86%
- **AdaLoss Accuracy**: 99.11%
- **Conclusion**: AdaLoss converges faster and generalizes better.

### CIFAR-10 Dataset

- **ArcFace Accuracy**: 62.35%
- **AdaLoss Accuracy**: 68.13%
- **Conclusion**: AdaLoss handles complex intra-class variation better.


## Visual Analysis

![AdaLoss CIFAR](https://github.com/user-attachments/assets/120fedc4-458e-488f-bd48-dbc5a8973fd7)
![AdaLoss MNIST](https://github.com/user-attachments/assets/7da03127-714f-4040-be23-0fbd5d1c4b30)
![ArcLoss CIFAR](https://github.com/user-attachments/assets/a0d1caf7-a90c-43fe-81b7-1986126a0906)
![ArcLoss MNIST](https://github.com/user-attachments/assets/e3f998b1-e867-4786-82ed-e6c28000e389)
![Comaprison AdaLoss vs ArcLoss](https://github.com/user-attachments/assets/332712c5-43a4-4578-81e8-8d4c533a4dcd)


## Conclusion

- **AdaLoss** significantly improves upon **ArcFace** by dynamically adjusting the margin based on training performance.
- Demonstrates **faster convergence** and **higher accuracy**, especially on challenging datasets like **CIFAR-10**.
- Shows potential for **robust generalization** across diverse classification tasks.


## Future Work

- Optimize the margin adjustment algorithm further.
- Extend experiments to real-world and larger datasets (e.g., ImageNet, CelebA).
- Integrate with transformer-based architectures.
