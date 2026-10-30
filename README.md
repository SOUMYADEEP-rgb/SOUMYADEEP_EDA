# Exploratory Data Analysis - Gunnels Dataset

## Overview

This project performs a comprehensive Exploratory Data Analysis (EDA) on the Gunnels dataset using Python and Google Colab.

The project is divided into four phases:

- **Phase 1:** Data understanding, cleaning, transformation, and exploratory analysis
- **Phase 2:** Statistical analysis, advanced visualization, and clustering
- **Phase 3.1:** Principal Component Analysis (PCA) and dimensionality reduction
- **Phase 3.2:** Logistic regression for predicting gunnel presence

The objective is to understand the distribution of gunnel presence and investigate relationships between environmental, shoreline, and habitat-related variables.

---

# Dataset

The dataset contains **1,592 observations** and **11 original variables** describing gunnel presence along with different shoreline and habitat characteristics.

### Dataset Source

https://raw.githubusercontent.com/salemprakash/EDA/main/Data/Gunnels.csv

### Main Variables

| Variable | Description |
|---|---|
| `rownames` | Serial number (dropped during analysis) |
| `Gunnel` | Gunnel presence (1) / absence (0) |
| `Time` | Observation time (minutes after midnight) |
| `Fromlow` | Minutes from low tide |
| `Slope` | Shoreline slope |
| `Rw` | Rockweed/Algae cover (proportion, 0-1) |
| `Amphiso` | Crustacean food density level (0-4) |
| `Subst` | Substratum type (1-13) |
| `Pool` | Pool condition (binary) |
| `Water` | Water condition (binary) |
| `Cobble` | Cobble presence (binary) |

---

# Phase 1 - Exploratory Data Analysis

Phase 1 focuses on understanding, cleaning, transforming, and exploring the dataset.

## Tasks Performed

### 1. Data Understanding

- Loaded the Gunnels dataset directly from the GitHub URL
- Examined the dataset dimensions
- Examined column names and data types
- Displayed the first 10 and last 10 observations
- Examined random samples
- Generated descriptive statistics (mean, median, standard deviation, variance, min, max, quartiles)

### 2. Data Quality Analysis

- Checked for missing values and calculated missing-value percentages (with a bar chart)
- Checked for duplicate observations
- Examined unique values and value counts
- Separated categorical and numerical variables

### 3. Data Cleaning

- Dropped duplicate observations where applicable
- Verified data types
- Checked the consistency of categorical and binary variables
- Dropped the `rownames` identifier column

### 4. Data Transformation

Additional variables were created to improve analysis:

- Converted observation time into hours (`Time_Hours`)
- Created `Time_Period` categories (Night, Morning, Afternoon, Evening)
- Created readable labels for binary variables:
  - `Gunnel_Label` (Absent / Present)
  - `Pool_Label`, `Water_Label`, `Cobble_Label` (No / Yes)

### 5. Univariate Analysis

- Histograms with KDE (Slope, Rw)
- Count plots (Gunnel presence, Amphiso food density)
- Frequency and relative frequency analysis

### 6. Bivariate Analysis

- Gunnel Presence vs Shoreline Slope (box plot)
- Gunnel Presence vs Rockweed/Algae Cover (box plot)
- Food Density vs Rockweed/Algae Cover (box plot)
- Time vs Minutes from Low Tide (scatter plot)

### 7. Multivariate Analysis

- Multivariate scatter plots (Slope, Rw, Amphiso, Gunnel presence; Time, Rw, Gunnel, Pool)
- Faceted visualizations (`FacetGrid` by Pool condition)
- Correlation heatmap
- Pair plot colored by gunnel presence
- Group-wise mean summary by gunnel presence

### 8. Phase 1 Output

A cleaned dataset was generated: `Gunnels_Cleaned.csv`

---

# Phase 2 - Statistical Analysis and Clustering

Phase 2 extends the exploratory analysis using statistical techniques, advanced visualizations, and unsupervised learning.

## 1. 1D Statistical Analysis

Variables analyzed: `Time`, `Fromlow`, `Slope`, `Rw`, `Amphiso`, `Subst`

- Skewness and kurtosis
- Outlier detection using the IQR method
- Box plots and histograms
- Frequency, relative frequency, and binned frequency distributions (pie and bar charts for `Time_Period`, binned `Fromlow`)

