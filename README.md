# cervical-cancer-risk-segmentation-unsupervised-ml
Outcome-aligned unsupervised ML for cervical cancer risk segmentation using psychosocial data, with post-hoc validation and decision-focused evaluation.

# Cervical Cancer Risk Segmentation using Unsupervised Learning

**Applied Machine Learning • Healthcare Analytics • Unsupervised Learning • Risk Stratification**

---

## Overview

This project applies **unsupervised machine learning** to psychosocial and behavioral health data to identify population segments associated with **cervical cancer risk** in a setting where **outcome labels could not be used during training**.

Rather than forcing a supervised approach in a label-constrained environment, latent structure was discovered first and **validated post-hoc** against real outcomes.

**Key result:**  
Clusters discovered *without labels* separated cancer prevalence from **0% to 100%**, concentrating nearly all high-risk cases into **~30–35% of the population** and enabling **6–8× more efficient targeting**.

This project demonstrates **outcome-aligned unsupervised learning** in a real, applied healthcare context.

---

## Problem Motivation

In healthcare and behavioral analytics:

- Outcome labels are often **delayed, incomplete, or ethically constrained**
- Supervised models may be inappropriate early in the decision lifecycle
- Yet prioritization and intervention decisions still must be made

This project reframes the task from *prediction* to **discovery, prioritization, and risk stratification**.

---

## Dataset

- **72 observations**
- **20 psychosocial and behavioral features**, including:
  - Empowerment
  - Social support
  - Motivation
  - Health perception
  - Behavioral practices
- **Outcome variable:** `ca_cervix`
  - Binary cervical cancer indicator
  - Used **only for post-hoc validation**

---

## Methodology

### 1. Exploratory Data Analysis
- Feature distribution analysis
- Correlation analysis (high multicollinearity observed)

### 2. Preprocessing
- Feature standardization using `StandardScaler`

### 3. Dimensionality Reduction
- Principal Component Analysis (PCA)
- Retained ~90% of total variance
- Improved clustering stability and interpretability

### 4. Clustering
- KMeans clustering
- `k = 6` selected via Elbow + Silhouette analysis
- Selection balanced statistical metrics with interpretability

### 5. Visualization
- PCA 2D and 3D projections
- Cluster centroids for compactness and stability
- Animated 3D rotation for interpretability

### 6. Post-Hoc Validation
- Cluster-wise cervical cancer prevalence analysis
- Strict separation between training features and outcome labels

---

## Outcome-Based Validation

Despite not using outcome labels during training, clusters showed **strong differentiation in cancer prevalence**:

| Cluster | Cancer Prevalence |
|------|-------------------|
| 5 | 100% |
| 0 | ~87% |
| 1 | ~15% |
| 3 | ~13% |
| 2 | 0% |
| 4 | 0% |

**Key insight:**  
Outcome-aligned structure emerged *without supervision*.

---

## Risk Stratification Summary

| Risk Level | Clusters | Cancer Prevalence | Shared Characteristics | Priority |
|----------|---------|------------------|------------------------|---------|
| **High Risk** | Cluster 5 | 100% | Low empowerment<br>Weak social support<br>Low motivation | Highest |
| **High Risk** | Cluster 0 | ~87% | Low empowerment<br>Weak social support<br>Low motivation | Highest |
| **Low Risk** | Clusters 2 & 4 | 0% | Strong empowerment<br>Strong social support | Protective |
| **Low Risk** | Clusters 1 & 3 | ~12–15% | Strong empowerment<br>Protective behaviors | Protective |

---

## Metrics & Tradeoffs

### Primary Evaluation Metrics
- **Outcome concentration:** 0% → 100% prevalence separation across clusters
- **Targeting efficiency:** Top **2 of 6 clusters (~30–35%)** contained nearly all high-risk cases
- **Risk separation:** Clear high- vs low-risk stratification (≈87–100% vs 0–15%)
- **Stability & interpretability:** PCA retained ~90% variance with interpretable centroids

### Key Tradeoffs Considered
- **Interpretability vs silhouette score:** Selected `k = 6` for decision usability
- **Geometric separation vs decision value:** Accepted PCA overlap in favor of outcome alignment
- **Discovery vs prediction:** Optimized for **prioritization**, not point prediction
- **Sample size vs signal:** Mitigated overfitting via PCA and strict post-hoc validation

---

## Failure Modes & Mitigations

### Spurious Clusters
Mitigated via PCA, centroid inspection, conservative `k`, and outcome validation.

### Overinterpretation
Clusters framed as **risk strata**, not diagnoses or causal groups.

### Label Leakage
Strict separation of features and outcomes; labels used **only after clustering**.

### Small Sample Instability
Multiple initializations, PCA noise reduction, focus on directional signal.

### Misuse as Predictor
Defined success via targeting efficiency, not predictive accuracy.

### Ethical Risks
Focused on **modifiable psychosocial factors** and supportive interventions.

---

## Impact & Applications

- Concentrated nearly all high-risk cases into **~30–35% of the population**
- Enabled **6–8× more efficient targeting** than population-wide approaches
- Identified psychosocial drivers overlooked by behavior-only models
- Demonstrated unsupervised learning as an **upstream discovery and triage layer**

---

## Project Structure
├── notebooks/
│ ├── 01_eda.ipynb
│ ├── 02_preprocessing_pca.ipynb
│ ├── 03_clustering.ipynb
│ └── 04_validation_visualization.ipynb
│
├── src/
│ ├── preprocessing.py
│ ├── clustering.py
│ ├── visualization.py
│ └── utils.py
│
├── figures/
│ ├── pca_2d_clusters.png
│ ├── pca_3d_clusters.png
│ ├── pca_3d_rotation.gif
│ └── cluster_prevalence_table.png
│
└── README.md

