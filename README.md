# CNN for Facial Emotion Recognition
### [LINK TO DRAFT REVIEW PAPER](https://drive.google.com/file/d/10JkByTfotQW8Hb-yZplxNjC1y4_lm0ZD/view?usp=sharing)
or 

https://drive.google.com/file/d/10JkByTfotQW8Hb-yZplxNjC1y4_lm0ZD/view?usp=sharing

This repository contains the implementation and experimental results of the paper:

> **"Designing a Lightweight Custom CNN for Efficient Emotion Recognition from Facial Expressions"**  

The project focuses on developing a **computationally efficient Convolutional Neural Network (CNN)** for facial emotion recognition using the **FER2013 dataset**. The approach achieves a strong trade-off between **accuracy and model size**, making it suitable for real-time or mobile applications.

---

## 🧠 Overview

Facial Emotion Recognition (FER) is an essential component of affective computing and human–computer interaction. Traditional deep models (e.g., VGG, ResNet) achieve high accuracy but are too large for low-power environments.  
This project introduces a **custom lightweight CNN** that maintains competitive accuracy while reducing parameters nearly **10×** compared to standard architectures.

---

## 📊 Dataset

**Dataset:** [FER2013](https://www.kaggle.com/datasets/msambare/fer2013)  
- Total images: **35,887** grayscale images (48×48 pixels)  
- Categories (7): `Angry`, `Disgust`, `Fear`, `Happy`, `Neutral`, `Sad`, `Surprise`  
- Split:  
  - Train: 28,709  
  - Validation: 3,589  
  - Test: 3,589  

**Data Augmentation:**  
Random rotation (±15°), horizontal flip, zoom (0.9–1.1), brightness variation (±20%), and small translations (±10%).

---

## 🧩 Model Architecture

The network consists of **three convolutional blocks** and a **dense classifier head**, designed for balanced performance and efficiency.

| Block | Layers | Filters | Dropout | Notes |
|:------|:--------|:---------|:----------|:------|
| 1 | Conv2D ×2 + BN + ReLU + MaxPool | 64 | 0.3 | Initial feature extraction |
| 2 | Conv2D ×2 + BN + ReLU + MaxPool | 128 | 0.4 | Intermediate feature learning |
| 3 | Conv2D ×2 + BN + ReLU + MaxPool | 256 | 0.5 | High-level feature extraction |
| Dense | FC-256 + BN + ReLU + Dropout + Softmax(7) | – | 0.5 | Classification head |

- **Total parameters:** ~2.1M  
- **Optimizer:** Adam (lr = 0.001)  
- **Loss:** Categorical Cross-Entropy  
- **Epochs:** 50  
- **Batch Size:** 32  
- **Early stopping and LR reduction** were used to prevent overfitting.

---

## 🚀 Results

| Metric | Validation Score |
|:--------|:----------------:|
| **Accuracy** | **66.17%** |
| **Training Accuracy** | 68.4% |
| **Validation Loss Plateau** | ~Epoch 35 |

### Per-Class F1-Scores
| Emotion | F1-Score |
|:--------:|:---------:|
| Angry | 0.49 |
| Disgust | 0.30 |
| Fear | 0.40 |
| Happy | 0.84 |
| Neutral | 0.59 |
| Sad | 0.55 |
| Surprise | 0.79 |

**Highlights**
- Excellent performance on **Happy** and **Surprise** classes  
- Common confusions among **Angry**, **Sad**, and **Fear**  
- Maintains only ~2% training–validation gap → strong generalization  
- **Inference time:** ~2.3 ms per image  

---

## ⚖️ Comparison with Existing Models

| Model | Accuracy | Parameters | Notes |
|:------|:----------|:------------|:------|
| VGG-16 | 70.8% | ~20M | Heavy architecture |
| ResNet-50 | 69.3% | ~25M | High compute cost |
| EfficientNet-B0 | 71.2% | ~15M | Good balance |
| **Proposed CNN** | **66.17%** | **2.1M** | Lightweight & real-time ready |

---

## 💻 How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/FER2013.git
   cd FER2013-LightweightCNN
