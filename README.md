# Comparative Analysis of Deep Learning for Renal Cancer Diagnosis

[![DOI](https://img.shields.io/badge/DOI-10.22456%2F2175--2745.150824-blue)](https://doi.org/10.22456/2175-2745.150824)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Paper](https://img.shields.io/badge/Paper-RITA%202026-green)](https://doi.org/10.22456/2175-2745.150824)

📄 **[Read the full paper](https://doi.org/10.22456/2175-2745.150824)**

---

This repository contains the source code and analysis scripts for the paper **"Impact of Wavelet Pre-processing on Deep Learning Architectures for Renal Cancer Diagnosis"**, published in *Revista de Informática Teórica e Aplicada (RITA)*.

The study performs a systematic comparison of Deep Learning architectures (CNNs and Vision Transformers) with and without wavelet-based pre-processing.

---

## Key Findings

- **MobileNetV2** achieves **100% test accuracy on this dataset** without wavelet pre-processing, establishing itself as the most efficient and pragmatic solution.
- **ResNet50** also reaches 100% accuracy, but requires the wavelet pre-processing pipeline to do so.
- Wavelet pre-processing has a complex, **architecture-dependent impact**: it benefits some CNNs (like ResNet50) but significantly degrades the performance of the Vision Transformer (ViT).
- Visual explainability (Grad-CAM) confirms that high-performance CNNs focus precisely on tumorous regions.

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

To ensure reproducibility, all project dependencies are listed in `requirements.txt`. Creating a virtual environment is highly recommended.

1. **Clone the repository:**
```bash
git clone https://github.com/vinimeirelres/renal-cancer-detection.git
cd renal-cancer-detection
```

2. **Install the dependencies:**
```bash
pip install -r requirements.txt
```

---

## 💾 Dataset

This study uses the **CT KIDNEY DATASET: Normal-Cyst-Tumor and Stone**, which is publicly available on Kaggle.

- **Link:** https://www.kaggle.com/datasets/nazmul0087/ct-kidney-dataset-normal-cyst-tumor-and-stone

### 📌 Dataset Preparation

Only the **"Normal"** and **"Tumor"** classes were used in this study.

From the original dataset:
- **Tumor:** 2,283 images  
- **Normal:** 5,077 images  

To address class imbalance, a **random undersampling** strategy was applied to the majority class ("Normal"), resulting in a **balanced dataset of 4,566 images (2,283 per class)**.

### 📂 Expected Folder Structure

For the scripts to work correctly, organize the dataset as follows:

```bash
./dataset/
├── Normal/
│   ├── image1.jpg
│   ├── image2.png
│   └── ...
└── Tumor/
    ├── image_tumor_1.jpg
    ├── image_tumor_2.png
    └── ...
```

### ⚙️ Preprocessing Notes

- Images are converted to **grayscale (1-channel)**
- Resized to **224×224 pixels**
- Dataset is split into:
  - 60% training  
  - 20% validation  
  - 20% test  
- Split is **fixed using a random seed (42)**

> Full dataset handling and preprocessing details are described in the published paper.

---

## 🚀 Reproducing the Results

The experimental process is divided into two parts: training each model individually and then aggregating the results for comparative analysis.

### Part 1: Training the Models (`detectarim_cnn_explicavel.ipynb`)

This notebook trains, validates, and tests a single model configuration at a time. To reproduce the full results of the paper, it must be executed 12 times, once for each configuration.

1. **Open the notebook** `detectarim_cnn_explicavel.ipynb` in Google Colab or a local Jupyter environment  
2. **Set the configuration** in the initial cells for one of the experiments listed below  
3. **Execute all cells** in sequence  
4. **Verify the output:** Results will be saved in `treinamentos/[model_name]/[original_or_wavelet]/`  
5. **Repeat** for all 12 configurations  

#### Experiment Configurations

| Run | `model_name`        | `USE_WAVELET_DATASET` |
|:---:|:-------------------|:----------------------|
| 1   | `'alexnet'`        | `False`               |
| 2   | `'alexnet'`        | `True`                |
| 3   | `'vgg16'`          | `False`               |
| 4   | `'vgg16'`          | `True`                |
| 5   | `'resnet50'`       | `False`               |
| 6   | `'resnet50'`       | `True`                |
| 7   | `'mobilenet_v2'`   | `False`               |
| 8   | `'mobilenet_v2'`   | `True`                |
| 9   | `'efficientnet_b7'`| `False`               |
| 10  | `'efficientnet_b7'`| `True`                |
| 11  | `'vit_b_16'`       | `False`               |
| 12  | `'vit_b_16'`       | `True`                |

---

### Part 2: Generating Comparative Reports (`metricas_agrupadas.ipynb`)

This notebook loads the saved results from all experiments to generate the final comparative analyses, tables, and figures.

1. Ensure all 12 runs from Part 1 are completed  
2. Open `metricas_agrupadas.ipynb`  
3. Run all cells  
4. Outputs will be saved in `treinamentos/relatorios_agrupados/`  

---

## 🔁 Reproducibility Notes

- **Framework:** PyTorch 2.6 (torchvision, ImageNet pre-trained weights)  
- **Language:** Python 3.11  
- **Hardware:** NVIDIA T4 GPU (Google Colab, CUDA)  
- **Batch size:** 16  
- **Optimizer:** Adam (lr = 1e-3)  
- **Loss:** Cross-Entropy  
- **Training:** Early Stopping (patience = 10), up to 500 epochs  
- **Data split:** 60/20/20 (fixed)  
- **Seed:** 42  
- **Input:** 224×224, normalized using training statistics  
- **Augmentation:** Horizontal flip, rotation (±10°), affine (training only)  

Additional implementation details are available in the published paper.

---

## 📜 How to Cite

If you use this code or our findings in your research, please cite:

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

Meireles Pereira Santos, V., Patrocinio, A. C., & de Sousa, P. M. (2026).  
**Impact of Wavelet Pre-processing on Deep Learning Architectures for Renal Cancer Diagnosis**.  
*Revista de Informática Teórica e Aplicada*, 33(2), 285–293.  
https://doi.org/10.22456/2175-2745.150824

---

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
