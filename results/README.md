# 📊Evaluation & Hardware Performance

[![Accuracy](https://img.shields.io/badge/Accuracy-Pending-yellow)](#)
[![Performance](https://img.shields.io/badge/Latency-Real--Time-brightgreen)](#)

## 📌Overview
This directory serves as the central hub for our model's evaluation metrics and the hardware performance benchmarks of our co-design system on the Kria KV260.

## 🧪Model Classification Metrics
*These metrics evaluate the model's ability to accurately classify fruit ripeness on an unseen test dataset.*

| Metric | Value |
|--------|-------|
| **Overall Accuracy** | *TBD%* |
| **Precision** | *TBD* |
| **Recall** | *TBD* |
| **F1-Score** | *TBD* |

## ⚡Hardware & System Performance
*These metrics demonstrate the efficiency of our ARM+DPU Co-Design pipeline.*

| Performance Metric | Result | Notes |
|--------------------|--------|-------|
| **End-to-End Latency** | *TBD ms* | Time from camera capture to final ARM post-processing. |
| **DPU Only Latency** | *TBD ms* | Time spent purely executing convolutions on the FPGA. |
| **Throughput (FPS)** | *TBD FPS* | Frames processed per second in real-time mode. |

## 📁Directory Structure
Visual evaluation artifacts will be uploaded here following final hardware testing:

```text
results/
├── figures/
│   ├── confusion_matrix.png     # Class-wise accuracy visualization
│   └── latency_benchmark.png    # ARM vs DPU time-cost analysis
└── README.md                    # Results documentation
