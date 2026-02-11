# 🧠Design Approach

[![Methodology](https://img.shields.io/badge/Methodology-Co--Design-blue)](#)
[![Optimization](https://img.shields.io/badge/Optimization-Edge%20AI-orange)](#)

## 📌Problem Understanding
Agricultural and food-processing industries require high-throughput, real-time sorting mechanisms. While deep learning provides excellent accuracy for grading fruit ripeness, running Convolutional Neural Networks (CNNs) entirely on standard embedded CPUs results in high latency and bottlenecked throughput. Conversely, implementing the entire pipeline in pure FPGA hardware limits flexibility and makes dynamic tasks (like camera control and UI) difficult.

## ⚙️Why Edge-AI and Co-Design?
To solve this, we adopted a **Hardware/Software Co-Design** methodology utilizing the Xilinx Kria KV260. 

> **The Core Philosophy:** Let the ARM processor handle dynamic, control-heavy software tasks, and let the FPGA (DPU) handle massive, parallel matrix operations.

By processing at the edge rather than the cloud, we achieve:
- **Zero Network Latency:** Immediate classification per frame.
- **Data Privacy & Bandwidth Savings:** Raw video feeds never leave the device.
- **Power Efficiency:** Utilizing the DPU consumes a fraction of the power of a desktop GPU.

## 🔄End-to-End Data Pipeline
Our system architecture explicitly partitions the MobileNetV2 inference pipeline:

1. **Frame Acquisition (ARM):** OpenCV captures frames from the video feed.
2. **Software Preprocessing (ARM):** - Extracts a localized Region of Interest (ROI).
   - Resizes the crop to 128x128.
   - Converts BGR to RGB.
   - Performs strict INT8 quantization matching the exact scales/zero-points expected by the model.
3. **Hardware Acceleration (DPU/FPGA):** The Vitis AI Runtime (VART) feeds the INT8 tensor to the DPU, which executes the deep-wise separable convolutions of MobileNetV2.
4. **Software Postprocessing (ARM):**
   - Receives INT8 logits from the DPU.
   - Dequantizes to FP32.
   - Applies a numerically stable Softmax and Argmax to determine class probabilities.

## ⚡Custom Software Optimizations
To ensure the pipeline remains strictly real-time, we introduced two major software-level optimizations on the ARM processor:

### 1. ROI-Based Inference Skipping
Fruit in an inspection line or camera frame often remains stationary for consecutive frames. We implemented an absolute-difference algorithm that compares the current ROI to the previous one. If the pixel delta is below a tuned threshold, **DPU inference is bypassed entirely**, and the previous label is reused. This dramatically drops active compute load.

### 2. Temporal Consistency Filtering
CNNs can occasionally suffer from frame-to-frame noise, causing the output label to flicker (e.g., Ripe -> Overripe -> Ripe). We implemented a sliding-window majority vote over a history of 5 frames. The final output is the statistically dominant class, ensuring a rock-solid user interface.
