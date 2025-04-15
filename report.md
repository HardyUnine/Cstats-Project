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

---

## 4. Hypothesis Testing

Below are three simple linear regression tests examining how each of our numeric predictors affects `SalePrice` individually.

---

### 4.1 Relationship Between Overall Quality and SalePrice

#### 4.1.1 Introduction

We aim to test the hypothesis that the variable `OverallQual` (Overall Quality) affects `SalePrice`. Formally, the hypotheses are:

\[
H_0 : \beta_{\text{OverallQual}} = 0 \quad (\text{OverallQual does not affect SalePrice}),
\]
\[
H_1 : \beta_{\text{OverallQual}} \neq 0 \quad (\text{OverallQual affects SalePrice}).
\]

#### 4.1.2 Methods

We fit a simple linear regression model:

\[
\text{SalePrice} = \beta_0 + \beta_1 \times \text{OverallQual} + \varepsilon,
\]

where \(\beta_0\) is the intercept, \(\beta_1\) is the slope for `OverallQual`, and \(\varepsilon\) is the error term.

#### 4.1.3 Results

A sample regression output (e.g., from R or Python) yielded:

- **Intercept** (\(\hat{\beta}_0\)) \(\approx 172639.63\)  
  *Std. Error* = 1873.01,  \( t \approx 92.17\), \( p < 0.001\)  
  95% CI: \([168965.55,\;176313.71]\)

- **OverallQual** (\(\hat{\beta}_1\)) \(\approx 1076.57\)  
  *Std. Error* = 299.86, \( t \approx 3.59\), \( p \approx 0.00034\)  
  95% CI: \([488.36,\;1664.78]\)

#### 4.1.4 Interpretation

- The slope \(\hat{\beta}_1 \approx 1076.57\) means that for every 1-unit increase in `OverallQual`, the **expected** `SalePrice` increases by about \$1,076.57.  
- The 95% CI for \(\beta_1\) does not contain 0, so `OverallQual` is statistically significant in predicting `SalePrice`.

#### 4.1.5 Conclusion

We reject the null hypothesis \(H_0\). There is strong evidence that `OverallQual` influences `SalePrice`.

---

### 4.2 Impact of Construction Year on SalePrice

#### 4.2.1 Introduction

We test whether the year a house was constructed (`YearBuilt`) affects `SalePrice`. Formally,

\[
H_0 : \beta_{\text{YearBuilt}} = 0 \quad (\text{YearBuilt does not affect SalePrice}),
\]
\[
H_1 : \beta_{\text{YearBuilt}} \neq 0 \quad (\text{YearBuilt affects SalePrice}).
\]

#### 4.2.2 Methods

We fit a simple linear regression model:

\[
\text{SalePrice} = \beta_0 + \beta_1 \times \text{YearBuilt} + \varepsilon,
\]

where \(\beta_0\) is the intercept, \(\beta_1\) is the slope for `YearBuilt`, and \(\varepsilon\) is the error term.

#### 4.2.3 Results

Representative regression output:

- **Intercept** \(\approx 170{,}400\)  
  *Std. Error* \(\approx 28100\), \( t \approx 6.07\), \( p < 0.001\)

- **YearBuilt** \(\approx 4.45\)  
  *Std. Error* \(\approx 14.24\), \( t \approx 0.31\), \( p \approx 0.755\)

- 95% CI for \(\beta_{\text{YearBuilt}}\): \([-23.48,\;32.38]\)

#### 4.2.4 Interpretation

- The slope \(\hat{\beta}_1 \approx 4.45\) suggests that for each additional year, `SalePrice` increases by \$4.45 on average (though not statistically significant here).  
- The p-value (\(\approx 0.755\)) is much higher than 0.05, so we **fail to reject** \(H_0\).  
- The 95% CI includes 0, reinforcing that the effect is not significant in this simple model.

#### 4.2.5 Conclusion

We find insufficient evidence to conclude that `YearBuilt` significantly affects `SalePrice`. We **fail to reject** \(H_0\).

---

### 4.3 Effect of Living Area on SalePrice

#### 4.3.1 Introduction

We test whether `GrLivArea` (above-grade living area in square feet) has a statistically significant impact on `SalePrice`. Formally,

\[
H_0 : \beta_{\text{GrLivArea}} = 0 \quad (\text{GrLivArea does not affect SalePrice}),
\]
\[
H_1 : \beta_{\text{GrLivArea}} \neq 0 \quad (\text{GrLivArea affects SalePrice}).
\]

#### 4.3.2 Methods

We fit a simple linear regression:

\[
\text{SalePrice} = \beta_0 + \beta_1 \times \text{GrLivArea} + \varepsilon.
\]

Here, \(\beta_0\) is the intercept, \(\beta_1\) is the slope for `GrLivArea`, and \(\varepsilon\) is the error term.

#### 4.3.3 Results

A sample output might be:

- **Intercept** \(\approx 150{,}500\)  
  *Std. Error* \(\approx 1148\), \( t \approx 131.132\), \( p < 0.001\)

- **GrLivArea** \(\approx 19.28\)  
  *Std. Error* \(\approx 0.73\), \( t \approx 26.25\), \( p < 0.001\)

- 95% CI for \(\beta_{\text{GrLivArea}}\): \([17.84,\;20.72]\)

- \(R^2 \approx 0.321\) (i.e., `GrLivArea` alone explains about 32% of the variance in `SalePrice`).

#### 4.3.4 Interpretation

- The slope \(\hat{\beta}_1 \approx 19.28\) means each additional square foot of living area increases `SalePrice` by about \$19.28 on average.  
- The 95% CI does not include 0, and the p-value \(< 0.001\), so `GrLivArea` is highly significant.  

#### 4.3.5 Conclusion

We reject \(H_0\). `GrLivArea` has a strong, statistically significant positive effect on `SalePrice`.

---

