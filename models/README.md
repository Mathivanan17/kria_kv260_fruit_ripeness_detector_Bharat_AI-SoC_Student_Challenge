# 🧠Compiled Edge Models

[![Model](https://img.shields.io/badge/Architecture-MobileNetV2-blue)](#)
[![Quantization](https://img.shields.io/badge/Quantization-INT8-orange)](#)
[![Format](https://img.shields.io/badge/Format-.xmodel-purple)](#)

## 📌Overview
This directory contains the model artifacts required for Edge deployment on the Xilinx Kria KV260. Deploying to the Deep Learning Processor Unit (DPU) requires strict model conversion and quantization steps to ensure real-time performance without sacrificing accuracy.

## 🔄The Deployment Pipeline
To achieve hardware acceleration, our standard MobileNetV2 model underwent the following transformation:
1. **Training:** The base MobileNetV2 architecture was trained on our categorical fruit ripeness dataset.
2. **Quantization:** The FP32 (floating-point) model was quantized to **INT8** using a representative calibration dataset. This step is mandatory for DPU execution and drastically reduces memory footprint and power consumption.
3. **Compilation:** The quantized model was compiled using the **Vitis AI Compiler**, generating the final `.xmodel` instruction set tailored specifically for the KV260's DPU architecture.

## 📁Directory Structure

```text
models/
├── fruit_net.xmodel      # The final compiled instruction set for the Xilinx DPU
├── quantized.tflite      # The intermediate INT8 quantized model
└── README.md             # Model documentation
