# Exploratory Data Analysis - Gunnels Dataset

## Overview

This project performs a comprehensive Exploratory Data Analysis (EDA) on the Gunnels dataset using Python and Google Colab.

The project is divided into two phases:

- **Phase 1:** Data understanding, cleaning, transformation, and exploratory analysis
- **Phase 2:** Statistical analysis, advanced visualization, and clustering

The objective is to understand the distribution of gunnel presence and investigate relationships between environmental, shoreline, and habitat-related variables.

---

# Dataset

The dataset contains **1,592 observations** describing gunnel presence along with different shoreline and habitat characteristics.

### Dataset Source

https://raw.githubusercontent.com/salemprakash/EDA/main/Data/Gunnels.csv

### Main Variables

- `Gunnel` - Gunnel presence/absence
- `Time` - Observation time
- `Fromlow` - Minutes from low tide
- `Slope` - Shoreline slope
- `Rw` - Rockweed/Algae cover
- `Amphiso` - Crustacean food density
- `Subst` - Substratum type
- `Pool` - Pool condition
- `Water` - Water condition
- `Cobble` - Cobble presence

---

# Phase 1 - Exploratory Data Analysis

Phase 1 focuses on understanding, cleaning, transforming, and exploring the dataset.

## Tasks Performed

### 1. Data Understanding

- Loaded the Gunnels dataset
- Examined the dataset dimensions
- Examined column names and data types
- Displayed the first and last observations
- Examined random samples
- Generated descriptive statistics

### 2. Data Quality Analysis

- Checked for missing values
- Calculated missing-value percentages
- Checked for duplicate observations
- Examined unique values
- Analyzed categorical and numerical variables

### 3. Data Cleaning

- Removed duplicate observations where applicable
- Verified data types
- Checked the consistency of categorical and binary variables

### 4. Data Transformation

Additional variables were created to improve analysis:

- Converted observation time into hours
- Created `Time_Period` categories:
  - Night
  - Morning
  - Afternoon
  - Evening
- Created readable labels for binary variables such as:
  - Gunnel Presence
  - Pool Condition
  - Water Condition
  - Cobble Condition

### 5. Univariate Analysis

Individual variables were analyzed using:

- Histograms
- Count plots
- Distribution plots
- Frequency distributions
- Relative frequency analysis

### 6. Bivariate Analysis

Relationships between pairs of variables were explored using:

- Box plots
- Scatter plots
- Comparative visualizations

Examples include:

- Gunnel Presence vs Shoreline Slope
- Gunnel Presence vs Rockweed/Algae Cover
- Food Density vs Rockweed/Algae Cover
- Time vs Minutes from Low Tide

### 7. Multivariate Analysis

Multiple variables were analyzed simultaneously using:

- Multivariate scatter plots
- Faceted visualizations
- Correlation heatmaps
- Pair plots

### 8. Phase 1 Output

A cleaned dataset was generated:

`Gunnels_Cleaned.csv`

---

# Phase 2 - Statistical Analysis and Clustering

Phase 2 extends the exploratory analysis using statistical techniques, advanced visualizations, and unsupervised learning.

## 1. 1D Statistical Analysis

Univariate statistical analysis was performed on the main numerical variables.

### Techniques Used

- Skewness
- Kurtosis
- Outlier detection using the IQR method
- Box plots
- Histograms
- Frequency distributions
- Relative frequency distributions
- Binned frequency analysis

Variables analyzed include:

- Time
- Fromlow
- Slope
- Rw
- Amphiso
- Subst

The IQR method was used to identify potential outliers in numerical variables.

---

# 2. 2D / Bivariate Statistical Analysis

Relationships between pairs of variables were statistically evaluated.

### Pearson Correlation

Pearson correlation was used to measure linear relationships between numerical variables.

The analysis included relationships such as:

- Slope vs Rw
- Time vs Fromlow
- Rw vs Amphiso
- Slope vs Fromlow

