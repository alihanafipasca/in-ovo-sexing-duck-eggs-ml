# 🦆 Early In-Ovo Sexing of Mojosari Duck Eggs on Day 5

## 📌 Overview

This repository contains the implementation and experimental resources for **early in-ovo sexing of Mojosari duck eggs on day 5 of incubation** using hybrid feature fusion and conventional machine-learning methods.

The study integrates **external morphological measurements**, **embryonic vascular features extracted from RGB candling images**, and **texture features based on Gray-Level Co-occurrence Matrix (GLCM)**. The resulting 15-feature representation is evaluated using four conventional machine-learning classifiers.

A total of **503 Mojosari duck eggs** were analyzed. The main experimental dataset was divided into **353 training eggs, 50 validation eggs, and 100 independent test eggs**. Model configuration and feature-group decisions were determined using the development data, while the independent test set was reserved for final evaluation.

---

## 🎯 Objectives

The main objectives of this study are to:

- **Develop an early in-ovo sexing approach** for Mojosari duck eggs at day 5 of incubation.

- **Integrate complementary feature representations**, combining five external morphological features obtained through direct egg measurements with five embryonic vascular and five GLCM-based textural features extracted from RGB candling images.

- **Investigate the contribution of different feature groups** through statistical analysis and feature ablation analysis to characterize and discriminate male and female Mojosari duck embryos.

- **Evaluate conventional machine-learning classifiers**, including Logistic Regression, Random Forest, SVM-RBF, and XGBoost, using different feature representations under a consistent evaluation protocol.

---

## 🧩 External Morphological Measurements

External morphological measurements were obtained independently from the RGB candling images using physical measurement instruments. **Egg length and width were measured using a digital caliper**, while **egg weight was measured using a digital weighing scale**.

The Shape Index was calculated from the measured width and length using:

```text
Shape Index = (Width / Length) × 100
```

Eccentricity was calculated from the measured length and width. These measurements form the external morphological feature group and were not derived from image processing.

---

## 🖼️ Image Processing and Segmentation

RGB candling images acquired on **day 5 of incubation** were processed through a sequence of preprocessing and segmentation procedures.

### Image Preprocessing

The preprocessing pipeline includes:

1. **ROI and Resize**
2. **Background Removal**
3. **R-component Extraction**
4. **G-component Extraction**
5. **R-channel Binarization**
6. **Image Multiplication**

### Embryonic Vascular Segmentation

The vascular segmentation pipeline includes:

1. **CLAHE (Contrast Limited Adaptive Histogram Equalization)**
2. **Background Removal**
3. **Morphological Opening**
4. **Adaptive Thresholding**
5. **Binarization**
6. **Image Complement**
7. **Masking and Erosion**
8. **Frangi Vesselness Filter**
9. **Frangi Vessel Visibility Enhancement**

The processed and segmented images were subsequently used for embryonic vascular and texture feature extraction.

---

## 🏷️ Ground Truth Labeling

Ground-truth sex labels were obtained after hatching using **vent sexing of one-day-old ducklings (DOD)**. Each egg was assigned a female (`F`) or male (`M`) label based on the observed sex of the corresponding duckling.

---

## 🔬 Feature Extraction

The final hybrid representation consists of **15 features** from three feature groups.

### 1. Morphological External

Five external morphological features were used:

* Length
* Width
* Shape Index
* Weight
* Eccentricity

### 2. Embryonic Vascular

Five features were extracted from the segmented embryonic vascular structures:

* Perimeter
* Sinus Terminalis Area
* Embryo Vascular Area
* Fractal Dimension
* Branch Nodes

### 3. Texture (GLCM)

Five textural features were extracted using the Gray-Level Co-occurrence Matrix (GLCM):

* GLCM Energy
* GLCM Contrast
* GLCM Correlation
* GLCM Homogeneity
* GLCM Entropy

The final hybrid representation contains **15 predictive features**.

---

## 📈 Statistical Analysis

Differences between female and male eggs were evaluated using:

* Mean ± Standard Deviation
* Welch's independent t-test
* Holm multiple-comparison adjustment
* Hedges' *g* effect size
* BCa bootstrap 95% confidence intervals

The statistical analysis was used to characterize differences between female and male eggs across the extracted morphological, embryonic vascular, and textural features.

---

## 🔍 Feature Importance

Feature importance was evaluated using **ReliefF**. The feature-importance analysis was performed using the training subset to prevent the independent test set from contributing to feature-importance estimation.

The resulting ReliefF scores were used to rank the relative importance of the extracted features for subsequent interpretation.

---

## 🤖 Machine Learning Models

