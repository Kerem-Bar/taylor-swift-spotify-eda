# 🎵 Taylor Swift Spotify Catalog - Exploratory Data Analysis (EDA)

An empirical Exploratory Data Analysis (EDA) investigating audio descriptors, structural layout, metadata parameters, and popularity as the primary metric of interest across Taylor Swift's Spotify discography.

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-3776AB?style=for-the-badge)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen?style=for-the-badge)

---


## 📌 Project Overview & Variable Taxonomy

Digital streaming platforms have revolutionized how musical trends and artistic performance are quantified, empowering creators and record labels to make data-driven decisions that mitigate commercial risks. This research conducts a structured Exploratory Data Analysis (EDA) on Taylor Swift's Spotify catalog (582 rows, 18 columns). Her multi-decade career and diverse musical style make her catalog an ideal empirical landscape to explore how acoustic features interact with audience engagement over time.

The variables are classified into four metadata defined categories:
* **Primary Metric of Interest (`int64`):** `popularity` (0 to 100 score calculated by Spotify based on stream volume and recency).
* **Audio Descriptors (`float64`):** Continuous acoustic features (`acousticness`, `danceability`, `energy`, `instrumentalness`, `liveness`, `speechiness`, `valence`, `loudness`, `tempo`).
* **Structural Layout Parameters (`int64`):** Spatial and sequencing parameters (`track_number`, `duration_ms`).
* **Identification & Metadata Parameters (`object`):** Metadata attributes (`name`, `album`, `id`, `uri`, `release_date`).
---

## 📁 Repository Structure

```text
taylor-swift-spotify-eda/
│
├── EDA_final_project.ipynb # Data Preprocessing, Univariate & Multivariate Notebook
├── taylor_swift_spotify.csv # Raw Spotify Dataset (582 records, 18 columns)
├── EDA Final Project Kerem Bar.pdf # Comprehensive EDA Academic Research Report
├── README.md # Repository Documentation & Findings
├── Figure1.png # Univariate Popularity Distribution & Box Plot
├── Figure2.png # Univariate Danceability Distribution & Box Plot
├── Figure3.png # Univariate Frequency across Engineered Album Families
├── Figure4.jpg # Pearson Correlation Matrix Heatmap
├── Figure5.jpg # Popularity vs. Release Date (Temporal Dynamics)
└── Figure6.png # Popularity Distribution across Album Families Box Plot

```

---

## 🔬 Methodology & Key Analysis Findings

### 1. Data Cleaning & Preprocessing

* **Outlier & Anomaly Isolation:** Isolated 3 non-musical voice memo records from *1989 (Deluxe Edition)* with exact 0 popularity scores.
* **Structural Album Clustering:** Resolved catalog re-recording fragmentation by engineering 12 high-level `album_families` categorical groups and shortening titles (e.g., TTPD, Deluxe, Live) for layout optimization.
* **Temporal Engineering:** Converted raw text release dates into active numerical `release_year` features to enable mathematical correlation and continuous time-series scatter plots.

### 2. Univariate Analysis

* **Popularity Distribution (Figure 1):** Mean = 57.86, Median = 62.00, Mode = 63.00, Skewness = -0.533. Left-skewed distribution driven by voice memo outliers. Upper statistical fence lies at 107.5 (beyond physical 100 limit), proving high-streaming tracks are true catalog behavior rather than statistical outliers.
* **Danceability Distribution (Figure 2):** Approximately symmetric bell-curve (Mean = 0.581, Skewness = -0.265). Upper outliers exposed severe catalog redundancy across expanded album editions.
* **Sample Distribution (Figure 3):** Horizontal count plot revealed group sample imbalance across the 12 album families (ranging from 1989 with 75 tracks to Live with 8 tracks).

### 3. Multivariate Analysis

