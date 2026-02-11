# kria_kv260_fruit_ripeness_detector_Bharat_AI-SoC_Student_Challenge
Edge AI fruit ripeness detector built for the Kria KV260. Features an INT8-quantized MobileNetV2 running on the FPGA DPU, paired with custom ARM-side ROI extraction and temporal smoothing.

# 🍎 Edge-AI Fruit Ripeness Detection on Kria KV260

### Hardware/Software Co-Design Project Submission
**Platform:** Xilinx Kria KV260 Vision AI Starter Kit • **Framework:** Vitis AI (VART)

[![arm developer labs](https://img.shields.io/badge/arm_developer_Labs-blueviolet)](https://arm-university.github.io/Arm-Developer-Labs/Challenge_Page.html)
[![Hardware](https://img.shields.io/badge/Hardware-Kria%20KV260-orange)](#)
[![Model](https://img.shields.io/badge/Model-MobileNetV2%20INT8-blue)](#)
[![Lang](https://img.shields.io/badge/Language-C++%20%7C%20OpenCV-purple)](#)
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen)](#)

🎥 **[Watch our 2-Minute Demo Video Here](#)** *(Link pending)*

---

## 🧠 Introduction

Deploying deep learning models on edge devices requires a careful balance of compute capability, power consumption, and latency. This project explores a **Hardware/Software Co-Design** approach to build a real-time fruit ripeness classification system. Instead of relying solely on the CPU (which introduces high latency) or moving the entire pipeline to the FPGA (which lacks control flexibility), this system partitions the workload. It leverages the ARM processor for dynamic data preparation and the Xilinx Deep Learning Processor Unit (DPU) for heavy convolutional acceleration, aligning perfectly with modern edge-computing paradigms.

## 🎯 Project Objective

The objective of this project is to design and demonstrate an edge-capable classification system that can:
- Accurately classify fruit ripeness into predefined categories using a live camera feed.
- Achieve real-time performance through hardware acceleration.
- Implement intelligent software optimizations (ROI tracking, temporal smoothing) to reduce unnecessary compute overhead.
- Demonstrate a complete Edge-AI pipeline using the Vitis AI Runtime (VART).

## 🧪 Ripeness Classes Considered

The system classifies inputs into four distinct ripeness stages:

[![Unripe](https://img.shields.io/badge/Class-Unripe-darkgreen)](#)
[![Ripe](https://img.shields.io/badge/Class-Ripe-yellow)](#)
[![Overripe](https://img.shields.io/badge/Class-Overripe-orange)](#)
[![Rotten](https://img.shields.io/badge/Class-Rotten-darkred)](#)

| Ripeness Stage | Description |
|--------------|-------------|
| **Unripe** | Early stage, firm texture, typically green coloration. |
| **Ripe** | Optimal consumption stage, peak color and texture. |
| **Overripe** | Past optimal stage, structural softening, minor blemishes. |
| **Rotten** | Severe degradation, significant dark spots, and texture collapse. |

## ⚙️ Hardware/Software Partitioning Strategy

This project follows a strict **Co-Design philosophy**: *Let the CPU handle control; let the FPGA handle math.*

* **ARM Cortex-A53 (Software):** Handles OpenCV camera capture, ROI extraction, BGR-to-RGB conversion, INT8 quantization, and post-processing (Dequantization, Softmax, Argmax, Temporal Smoothing).
* **FPGA Fabric / DPU (Hardware):** Executes the computationally intensive convolution layers of the INT8 quantized MobileNetV2 model.

## ⚡ Key Software Optimizations

To achieve maximum efficiency on the KV260, custom ARM-side logic was implemented prior to DPU interaction:
- **ROI-Based Inference Skipping:** The system calculates pixel differences between frames. If the Region of Interest (ROI) hasn't significantly changed, DPU inference is bypassed.
- **Temporal Consistency Filtering:** A sliding-window majority vote is applied over the last 5 frames to prevent UI flickering and ensure stable predictions.
- **End-to-End INT8 Pipeline:** Preprocessing outputs are quantized to exactly match the DPU's INT8 expectations, eliminating redundant datatype conversions on the FPGA.

## 📁 Repository Structure

```text
KV260-Fruit-Ripeness-Detection/
├── docs/                     # Detailed methodology and project report
├── src/                      # C++ source code for the ARM processor
├── models/                   # Compiled DPU models and TFLite variants
├── results/                  # Evaluation metrics and latency results
└── README.md                 # Main project documentation