Four conventional machine-learning classifiers were evaluated:

1. **Logistic Regression**
2. **Random Forest**
3. **SVM with RBF kernel**
4. **XGBoost**

Hyperparameter optimization was performed using **Bayesian optimization with BayesSearchCV** and stratified cross-validation on the development data.

For models requiring feature scaling, **RobustScaler** was used within the modeling workflow.

The independent test set was kept separate from model configuration and hyperparameter optimization.

---

## 🧩 Feature Ablation Analysis

Feature ablation analysis was performed using seven feature-group configurations:

1. Morphological
2. Embryologic Vascular
3. Textural (GLCM)
4. Morphological + Embryologic Vascular
5. Morphological + Textural (GLCM)
6. Embryologic Vascular + Textural (GLCM)
7. Morphological + Embryologic Vascular + Textural (GLCM)

The ablation analysis was conducted using the **development data** to examine the contribution of different feature groups.

The independent test set was not used for feature-group selection or ablation-based configuration decisions.

---

## 🧪 Final Independent Test Results

After the model configuration had been fixed using the development data, the final configuration was evaluated once on an **untouched independent test set of 100 eggs**.

The independent test set was reserved exclusively for final evaluation and was not used for feature-group selection, hyperparameter optimization, or model configuration.

---

## 🔒 Experimental Protocol

The main experimental protocol follows a strict **development-test separation** using 503 Mojosari duck eggs:

```text
503 eggs
│
├── Development: 403 eggs
│   ├── Training:    353 eggs
│   └── Validation:   50 eggs
│
└── Independent Test: 100 eggs
```

All model and feature-group configuration decisions were made using the **development data only**. The independent test set was not used for hyperparameter optimization, feature-group selection, or ablation-based selection. It was reserved for a single final evaluation after the model configuration had been fixed.

The predefined training, validation, and independent test indices are provided in:

```text
Features/splits/
├── train_indices.csv
├── validation_indices.csv
└── test_indices.csv
```

---

## 🔄 Batch-Held-Out Robustness

An additional **batch-held-out evaluation** was conducted to assess model robustness across different acquisition stages.

In **Experiment A (Stage 1 → Stage 2)**, Acquisition Stage 1 was used for model development, while Acquisition Stage 2 was completely held out as an independent test set.

### Batch-Held-Out Dataset

```text
Experiment_A_Stage1_to_Stage2
│
├── Acquisition Stage 1
│   ├── Training:    185 eggs
│   │   ├── Female:   78
│   │   └── Male:    107
│   │
│   └── Validation:   47 eggs
│       ├── Female:   20
│       └── Male:     27
│
└── Acquisition Stage 2
    └── Independent Test: 271 eggs
        ├── Female:       96
        └── Male:        175
```
In this batch-held-out experiment, the model was developed using only the **Stage 1 training and validation subsets** and subsequently evaluated on the completely held-out **Stage 2 independent test set**.
This evaluation provides an additional assessment of model performance when tested on eggs acquired during a different acquisition stage.

---

## 📊 Evaluation Metrics

Model performance was evaluated using multiple complementary metrics:

| Metric                      | Description                                                 |
| --------------------------- | ----------------------------------------------------------- |
| **Accuracy**                | Proportion of correctly classified eggs                     |
| **Balanced Accuracy**       | Mean recall across female and male classes                  |
| **Macro-F1**                | Average F1-score across the two classes                     |
| **Female Recall**           | Proportion of female eggs correctly identified              |
| **Male Recall**             | Proportion of male eggs correctly identified                |
| **ROC-AUC**                 | Area under the receiver operating characteristic curve      |
| **Confusion Matrix**        | Distribution of correct and incorrect predictions           |
| **95% Confidence Interval** | Bootstrap-based uncertainty interval for evaluation metrics |

Because the class distribution was not perfectly balanced, **Balanced Accuracy and Macro-F1** were reported alongside conventional accuracy.

---

# 📂 Repository Structure

