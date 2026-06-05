# Retinal Blood Vessel Segmentation

**Course:** Advanced Topics in Image Analysis  
**Datasets:** DRIVE · STARE  
**Methods:** Classical Pipeline (Matched Filter + Otsu) · Random Forest Hybrid

---

## Overview

This project implements retinal blood vessel segmentation using two approaches:

1. **Classical Pipeline** — Green channel extraction → CLAHE enhancement → Gaussian smoothing → Matched filter → Otsu thresholding → Morphological cleanup
2. **Random Forest Hybrid** — 7 hand-crafted pixel features fed into a supervised classifier, replacing the fixed Otsu threshold with a learned decision boundary

Evaluated on the **DRIVE** (20 images, provided FOV mask) and **STARE** (20 images, auto-generated FOV mask) datasets.

---

## Results

| Method | Sensitivity | Specificity | Dice | AUC |
|--------|------------|------------|------|-----|
| Classical — DRIVE | 0.6390 | 0.9504 | 0.6501 | 0.7947 |
| Classical — STARE | 0.6194 | 0.9424 | 0.6226 | 0.7809 |
| RF Hybrid — DRIVE | 0.8556 | 0.8903 | 0.6600 | 0.8729 |
| RF Hybrid — STARE | 0.8012 | 0.8854 | 0.6408 | 0.8433 |

---

## Repository Structure
```
├── Retinal_Blood_Vessel_Segmentation_Clean.ipynb   # Main notebook
├── pipeline_visualization.png                       # All pipeline stages
├── metrics_comparison.png                           # Bar chart comparison
├── per_image_dice.png                               # Per-image Dice scores
├── feature_importance.png                           # RF feature importances
└── README.md
```
---

## How to Run

### On Google Colab (recommended)

1. Upload the notebook to [colab.research.google.com](https://colab.research.google.com)
2. Download the datasets (see below) and place them in your Google Drive:
   ```
   /content/DRIVE/training/images
   /content/DRIVE/training/1st_manual
   /content/DRIVE/training/mask
   /content/STARE/stare-images
   /content/STARE/labels-vk
   ```
4. Run cells top to bottom

### Datasets

| Dataset | Link | Notes |
|---------|------|-------|
| DRIVE | [Kaggle](https://www.kaggle.com/datasets/andrewmvd/drive-digital-retinal-images-for-vessel-extraction) | 40 images (20 train / 20 test), expert-annotated ground truth masks |
| STARE | [cecas.clemson.edu](https://cecas.clemson.edu/~ahoover/stare/probing/index.html) | 20 images including pathological cases, used for cross-dataset generalization only |
## Dependencies
```
numpy
opencv-python
matplotlib
Pillow
scikit-learn
```

All available by default on Google Colab.

---

## Notebook Structure

| Section | Content |
|---------|---------|
| 1. Setup & Data Loading | Imports, dataset loading functions |
| 2. Exploratory Data Analysis | Class imbalance, sample visualizations |
| 3. Pipeline Components | Each stage built and tested individually |
| 4. Hyperparameter Search | 3-round coarse-to-fine grid search |
| 5. Final Classical Pipeline | Full pipeline with best parameters |
| 6. STARE Generalization | Auto FOV generation, cross-dataset evaluation |
| 7. Random Forest Hybrid | Feature extraction, training, evaluation |
| 8. Results & Visualizations | Summary table, charts |