### Independent T-Test

Independent t-tests were performed to compare numerical variables between:

- Gunnel Absent
- Gunnel Present

Variables analyzed include:

- Time
- Fromlow
- Slope
- Rw
- Amphiso

### Chi-Square Test

Chi-square tests of independence were performed to examine associations between Gunnel Presence and categorical variables:

- Pool
- Water
- Cobble

### ANOVA

One-way ANOVA was performed to examine differences in Rockweed/Algae Cover (`Rw`) across different `Amphiso` food-density levels.

### Additional Visualizations

- Correlation heatmaps
- Regression plots
- Contingency tables
- Comparative charts

---

# 3. 3D and Multivariate Analysis

Three-dimensional and higher-dimensional relationships were explored to understand interactions between multiple environmental and habitat variables.

The analysis considers combinations of variables such as:

- Shoreline Slope
- Rockweed/Algae Cover
- Food Density
- Minutes from Low Tide
- Gunnel Presence

These visualizations help examine relationships that cannot be fully represented using only one or two variables.

---

# 4. K-Means Clustering

K-Means clustering was performed as an unsupervised learning technique to identify groups of observations with similar environmental characteristics.

### Features Used

- `Time`
- `Fromlow`
- `Slope`
- `Rw`
- `Amphiso`
- `Subst`

The features were standardized using `StandardScaler` before clustering.

### Techniques Used

- Standardization
- Elbow Method
- WCSS / Inertia
- Silhouette Score
- K-Means clustering
- PCA-based cluster visualization
- Cluster profiling

The analysis evaluated different values of `k` using both the Elbow Method and Silhouette Scores.

A final K-Means model with **4 clusters** was implemented for further interpretation.

### Cluster Visualization

Principal Component Analysis (PCA) was used to reduce the standardized feature space to two dimensions for visualizing the K-Means clusters.

Cluster profiles were also created by calculating the mean values of the original clustering variables within each cluster.

---

# 5. Hierarchical Clustering

Hierarchical clustering was performed to provide another perspective on the grouping structure within the dataset.

### Techniques Used

- Ward linkage
- Euclidean distance
- Dendrogram
- Agglomerative clustering
- PCA-based visualization

A sample of observations was used to construct and visualize the dendrogram.

An agglomerative hierarchical clustering model with **4 clusters** was then applied to the standardized dataset.

The resulting clusters were compared and visualized using the PCA representation.

---

# Statistical and Machine Learning Techniques Used

The project incorporates the following techniques:

### Descriptive Analysis

- Mean
- Median
- Standard deviation
- Variance
- Minimum and maximum
- Quartiles

### Statistical Analysis

- Skewness
- Kurtosis
- Pearson correlation
- Independent t-test
- Chi-square test
- One-way ANOVA

### Exploratory Visualization

- Histograms
- Box plots
- Count plots
- Scatter plots
- Regression plots
- Heatmaps
- Pair plots
- Frequency charts
- Multivariate plots
- 3D visualizations

### Clustering

- K-Means clustering
- Elbow method
- Silhouette analysis
- Hierarchical clustering
- Ward linkage
- Dendrogram
- PCA-based cluster visualization

---

# Key Findings

- The dataset contains **1,592 observations** and **11 original variables**.
- No missing values were found in the original dataset.
- Gunnel presence is relatively rare, with approximately **3.02%** of observations indicating presence.
- Several variables show different distribution characteristics, including noticeable skewness in variables such as `Slope`, `Amphiso`, and `Subst`.
- Statistical tests were used to identify significant relationships and differences among environmental and habitat variables.
- Gunnel presence was statistically examined in relation to numerical and categorical habitat characteristics.
- K-Means clustering identified four groups of observations based on standardized environmental and habitat characteristics.
- Hierarchical clustering provided an additional clustering perspective using Ward linkage.
- PCA was used to visualize the clustering structure in a reduced two-dimensional space.

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

# DONE BY 23BDS0134 
