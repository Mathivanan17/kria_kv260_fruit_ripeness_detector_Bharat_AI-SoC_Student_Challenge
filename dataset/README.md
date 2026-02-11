# 📂Dataset Organization

[![Dataset](https://img.shields.io/badge/Format-Categorical-yellow)](#)
[![Classes](https://img.shields.io/badge/Classes-4-brightgreen)](#)

## 📌Overview
This directory describes the dataset structure used to train and validate the MobileNetV2 fruit ripeness classification model. Because this is a multi-class image classification task, the dataset is organized using an industry-standard categorical directory structure.

## 🧪Ripeness Classes
The dataset is balanced across four distinct phases of fruit ripeness:
1. **Unripe**
2. **Ripe**
3. **Overripe**
4. **Rotten**

## 📁Directory Structure
To ensure reproducibility and seamless integration with ML training pipelines, the dataset is strictly split into training and validation sets. Within each split, the images are sorted into subdirectories named after their respective class labels:

```text
dataset/
├── train/
│   ├── unripe/       # Training images of unripe fruit (.jpg/.png)
│   ├── ripe/         # Training images of ripe fruit
│   ├── overripe/     # Training images of overripe fruit
│   └── rotten/       # Training images of rotten fruit
│
└── val/
    ├── unripe/       # Validation images for unripe fruit
    ├── ripe/         # Validation images for ripe fruit
    ├── overripe/     # Validation images for overripe fruit
    └── rotten/       # Validation images for rotten fruit