## 2. 2D / Bivariate Statistical Analysis

### Pearson and Spearman Correlation

| Pair | Result |
|---|---|
| Slope vs Rw | Pearson r = 0.020 (not significant); Spearman rho = 0.112 (significant) |
| Time vs Fromlow | r = 0.216 (significant) |
| Rw vs Amphiso | r = 0.230 (significant) |
| Slope vs Fromlow | r = 0.091 (significant) |

### Independent T-Test (Gunnel Absent vs Present, Welch's)

Significant differences were found for `Time`, `Fromlow` (strongest), `Rw`, and `Amphiso`. `Slope` showed no significant difference.

### Chi-Square Test of Independence

Gunnel presence was significantly associated with `Pool`, `Water`, and `Cobble` (strongest association with `Cobble`).

### One-Way ANOVA

`Rw` differs significantly across `Amphiso` food-density levels (F = 33.38, p < 0.001).

### Additional Visualizations

- Heatmap of Gunnel vs Pool (row-normalized)
- Regression plots and joint plots (Slope vs Rw)
- Contingency tables (Pool vs Water) with row and column percentages
- Stacked and grouped bar plots
- Side-by-side box plot and violin plot

## 3. 3D and Multivariate Analysis

- 3D scatter plots (Slope, Rw, Time_Hours; Fromlow, Rw, Amphiso)
- Annotated correlation heatmap for the six numerical variables
- Extended pair plot colored by gunnel presence
- 4-variable bubble plot (Slope, Rw, Amphiso as size, Fromlow as color)
- Group statistics across Gunnel x Pool combinations, faceted box plots, and grouped bar chart with error bars
- Multivariate logistic regression (`statsmodels`) on `Slope`, `Rw`, `Amphiso`, `Fromlow`, with odds ratios. `Fromlow` and `Amphiso` were the significant predictors.

## 4. K-Means Clustering

**Features:** `Time`, `Fromlow`, `Slope`, `Rw`, `Amphiso`, `Subst` (standardized with `StandardScaler`)

- Elbow method (WCSS / inertia) and silhouette scores for k = 2 to 10
- Final model with **4 clusters** (sizes: 594, 632, 82, 284)
- PCA-based 2D cluster visualization
- Cluster profiling using mean values of the original variables

Cluster highlights:

| Cluster | Notable characteristics |
|---|---|
| 0 | Low `Rw`, far from low tide |
| 1 | High `Rw`, closer to low tide |
| 2 | Very steep slope (small group) |
| 3 | High `Amphiso` food density, higher `Subst` |

## 5. Hierarchical Clustering

- Ward linkage with Euclidean distance
- Dendrogram on a random sample of 100 observations
- Agglomerative clustering with **4 clusters** (sizes: 545, 403, 282, 362)
- PCA-based visualization
- Cross-tabulation and heatmap comparing K-Means and hierarchical assignments

---

# Phase 3 - Principal Component Analysis (PCA)

Phase 3 applies PCA to reduce dimensionality and understand which variables drive variation in the dataset.

### Data Preparation

- Loaded the dataset again and dropped `rownames` and `Gunnel`
- Removed **90 duplicate rows** (1,592 to 1,502 observations)
- Checked for all-missing and constant columns (none found)
- Median imputation pipeline for numeric columns (no missing values were present)
- Standardized the 9 features (`Time`, `Fromlow`, `Slope`, `Rw`, `Amphiso`, `Subst`, `Pool`, `Water`, `Cobble`)

### Analysis Performed

- Eigenvalues, explained variance, and cumulative variance table
- Scree plot and cumulative variance plot (80% / 90% / 95% thresholds)
- 2D PCA projection
- PCA loadings table, loadings heatmap, and per-component loading bar charts
- 3D PCA visualization

### Results

| Metric | Value |
|---|---|
| PC1 explained variance | 23.74% |
| PC2 explained variance | 19.65% |
| First 2 components (cumulative) | 43.38% |
| First 3 components (cumulative) | 57.98% |
| Components for 80% variance | 6 |
| Components for 90% variance | 7 |
| Components for 95% variance | 8 |

- **PC1** is driven mainly by `Cobble` and `Subst`.
- **PC2** is driven mainly by `Water`, `Rw`, and `Pool`.
- The variance is spread fairly evenly across components, so a 2D projection captures well under half of the total variance.

