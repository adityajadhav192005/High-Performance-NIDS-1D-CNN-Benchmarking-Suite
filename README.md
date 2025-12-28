# 🛡️ High-Performance NIDS: 1D-CNN Benchmarking Suite

A specialized Deep Learning framework for **Network Intrusion Detection Systems (NIDS)**. This project implements a high-performance **1D-Convolutional Neural Network (1D-CNN)** optimized for modern GPU architectures (RTX 5090) to classify network traffic across multiple industry-standard datasets.

---

## 📖 Project Overview

This repository provides an automated benchmarking suite to evaluate AI models against diverse cybersecurity datasets. It features a robust data preprocessing pipeline designed to handle the inconsistencies (Infinity values, text labels, encoding shifts) found in large-scale network captures like CIC-IDS2017.

### Architecture Highlights:

* **Feature Space:** 78-dimensional network flow statistics.
* **Deep Learning Model:** 4-Block 1D-CNN with Batch Normalization and Dropout.
* **Hardware Acceleration:** Mixed Precision (FP16) support for high-throughput training.

---

## 🏗️ Model Architecture

The core architecture is designed to capture spatial correlations within flow features without the computational cost of 2D image conversion.

| Layer | Type | Configuration |
| --- | --- | --- |
| **Input** | Feature Vector | 1x78 Normalized Features |
| **Conv Block 1** | Conv1D + BN | 64 Filters, Kernel Size 5 |
| **Conv Block 2** | Conv1D + BN | 128 Filters, Kernel Size 5 |
| **Conv Block 3** | Conv1D + BN | 256 Filters, Kernel Size 5 |
| **Pooling** | MaxPooling | Size 3, Stride 2 |
| **Dense 1** | Fully Connected | 256 Neurons + Dropout(0.3) |
| **Dense 2** | Fully Connected | 128 Neurons |
| **Output** | Softmax | Multi-class (up to 15 categories) |

---

## 📊 Dataset Support

The suite is pre-configured to process the following datasets located in `D:\Dataset\`:

1. **Reference:** `BASE_PAPER.csv` (Primary baseline)
2. **CIC-IDS2017:** MachineLearningCVE (DDoS, Botnet, Web Attacks, etc.)
3. **CSE-CIC-IDS2018:** AWS Infrastructure Traffic captures.
4. **TrafficLabelling:** Generated Labelled Flows.

---

## ⚙️ Performance Tuning (RTX 5090)

This implementation is specifically tuned for high-end hardware:

* **Batch Size:** 2048 (Utilizing 24GB+ VRAM).
* **Mixed Precision:** `mixed_float16` global policy enabled to double training speed.
* **Optimized Loader:** Engine-level C-parsing for massive CSV files.

---

## 🚀 Installation & Usage

### 1. Requirements

```bash
pip install numpy pandas tensorflow matplotlib seaborn scikit-learn

```

### 2. File Structure

Ensure your datasets are organized as follows:

```text
D:/Dataset/
├── BASE_PAPER.csv
├── MachineLearningCSV/MachineLearningCVE/*.csv
└── CSE-CIC-IDS2018/*.csv

```

### 3. Execution

Run the ultimate benchmark script:

```bash
python ultimate_benchmark.py

```

---

## 📈 Evaluation Metrics

The framework automatically outputs a `Final_Benchmark_Report.csv` with the following:

* **Accuracy:** Overall classification success.
* **F1-Score:** Harmonic mean of Precision and Recall (Critical for imbalanced data).
* **Precision:** Measurement of False Positive rates.
* **MCC (Matthews Correlation Coefficient):** Quality of binary and multiclass classifications.
* **Training Latency:** Per-dataset training duration.

---

## 📜 License

This project is intended for research and educational purposes. Dataset rights belong to the University of New Brunswick (UNB) and relevant authors.
