# Early In-Ovo Sexing of Mojosari Duck Eggs on Day 5 Using Hybrid Feature Fusion and Machine Learning
<h1 align="center">
Early In-Ovo Sexing of Mojosari Duck Eggs on Day 5
</h1>

<h3 align="center">
Hybrid Feature Fusion and Machine Learning
</h3>

<p align="center">
Reproducibility Repository for Early Sex Classification of Mojosari Duck Eggs
</p>

---

## 📌 Overview

This repository contains the implementation, feature datasets, image-processing outputs, experimental notebooks, and evaluation results supporting the research study:

> **Early In-Ovo Sexing of Mojosari Duck Eggs on Day 5 Using Hybrid Feature Fusion and Machine Learning**

The study investigates a non-invasive approach for early sex classification of Mojosari duck eggs at day 5 of incubation by integrating external morphological measurements with embryonic vascular and Gray-Level Co-occurrence Matrix (GLCM) textural features extracted from RGB candling images.

A total of **503 labeled Mojosari duck eggs** were analyzed.

The study evaluated four machine-learning classifiers:

- Logistic Regression (LR)
- Random Forest (RF)
- Support Vector Machine with RBF kernel (SVM-RBF)
- XGBoost (XGB)

The independent test set was reserved for final evaluation after the experimental configuration had been fixed using the development data.

---

## 🎯 Research Objectives

The main objectives of this study are to:

1. Characterize sex-related differences in morphological, embryonic vascular, and textural features of Mojosari duck eggs at day 5 of incubation.
2. Extract quantitative features from RGB candling images while maintaining the eggshell intact.
3. Evaluate different combinations of feature groups for early in-ovo sex classification.
4. Evaluate conventional machine-learning classifiers using the extracted feature representation.
5. Assess classification robustness under acquisition-stage variation using a batch-held-out evaluation.

---

## 🥚 Dataset

A total of **600 Mojosari duck eggs** were initially acquired in two acquisition stages.

After incubation and ground-truth labeling, **503 eggs** were retained for analysis.

| Dataset | Number |
|---|---:|
| Initial eggs | 600 |
| Labeled eggs analyzed | 503 |

The final dataset consisted of:

| Acquisition Stage | Female | Male | Total |
|---|---:|---:|---:|
| Stage 1 | 98 | 134 | 232 |
| Stage 2 | 96 | 175 | 271 |
| **Total** | **194** | **309** | **503** |

---

## 📷 Image Acquisition

RGB candling images were acquired on **day 5 of incubation** while the eggshell remained intact.

The image acquisition procedure was conducted under controlled conditions using an RGB camera and LED-based candling illumination.

The acquired images were subsequently processed for embryonic vascular segmentation and GLCM texture extraction.

The RGB images are stored in:

```text
Day_5/