---

# Phase 4 - Logistic Regression (Module 7)

A supervised classification model was built to predict gunnel presence.

### Setup

- Features: `Time`, `Fromlow`, `Slope`, `Rw`, `Amphiso`, `Subst`, `Pool`, `Water`, `Cobble`
- Target: `Gunnel`
- Stratified 80/20 train-test split (train: 1,273, test: 319; `random_state=42`)
- Features standardized using `StandardScaler` (fitted on the training set only)
- Model: `LogisticRegression(max_iter=1000)`

### Evaluation

| Metric | Value |
|---|---|
| Accuracy | 0.9687 |
| Precision (Present) | 0.00 |
| Recall (Present) | 0.00 |
| F1 Score (Present) | 0.00 |
| ROC-AUC | 0.9392 |

The model reaches high accuracy only because it predicts "Absent" for nearly every observation, which is expected with a ~3% positive class. The ROC-AUC of 0.94 shows the model still ranks observations well. Evaluation included a confusion matrix, ROC curve, classification report, and coefficient chart.

### Strongest Coefficients (standardized)

| Feature | Coefficient |
|---|---|
| Fromlow | -2.159 |
| Cobble | 1.030 |
| Time | -0.473 |
| Slope | 0.388 |
| Pool | 0.327 |

Gunnels are more likely to be present closer to low tide and where cobble is present.

### Suggested Improvements

- Use `class_weight="balanced"` or resampling (e.g., SMOTE) to handle class imbalance
- Tune the decision threshold using the precision-recall curve
- Report PR-AUC alongside ROC-AUC

---

# Statistical and Machine Learning Techniques Used

### Descriptive Analysis

- Mean, median, standard deviation, variance, minimum and maximum, quartiles

### Statistical Analysis

- Skewness, kurtosis
- Pearson and Spearman correlation
- Independent (Welch's) t-test
- Chi-square test of independence
- One-way ANOVA
- Multivariate logistic regression with odds ratios (`statsmodels`)

### Exploratory Visualization

- Histograms, box plots, violin plots, count plots
- Scatter plots, regression plots, joint plots, bubble plots
- Heatmaps, pair plots, facet grids
- Pie charts, stacked and grouped bar charts
- 3D visualizations

### Machine Learning

- K-Means clustering, elbow method, silhouette analysis
- Hierarchical clustering, Ward linkage, dendrogram
- Principal Component Analysis (scree plot, loadings, 2D and 3D projections)
- Logistic regression classification (confusion matrix, ROC curve, ROC-AUC)

---

# Key Findings

- The dataset contains **1,592 observations** and **11 original variables**, with no missing values.
- Gunnel presence is rare: **48 of 1,592 observations (about 3.02%)**.
- `Slope` (skew 2.96), `Amphiso` (skew 1.95), and `Subst` (skew 1.23) are noticeably right-skewed. `Slope` has the most outliers by the IQR method (9.92%).
- Gunnels were observed much closer to low tide on average (mean `Fromlow` of about 38 vs 153 minutes).
- Gunnel presence is significantly associated with `Pool`, `Water`, and `Cobble`.
- In the multivariate logistic model, `Fromlow` and `Amphiso` were the significant predictors.
- K-Means and hierarchical clustering each found four groups, with partial agreement between the two methods.
- PCA shows variance is spread across several components (6 needed for 80%), with `Cobble`, `Subst`, `Water`, `Rw`, and `Pool` driving the leading components.
- The logistic regression classifier achieved 96.9% accuracy and ROC-AUC of 0.94, but failed to detect any positive cases at the default threshold because of class imbalance.

---

# Notes and Limitations

- Duplicate checking depends on whether `rownames` is present: none were found with it, while 90 duplicate rows appear once it is removed (used in Phase 3).
- The logistic regression in Phase 2 reported possible quasi-separation, so its coefficients should be interpreted with caution.
- Silhouette scores are modest (0.25 at k = 4), indicating loosely separated clusters.

---

# Output Files

- `Gunnels_Cleaned.csv` - cleaned dataset with derived variables from Phase 1

---

# Tools and Technologies

- Python
- Google Colab
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy
- Scikit-learn
- Statsmodels

---

# DONE BY 23BDS0134 (Soumyadeep Dasgupta)
