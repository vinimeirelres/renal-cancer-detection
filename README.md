# Comparative Analysis of Deep Learning for Renal Cancer Diagnosis

This repository contains the source code and analysis scripts for the paper **"Assessing the Synergy of Deep Learning Architectures and Wavelet Pre-processing for Computer-Aided Diagnosis of Renal Cancer"**.

The goal of this study was to perform a systematic analysis comparing different Deep Learning architectures (CNNs and Vision Transformers) with and without a wavelet-based pre-processing pipeline. The primary finding identifies the **MobileNetV2** architecture (without complex pre-processing) as the optimal computational pipeline, offering an ideal balance between maximum performance and computational efficiency.

---

## 🔧 Environment Setup

To ensure reproducibility, all project dependencies are listed in the `requirements.txt` files. Creating a virtual environment is recommended.

1.  Clone this repository:
    ```bash
    git clone [YOUR_REPOSITORY_URL]
    cd [FOLDER_NAME]
    ```

2.  Install the dependencies:
    ```bash
    pip install -r requirements.txt
    ```

---

## 💾 Dataset

This study uses the **CT KIDNEY DATASET: Normal-Cyst-Tumor and Stone**, which is publicly available on Kaggle.

* **Link:** [https://www.kaggle.com/datasets/nazmul0087/ct-kidney-dataset-normal-cyst-tumor-and-stone](https://www.kaggle.com/datasets/nazmul0087/ct-kidney-dataset-normal-cyst-tumor-and-stone)

For the scripts to work correctly, the dataset must be organized in the following folder structure, containing only the two classes used in the study:

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

## 🚀 Usage

IMPORTANT NOTE: To ensure full authenticity, this repository contains the exact notebooks used for the research. The training process (detectarim_cnn_explicavel.ipynb) must be run manually for each of the 12 configurations (6 models x 2 dataset types) by adjusting the model_name and USE_WAVELET_DATASET variables in the configuration cells for each run

The project is divided into two main notebooks:

### Step 1: Individual Training and Evaluation (`detectarim_cnn_explicavel.ipynb`)

This notebook is responsible for training, validating, and testing a single model at a time, saving its weights, metrics, and Grad-CAM heatmaps.

1.  **Open the notebook** `detectarim_cnn_explicavel.ipynb` in Google Colab or a local Jupyter environment.

2.  **Configure the variables** in the initial configuration cells:
    * `model_name`: Choose one of the architectures (e.g., `'mobilenet_v2'`).
    * `USE_WAVELET_DATASET`: Change to `True` or `False` to select the dataset.
    * `BASE_PATH` and `ds_path`: Adjust the paths for your environment.

3.  **Execute the cells** in sequence. The notebook will guide you through the entire process.

4.  **Output:** At the end of the execution, a folder structure will be created in `treinamentos/[model_name]/[original_or_wavelet]/`, containing the weights (`.pth`), metric reports (`.pkl`, `.txt`), confusion matrices, and heatmaps.

**Repeat this step for all 12 configurations** (6 models x 2 datasets) you wish to include in the final analysis.

### Step 2: Comparative Analysis and Report Generation (`metricas_agrupadas.ipynb`)

This notebook loads the saved results from all experiments to generate the comparative analyses and the efficiency report.

1.  **Prerequisite:** Ensure that the results from Step 1 have already been generated for all desired models.
2.  **Open the notebook** `metricas_agrupadas.ipynb`.

3.  **Configure the variables** in the configuration cells, if necessary (e.g., `BASE_PATH`).

4.  **Execute all cells**.

5.  **Output:** The notebook will save the final comparative reports and graphs to the `treinamentos/relatorios_agrupados/` folder.
