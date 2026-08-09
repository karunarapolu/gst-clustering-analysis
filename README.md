# GST State-wise Analysis and Clustering

## Overview

This project presents a statistical and unsupervised learning analysis of **state-wise Goods and Services Tax (GST) collections in India** across multiple financial years.

The objective is to investigate how GST collections vary across States and Union Territories, identify patterns in their collection profiles, and group states with similar characteristics using **K-Means clustering**.

The analysis combines:

* Exploratory Data Analysis (EDA)
* Descriptive statistics
* Data visualization
* Year-over-year growth analysis
* K-Means clustering
* Principal Component Analysis (PCA)
* Volatility analysis using the Coefficient of Variation

The project is also being developed into a **research paper**, with further analysis and interpretation currently in progress.

---

## Objectives

The project aims to explore the following questions:

1. How do GST collections vary across Indian States and Union Territories?
2. How have GST collections changed across financial years?
3. Which states have similar GST collection profiles?
4. Can states be grouped according to similar year-over-year GST growth patterns?
5. How does the relative volatility of GST collections differ between states?
6. Can unsupervised learning reveal meaningful groups within the state-wise GST data?

---

## Dataset

The dataset contains GST collection information for Indian States and Union Territories across the following financial years:

* 2020–21
* 2021–22
* 2022–23
* 2023–24
* 2024–25

The dataset also contains aggregate information relating to GST collections, including domestic and import components.

### Data preprocessing

Before statistical analysis and clustering, summary/aggregate rows are separated from the state-level observations. The state-level observations are then used for descriptive analysis and clustering.

The notebook loads the dataset using:

```python
df = pd.read_csv("gst_data.csv")
```

The dataset should therefore be placed in the appropriate `data/` directory when reproducing the analysis.

See [`data/README.md`](data/README.md) for information about the dataset source and usage.

---

# Methodology

## 1. Exploratory Data Analysis

The first stage of the project examines the structure and characteristics of the dataset.

The analysis includes:

* First five observations
* Dataset information and data types
* Descriptive statistics
* State-wise summary statistics
* Year-wise statistical analysis

For each state, the following statistics are calculated across the observed financial years:

* Mean
* Median
* Minimum
* Maximum
* Standard deviation
* Variance

The analysis also examines distributional characteristics using:

* Skewness
* Kurtosis

These statistics provide an initial understanding of the differences and variation in GST collections across states.

---

## 2. State-wise GST Visualization

Several visualizations are used to examine the temporal and geographical variation in GST collections.

### GST Collection Heatmap

A heatmap is used to visualize state-wise GST collections across financial years.

This allows differences between states and changes over time to be examined simultaneously.

### Multi-year State Comparison

A grouped bar chart compares GST collections across states and financial years.

### Year-wise Mean GST Collection

The mean GST collection across states is calculated for each financial year to examine the overall change in state-level collections over time.

### State Comparison

The project also includes a direct comparison of GST collections for selected states, including Maharashtra and Karnataka.

### Total GST Collection

Aggregate GST collections are visualized across the observed financial years.

### Domestic vs Import GST Collection

Domestic and import GST collections are compared across financial years to examine their relative contribution to total GST collections.

---

# 3. K-Means Clustering Based on GST Collections

The first clustering analysis groups states according to their **absolute GST collection profiles**.

The financial-year GST collection values are used as features.

### Feature matrix

The five financial-year values form the feature matrix:

```text
2020-21
2021-22
2022-23
2023-24
2024-25
```

Because the features can differ substantially in magnitude, the values are standardized using `StandardScaler`.