* **Correlation Analysis (Figure 4):** Strong linear positive association between `popularity` and `release_year` (r = 0.63). Identified severe multicollinearity risk between `energy` and `loudness` (r = 0.79) and strong negative correlation between `loudness` and `acousticness` (r = -0.73).
* **Temporal Dynamics & Re-recordings (Figure 5):** Validated the "Recency Effect" where post-2020 releases sustain elevated popularity (60–80+). Uncovered dramatic upward popularity shifts in modern re-recorded albums ("Taylor's Version") compared to original releases.
* **Era Micro-Anomalies (Figure 6):** Proved global baselines obscure localized behavior. Isolated era-specific outliers:
* **evermore (2020):** *"willow"* (popularity: 77) acts as a positive anomaly in a quiet indie-folk catalog.
* **TTPD (2024):** *"Fortnight"* (popularity: 91) sits above the upper fence, while *"Clara Bow"* (popularity: 67) represents a deep-cut anomaly in a highly streamed era.



---

## 💡 Conclusions & Downstream Predictive Modeling Guidelines

This EDA directly informs future machine learning tasks by establishing explicit data-structuring and modeling requirements:

1. **Mandatory Outlier Filter:** The 3 non-musical voice memo outliers must be removed prior to fitting linear models to prevent severe parameter distortion and artificial variance inflation.
2. **Minimum Category Sample Thresholds:** To address group sample imbalance and high statistical variance in smaller categories (e.g., *Live* family with n = 8), downstream modeling must enforce minimum sample size thresholds per `album_families`.
3. **Model-Specific Multicollinearity Management:** The high linear correlation between `energy` and `loudness` (r = 0.79) poses a multicollinearity risk in linear regression (requiring feature reduction or PCA), whereas both features can safely be retained in tree-based ensemble algorithms.
4. **Localized Era Framework (Preventing Pooling Bias):** `popularity` remains the core target variable. Because temporal progression and localized era characteristics heavily outweigh standalone acoustic features, modeling must be executed dynamically at the `album_families` level to prevent macro-aggregate pooling bias.

---

## 📊 Visualizations Highlights

| Figure 1: Popularity Distribution | Figure 2: Danceability Distribution |
| :---: | :---: |
| ![Figure 1](Figure1.png) | ![Figure 2](Figure2.png) |
| *Histogram & Box Plot isolating voice memo outliers.* | *Distribution curve identifying catalog redundancies.* |

| Figure 3: Album Families Count Plot | Figure 4: Correlation Matrix Heatmap |
| :---: | :---: |
| ![Figure 3](Figure3.png) | ![Figure 4](Figure4.jpg) |
| *Sample frequency across 12 engineered album families.* | *Pearson correlation heatmap identifying feature risk.* |

| Figure 5: Popularity vs. Release Date Dynamics | Figure 6: Popularity by Album Family |
| :---: | :---: |
| ![Figure 5](Figure5.jpg) | ![Figure 6](Figure6.png) |
| *Scatter plot illustrating recency & re-recording impact.* | *Box plot highlighting localized era variance & anomalies.* |
---

## 🛠️ Tech Stack & Methods

* **Language:** Python 3.10+
* **Data Manipulation & Analysis:** Pandas, NumPy
* **Data Visualization:** Matplotlib, Seaborn
* **Statistical Techniques:** Pearson Correlation Analysis, Interquartile Range (IQR) Outlier Fences, Temporal Feature Extraction, Categorical Structural Clustering

---

## 🚀 How to Run

1. Clone the repository:
```bash
git clone [https://github.com/Kerem-Bar/taylor-swift-spotify-eda.git](https://github.com/Kerem-Bar/taylor-swift-spotify-eda.git)

```


2. Install dependencies:
```bash
pip install pandas matplotlib seaborn numpy

```


3. Open and execute the notebook:
```bash
jupyter notebook EDA_final_project.ipynb

```



---

## 👤 Author

**Kerem Bar**

* Master's Student in Information Sciences (Information Technology Specialization)