```text
In-Ovo_Sexing_Duck_Eggs/
│
├── README.md
├── requirements.txt
│
├── Features/
│   ├── Morphological_Raw.xlsx
│   ├── Calculate_Morphological.csv
│   ├── Embryo_Vascular1.csv
│   ├── Embryo_Vascular2.csv
│   ├── GLCM.csv
│   ├── GroundTruth_VentSexing.csv
│   ├── Morphological.csv
│   ├── Embryologic_Vascular.csv
│   ├── Textural_GLCM.csv
│   ├── Morphological_Embryologic_Vascular.csv
│   ├── Morphological_Textural_GLCM.csv
│   ├── Embryologic_Vascular_Textural_GLCM.csv
│   ├── Morphological_Embryologic_Vascular_Textural_GLCM.csv
│   ├── Acquisition_Stage.csv
│   ├── Hybrid_Feature.csv
│   │
│   └── splits/
│       ├── train_indices.csv
│       ├── validation_indices.csv
│       └── test_indices.csv
│
├── Preprocessing/
│   ├── ROI_Resize/
│   ├── Remove_Background/
│   ├── R_Component/
│   ├── G_Component/
│   ├── Binarization/
│   └── Multiplication_Mask/
│
├── Segmentation/
│   ├── CLAHE_Day-5/
│   ├── Remove_Background/
│   ├── Morphological_Opening_Day-5/
│   ├── Adaptive_Threshold_Day-5/
│   ├── Binarization/
│   ├── Complement_Day-5/
│   ├── Masking_Erosion_Day-5/
│   ├── Frangi_Vesselness_Day-5/
│   └── Frangi_Vessel_Visibility_Day-5/
│
├── Experiments/
│   ├── preprocessing.ipynb
│   ├── segmentation.ipynb
│   ├── features.ipynb
│   ├── statistical_analysis.ipynb
│   └── in-ovo-sexing-ml.ipynb
│
└── results/
    ├── model_selection.csv
    ├── metrics.csv
    ├── selected_hyperparameters.csv
    ├── predictions.csv
    ├── confusion_matrices.csv
    ├── acquisition_stage_class_distribution.csv
    ├── etc...
```

# 📋 Directory Description

| Directory        | Description                                                                                                                                                    |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Features/`      | Raw morphological measurements, extracted features, ground-truth labels, acquisition-stage information, combined feature datasets, and predefined data splits. |
| `Preprocessing/` | Intermediate outputs from RGB image preprocessing.                                                                                                             |
| `Segmentation/`  | Intermediate outputs from embryonic vascular segmentation and vessel enhancement.                                                                              |
| `Experiments/`   | Jupyter notebooks for preprocessing, segmentation, feature extraction, statistical analysis, and machine-learning experiments.                                 |
| `results/`       | Model configurations, selected hyperparameters, evaluation metrics, predictions, confusion matrices, and acquisition-stage distributions.                      |

---

## 🧩 Dependencies

The experiments were implemented in **Python** using Jupyter Notebook.

The main libraries include:

* NumPy
* Pandas
* OpenCV
* scikit-image
* scikit-learn
* scikit-optimize
* XGBoost
* scikit-rebate
* Matplotlib
* Seaborn
* OpenPyXL

Install all required dependencies using:

```bash
pip install -r requirements.txt
```

---

## 🚀 Running the Notebook

The notebooks can be executed sequentially according to the following workflow.

### 1. Image Preprocessing

```text
Experiments/preprocessing.ipynb
```

This notebook performs ROI extraction, resizing, background removal, RGB component processing, binarization, and image multiplication.

### 2. Embryonic Vascular Segmentation

```text
Experiments/segmentation.ipynb
```

This notebook performs CLAHE enhancement, morphological processing, adaptive thresholding, masking, erosion, Frangi vesselness filtering, and vessel visibility enhancement.

### 3. Feature Extraction

```text
Experiments/features.ipynb
```

This notebook calculates the morphological, embryonic vascular, and GLCM texture features and generates the combined feature datasets.

### 4. Statistical Analysis

```text
Experiments/statistical_analysis.ipynb
```

This notebook performs descriptive and inferential statistical analyses of the extracted features.

### 5. Machine-Learning Experiments

```text
Experiments/in-ovo-sexing-ml.ipynb
```

This notebook performs feature ablation analysis, model configuration, hyperparameter optimization, final independent-test evaluation, and batch-held-out robustness evaluation.

---

## 📚 Citation

If you use this repository, dataset processing workflow, feature extraction procedures, or experimental implementation in your research, please cite the associated publication:

```text
M. Ali Hanafiah, et al.
Early In-Ovo Sexing of Mojosari Duck Eggs on Day 5 Using Hybrid Feature Fusion and Machine Learning.
```

The complete citation will be updated after the associated manuscript is formally published.

---

## 👨‍💻 Author

**M. Ali Hanafiah**

Research on early non-invasive in-ovo sexing of Mojosari duck eggs using external morphological measurements, image-derived features, and conventional machine learning.

---

## 📄 License

MIT License

Copyright (c) 2026 M. Ali Hanafiah

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...

---

## ⭐ Acknowledgement

The authors acknowledge the contribution of the hatchery and personnel involved in the acquisition of Mojosari duck eggs, candling images, morphological measurements, and post-hatching ground-truth sex determination.
