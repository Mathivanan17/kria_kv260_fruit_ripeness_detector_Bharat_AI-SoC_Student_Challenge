# 💻ARM Pipeline Source Code

[![Language](https://img.shields.io/badge/Language-C++-blue)](#)
[![Library](https://img.shields.io/badge/Library-OpenCV-green)](#)
[![API](https://img.shields.io/badge/API-Vitis%20AI%20(VART)-purple)](#)

## 📌Overview
This directory contains the C++ application executed by the ARM Cortex-A53 processor on the Kria KV260. It orchestrates the entire Edge-AI pipeline, handling real-time camera capture, software-level optimizations, and delegation of neural network math to the FPGA's DPU.

## 🧩Module Breakdown
* `main.cpp`: The core execution loop handling camera capture, timing, and system orchestration.
* `preprocess_int8.cpp`: Handles image resizing, BGR to RGB conversion, and strict INT8 quantization to perfectly match the `.xmodel` numerical contract.
* `postprocess_softmax.cpp`: Dequantizes DPU logits back to FP32, applies a numerically stable Softmax, and performs Argmax to determine the final class.
* `roi_crop.cpp` & `roi_utils.cpp`: Extracts the center Region of Interest (ROI) and computes frame-to-frame pixel differences to enable inference skipping.
* `temporal_filter.cpp`: Applies a sliding-window majority vote over the last 5 frames to stabilize predictions and eliminate UI flickering.
* `dpu_inference.cpp`: Interfaces with the Vitis AI Runtime (VART) to push input tensors to the FPGA DPU and retrieve output logits.
