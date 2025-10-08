# Comparative Analysis of Deep Learning for Renal Cancer Diagnosis

[![Paper-License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

This repository contains the source code and analysis scripts for the paper **"Impact of Wavelet Pre-processing on Deep Learning Architectures for Renal Cancer Diagnosis"**. and is eligible for publication in a special issue of the *Revista de Informática Teórica e Aplicada (RITA)*, conditional upon formatting adjustments.

The study performs a systematic analysis comparing different Deep Learning architectures (CNNs and Vision Transformers) with and without a wavelet-based pre-processing pipeline. Our primary finding identifies the **MobileNetV2** architecture, without complex pre-processing, as the optimal computational pipeline, offering a state-of-the-art performance with superior computational efficiency.

## Key Findings
- **MobileNetV2** achieves 100% test accuracy without wavelet pre-processing, establishing itself as the most efficient and pragmatic solution.
- **ResNet50** also reaches 100% accuracy, but requires the wavelet pre-processing pipeline to do so.
- Wavelet pre-processing has a complex, **architecture-dependent impact**: it benefits some CNNs (like ResNet50) but significantly degrades the performance of the Vision Transformer (ViT).
- Visual explainability (Grad-CAM) confirms that high-performance CNNs focus precisely on tumorous regions.

---

## 🔧 Environment Setup

To ensure reproducibility, all project dependencies are listed in `requirements.txt`. Creating a virtual environment is highly recommended.

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/your-repository-name.git](https://github.com/your-username/your-repository-name.git)
    cd your-repository-name
    ```

2.  **Install the dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

---

## 💾 Dataset

This study uses the **CT KIDNEY DATASET: Normal-Cyst-Tumor and Stone**, which is publicly available on Kaggle.

- **Link:** [https://www.kaggle.com/datasets/nazmul0087/ct-kidney-dataset-normal-cyst-tumor-and-stone](https://www.kaggle.com/datasets/nazmul0087/ct-kidney-dataset-normal-cyst-tumor-and-stone)

For the scripts to work correctly, download the dataset and organize it in the following folder structure, containing only the two classes used in the study ("Normal" and "Tumor"):

```
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


---

## 🚀 Reproducing the Results

The experimental process is divided into two parts: training each model individually and then aggregating the results for comparative analysis.

### Part 1: Training the Models (`detectarim_cnn_explicavel.ipynb`)

This notebook trains, validates, and tests a single model configuration at a time. To reproduce the full results of the paper, it must be executed 12 times, once for each configuration.

1.  **Open the notebook** `detectarim_cnn_explicavel.ipynb` in Google Colab or a local Jupyter environment.
2.  **Set the configuration** in the initial cells for one of the experiments listed in the table below.
3.  **Execute all cells** in sequence.
4.  **Verify the output:** A folder will be created under `treinamentos/[model_name]/[original_or_wavelet]/` containing the model weights (`.pth`), metric reports (`.pkl`, `.txt`), and Grad-CAM heatmaps.
5.  **Repeat** for all 12 configurations.

#### **Experiment Configurations**

| Run | `model_name`         | `USE_WAVELET_DATASET` |
|:---:|:---------------------|:----------------------|
| 1   | `'alexnet'`          | `False`               |
| 2   | `'alexnet'`          | `True`                |
| 3   | `'vgg16'`            | `False`               |
| 4   | `'vgg16'`            | `True`                |
| 5   | `'resnet50'`         | `False`               |
| 6   | `'resnet50'`         | `True`                |
| 7   | `'mobilenet_v2'`     | `False`               |
| 8   | `'mobilenet_v2'`     | `True`                |
| 9   | `'efficientnet_b7'`  | `False`               |
| 10  | `'efficientnet_b7'`  | `True`                |
| 11  | `'vit_b_16'`         | `False`               |
| 12  | `'vit_b_16'`         | `True`                |

### Part 2: Generating Comparative Reports (`metricas_agrupadas.ipynb`)

This notebook loads the saved results from all 12 experiments to generate the final comparative analyses, tables, and graphs presented in the paper.

1.  **Prerequisite:** Ensure that all 12 training runs from Part 1 have been completed successfully.
2.  **Open the notebook** `metricas_agrupadas.ipynb`.
3.  **Execute all cells**. The notebook will automatically find the results from the `treinamentos/` directory.
4.  **Final Output:** The comparative reports and figures will be saved to the `treinamentos/relatorios_agrupados/` folder.

---

## 📜 How to Cite

If you use this code or our findings in your research, please cite our work. As the paper is accepted at the conference but not yet in the journal, please use the following BibTeX entry:

```bibtex
@inproceedings{santos2025impact,
  title={Impact of Wavelet Pre-processing on Deep Learning Architectures for Renal Cancer Diagnosis},
  author={Santos, Vinícius Meireles Pereira and Patrocinio, Ana Claudia and de Sousa, Pedro Moises},
  booktitle={XX Workshop on Computer Vision (WVC'25)},
  year={2025},
  note={Eligible for publication in a special issue of Revista de Informática Teórica e Aplicada (RITA)}
}

---
---
## 📄 License
The code in this repository is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
