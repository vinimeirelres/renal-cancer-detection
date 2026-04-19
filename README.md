# Comparative Analysis of Deep Learning for Renal Cancer Diagnosis

[![DOI](https://img.shields.io/badge/DOI-10.22456%2F2175--2745.150824-blue)](https://doi.org/10.22456/2175-2745.150824)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Paper](https://img.shields.io/badge/Paper-RITA%202026-green)](https://doi.org/10.22456/2175-2745.150824)

📄 **[Read the full paper](https://doi.org/10.22456/2175-2745.150824)**

---

This repository contains the source code and analysis scripts for the paper  
**"Impact of Wavelet Pre-processing on Deep Learning Architectures for Renal Cancer Diagnosis"**,  
published in *Revista de Informática Teórica e Aplicada (RITA)*.

The study performs a systematic comparison of Deep Learning architectures (CNNs and Vision Transformers) with and without wavelet-based pre-processing.

👉 **Main insight:** the best solution is not the most complex — it's the most efficient.

---

## 🧠 Key Findings

- **MobileNetV2** achieves **100% test accuracy on this dataset** without wavelet pre-processing  
- **ResNet50** reaches 100%, but **depends on wavelet filtering**  
- Wavelet impact is **architecture-dependent**  
- **ViT performance drops significantly** with wavelet  
- Grad-CAM shows CNNs focus precisely on tumor regions  

---

## 📊 Results Snapshot

### Performance Comparison (Test Set)

| Model            | Dataset    | Accuracy | AUC  |
|------------------|-----------|----------|------|
| MobileNetV2      | Original  | 100.00%  | 1.00 |
| ResNet50         | Wavelet   | 100.00%  | 1.00 |
| EfficientNet-B7  | Original  | 99.89%   | 1.00 |
| ViT-B/16         | Original  | 88.70%   | 0.93 |
| ViT-B/16         | Wavelet   | 75.30%   | 0.84 |

---

## 🔧 Environment Setup

```bash
git clone https://github.com/vinimeirelres/renal-cancer-detection.git
cd renal-cancer-detection
pip install -r requirements.txt
```

---

## 💾 Dataset

Dataset: **CT KIDNEY DATASET: Normal-Cyst-Tumor and Stone**  
🔗 https://www.kaggle.com/datasets/nazmul0087/ct-kidney-dataset-normal-cyst-tumor-and-stone

### 📌 Preparation

- Used classes: **Normal** and **Tumor**
- Tumor: 2,283 images  
- Normal: 5,077 images  
- Balanced via **random undersampling**
- Final dataset: **4,566 images (2,283 per class)**

### 📂 Structure

```bash
dataset/
├── Normal/
└── Tumor/
```

### ⚙️ Preprocessing

- Grayscale (1-channel)
- Resize: 224×224
- Split: 60/20/20
- Seed: 42

---

## 🚀 Reproducing the Results

### Part 1 — Train Models

Notebook: `detectarim_cnn_explicavel.ipynb`

Run **12 experiments**:

| Model | Wavelet |
|------|--------|
| alexnet | on/off |
| vgg16 | on/off |
| resnet50 | on/off |
| mobilenet_v2 | on/off |
| efficientnet_b7 | on/off |
| vit_b_16 | on/off |

Outputs:
```
treinamentos/
```

---

### Part 2 — Aggregate Results

Notebook: `metricas_agrupadas.ipynb`

Generates:
```
treinamentos/relatorios_agrupados/
```

---

## 🔁 Reproducibility Notes

- PyTorch 2.6 / Python 3.11  
- GPU: NVIDIA T4 (Colab)  
- Batch size: 16  
- Optimizer: Adam (1e-3)  
- Loss: Cross-Entropy  
- Early stopping (patience=10)  
- Max epochs: 500  
- Seed: 42  
- Augmentation: flip, rotation, affine  

---

## 📜 How to Cite

```bibtex
@article{santos2026impact,
  title={Impact of Wavelet Pre-processing on Deep Learning Architectures for Renal Cancer Diagnosis},
  author={Santos, Vin{\'i}cius Meireles Pereira and Patrocinio, Ana Claudia and de Sousa, Pedro Moises},
  journal={Revista de Inform{\'a}tica Te{\'o}rica e Aplicada},
  volume={33},
  number={2},
  pages={285--293},
  year={2026},
  doi={10.22456/2175-2745.150824}
}
```

---
## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
