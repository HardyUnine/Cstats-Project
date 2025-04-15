# House Prices Project Report

## 1. Abstract

In this project, we aim to predict house prices using the [Ames Housing dataset](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data). Initially, we focus on three numerical variables—**Overall Quality (`OverallQual`)**, **Construction Year (`YearBuilt`)**, and **Living Area (`GrLivArea`)**—to explore basic relationships with `SalePrice`. Later, we plan to incorporate additional categorical features (e.g., **Neighborhood**, **ExterQual**, **KitchenQual**) using dummy encoding or ANOVA to capture their influence on house prices.  

Our approach applies classical statistical inference for exploratory analysis, followed by a regression model. Future steps involve extending the model to include categorical variables and performing more advanced statistical methods (ANOVA, time series, etc.).

---

## 2. Introduction

### 2.1 Objective

The goal of this project is to get hands-on experience applying statistical techniques to a real-world dataset. Specifically, we:

- Explore the distribution and basic statistics of the `SalePrice` variable.
- Investigate correlations between `SalePrice` and selected numerical features.
- Plan to incorporate additional categorical features for improved predictive power.
- May extend to advanced methods like ANOVA, time series, or other modeling techniques.

### 2.2 Dataset

The Ames Housing dataset includes extensive details about house sales, such as size, quality, neighborhood, and various design features. The dataset was downloaded from [Kaggle](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data). It contains:

- `train.csv`: Features + `SalePrice` for 1,460 houses.
- `test.csv`: Features for 1,459 houses (no `SalePrice` column).

---

## 3. Methods

### 3.1 Data Loading & Preprocessing

1. **Loading the Data**  
   - We used `pandas.read_csv()` to load both `train.csv` and `test.csv`.
   
2. **Handling Missing Values**  
   - We checked numerical features for missing values and found that our three features of interest—`OverallQual`, `YearBuilt`, and `GrLivArea`—had no missing values.  
   - For initial modeling, we focus on these three numeric features, since they are complete.

3. **Selecting Numeric Features for Preliminary Analysis**  
   - **OverallQual**: An ordinal variable from 1–10 indicating the overall material and finish of the house.  
   - **YearBuilt**: The original construction date of the house.  
   - **GrLivArea**: Above grade (ground) living area in square feet.  
   - **SalePrice**: Our target variable.

4. **(Planned) Categorical Features**  
   - **Neighborhood**: A categorical feature with multiple distinct neighborhoods.  
   - **ExterQual**: A categorical feature for external quality.  
   - **KitchenQual**: A categorical feature for kitchen quality.  

   In future steps, we plan to implement these categorical variables—possibly via dummy encoding or ANOVA—to evaluate their impact on `SalePrice`.

---

### 3.2 Classical Statistical Inference

Before building models, we computed basic statistics for `SalePrice`:

- **Mean, Median, Standard Deviation** of `SalePrice`.
- **Confidence Interval** for the mean sale price using a t-distribution approach.
- **Correlation** between `SalePrice` and the three chosen numeric variables (`OverallQual`, `YearBuilt`, `GrLivArea`).

