# Adversarial CNN — Robustness Against Adversarial Attacks on MNIST

A deep learning project focused on evaluating and improving the robustness of Convolutional Neural Networks (CNNs) against adversarial attacks on the MNIST handwritten digit dataset. The project benchmarks multiple white-box attack techniques and implements adversarial training strategies to significantly improve model robustness while maintaining high clean-data accuracy.

---

## Overview

Modern neural networks are highly vulnerable to adversarial perturbations — small, often imperceptible modifications to input data that can drastically change model predictions.  

This project:
- Trains a baseline CNN on MNIST
- Evaluates its robustness against multiple adversarial attacks
- Implements adversarial training defenses
- Compares robustness across different clean/adversarial training ratios

---

## Model Architecture

The baseline CNN consists of:

- 2 Convolutional Layers
- Max Pooling Layers
- 2 Fully Connected Dense Layers
- ReLU activations
- Softmax output layer

Dataset:
- **MNIST Handwritten Digits**
- 60,000 training images
- 10,000 test images

---

## Adversarial Attacks Implemented

### 1. FGSM (Fast Gradient Sign Method)
A single-step gradient-based attack that perturbs inputs in the direction of the loss gradient.

### 2. PGD (Projected Gradient Descent)
An iterative and stronger version of FGSM that repeatedly updates perturbations within a bounded region.

### 3. Carlini-Wagner (CW) Attack
An optimization-based attack designed to generate minimal but highly effective adversarial perturbations.

### 4. DeepFool
An iterative attack that pushes samples toward the nearest decision boundary with minimal perturbation.

---

## Experimental Pipeline

### Step 1 — Train Baseline CNN

Train a standard CNN on clean MNIST data.

- Clean Accuracy: **99.08%**

---

### Step 2 — Evaluate Under Adversarial Attacks

The trained model is attacked using all four adversarial methods.

| Attack     | Accuracy |
|------------|----------|
| Clean      | 99.08%   |
| FGSM       | 97.1%    |
| PGD        | 96.1%    |
| CW         | 20.3%    |
| DeepFool   | 0.0%     |

### Observation
While the baseline model performs well under FGSM and PGD, optimization-based attacks such as CW and DeepFool completely collapse model performance.

---

### Step 3 — Adversarial Training

New models are trained using mixtures of:
- Clean samples
- FGSM-generated adversarial samples

Training ratios explored:

- 10% adversarial / 90% clean
- 30% adversarial / 70% clean
- 50% adversarial / 50% clean
- 70% adversarial / 30% clean
- 90% adversarial / 10% clean

---

## Best Performing Defense

### Optimal Ratio: 50% Clean + 50% Adversarial

| Attack     | Accuracy |
|------------|----------|
| Clean      | 99.18%   |
| FGSM       | 98.5%    |
| PGD        | 98.7%    |
| CW         | 99.0%    |
| DeepFool   | 99.1%    |

### Key Findings

- Robustness improved from **0–20%** to **98–99%**
- Clean accuracy slightly improved despite adversarial training
- Defense generalized successfully to unseen attack types
- The model trained only on FGSM examples still resisted CW and DeepFool attacks effectively

---

## Defense Ratio Comparison

| Defense Ratio | Clean | FGSM | PGD | CW | DeepFool |
|----------------|------|------|------|------|------|
| No Defense | 99.08% | 97.1% | 96.1% | 20.3% | 0.0% |
| 10% Adversarial | 99.07% | 98.4% | 98.5% | 98.7% | 98.2% |
| 30% Adversarial | 99.14% | 98.6% | 98.7% | 99.0% | 98.9% |
| **50% Adversarial** | **99.18%** | **98.5%** | **98.7%** | **99.0%** | **99.1%** |
| 70% Adversarial | 99.07% | 98.5% | 98.6% | 98.8% | 98.8% |
| 90% Adversarial | 98.99% | 98.4% | 98.4% | 98.6% | 98.8% |

---

## Tech Stack

- Python
- TensorFlow / Keras
- NumPy
- Matplotlib

---

## Installation

Clone the repository:

```bash
git clone <repo-url>
cd Adversarial-CNN
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Author

Khushi Yadav