```python
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

K-Means clustering is then applied with three clusters.

```python
KMeans(n_clusters=3, random_state=42)
```

The resulting clusters represent groups of states with similar GST collection profiles across the observed years.

The states belonging to each cluster are displayed for interpretation.

---

# 4. PCA Visualization of GST Clusters

Since the clustering is performed using multiple financial-year variables, Principal Component Analysis (PCA) is used to project the standardized data into two dimensions.

```python
PCA(n_components=2)
```

The first two principal components are then plotted, with states labelled according to their cluster.

This provides a two-dimensional visual representation of the similarity structure identified by K-Means.

> **Important:** PCA is used here for visualization; the clustering itself is performed on the standardized feature matrix.

---

# 5. Year-over-Year Growth Analysis

Absolute GST collections do not necessarily capture how quickly a state's collections are changing.

Therefore, a second clustering analysis is performed using **year-over-year GST growth rates**.

For each state, the growth rate between consecutive financial years is calculated as:

```text
Growth Rate (%) =
(Current Year Collection - Previous Year Collection)
--------------------------------------------------- × 100
             Previous Year Collection
```

This produces growth features for the consecutive financial-year periods.

The resulting growth-rate features are standardized before applying K-Means clustering.

Three growth-based clusters are generated.

This allows states to be compared according to their **growth trajectories**, rather than their absolute GST collection levels.

---

# 6. PCA Visualization of Growth Clusters

PCA is again applied to the standardized growth-rate features to reduce the dimensionality to two components.

The resulting two-dimensional representation is used to visualize the growth-based clusters.

States are labelled in the plot to make the resulting groups easier to interpret.

---

# 7. Volatility Analysis

A third perspective examines the **relative volatility** of GST collections across states.

For each state, three measures are calculated:

### Mean GST Collection

The average GST collection across the observed financial years.

### Standard Deviation

The standard deviation of GST collection across the observed years.

### Coefficient of Variation

The coefficient of variation is calculated as:

```text
CV = Standard Deviation / Mean
```

Unlike standard deviation alone, the coefficient of variation measures dispersion relative to the magnitude of the state's GST collections.

This makes it useful for comparing the relative variability of states with substantially different collection levels.

---

# 8. Volatility Clustering

The coefficient of variation is used as the feature for a separate K-Means clustering analysis.

States are grouped into three volatility clusters.

The resulting clusters are examined using a scatter plot of:

* Mean GST Collection
* Coefficient of Variation

This allows states to be viewed simultaneously in terms of their collection magnitude and relative volatility.

---

# Clustering Approaches

The project therefore examines state-level GST data from three different perspectives:

| Analysis                  | Features Used                  | Purpose                                           |
| ------------------------- | ------------------------------ | ------------------------------------------------- |
| GST Collection Clustering | Financial-year GST collections | Identify states with similar collection profiles  |
| Growth Clustering         | Year-over-year growth rates    | Identify states with similar growth patterns      |
| Volatility Clustering     | Coefficient of Variation       | Identify states with similar relative variability |

This multi-dimensional approach allows the same states to be studied not only by **how much GST they collect**, but also by **how their collections grow and fluctuate over time**.

---

# Technologies Used

### Programming Language

* Python

### Data Analysis

* Pandas
* NumPy
* SciPy

### Visualization

* Matplotlib
* Seaborn
* Plotly

### Machine Learning

* Scikit-learn

  * K-Means
  * StandardScaler
  * PCA

### Development Environment

* Google Colab
* Jupyter Notebook

---

# Repository Structure

```text
gst-state-clustering/
├── LICENSE
├── README.md
├── data
│   ├── README.md
│   └── gst_data.csv
├── figures  
├── gst_analysis_and_clustering.ipynb
└── requirements.txt

```

---

# Reproducing the Analysis

## 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/gst-state-clustering.git
cd gst-state-clustering
```

## 2. Install dependencies

```bash
pip install -r requirements.txt
```

## 3. Open the notebook

Open:

```text
notebooks/GST_State_Analysis_and_Clustering.ipynb
```

The notebook can be run using Jupyter Notebook/JupyterLab or Google Colab.


---


## Author

**Disha**

B.Sc. Mathematics, Statistics and Data Science

**Karuna**

B.Sc. Mathematics, Statistics and Computer



---

## License

The source code in this repository is provided under the MIT License.

The dataset is subject to the terms and license of its original data source. See [`data/README.md`](data/README.md) for dataset attribution and licensing information.
