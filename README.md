# 🏠 Real Estate Management — Detailed Analysis

> A comprehensive Power BI analytics report combining descriptive statistics, outlier detection, feature correlation, and machine learning price prediction for residential real estate data.

---

## 📊 Live Dashboard

🔗 [View Interactive Dashboard on Power BI Service](#) ← *Replace with your published link*

---

## 📁 Project Overview

| Detail | Info |
|---|---|
| **Tool** | Microsoft Power BI Desktop |
| **Data Source** | Excel / CSV |
| **Domain** | Real Estate & Property Analytics |
| **Target Roles** | BI Developer · Data Analyst |
| **Report Pages** | 8 |
| **Custom Visuals** | Histogram, Box & Whisker, Heatmap by Powerviz, Inforiver Analytics+ |
| **Python Integration** | Correlation Matrix, Multicollinearity Analysis, Price Prediction Model |

---

## 🎯 Business Problem

A real estate firm needed a data-driven solution to:
- Understand the distribution and statistical profile of housing prices and property features
- Detect pricing and area outliers that skew market analysis
- Identify which property features (bedrooms, bathrooms, furnishing, location) drive the highest prices
- Measure correlations and multicollinearity between features to support sound modeling
- Build and evaluate a **price prediction model** to estimate property values from features

---

## 📐 Data Model

Built on a single fact table with supporting measure tables:

**Fact Table**
- `Housing` — property records including price, area, bedrooms, bathrooms, stories, parking, and binary feature flags (basement, guestroom, mainroad, preferred area, air conditioning, hot water heating, furnishing status)

**Computed Columns in Housing Table**
- `Area_Bins` — bucketed area ranges for frequency distribution
- `Price_Bins` — bucketed price ranges for frequency distribution
- `Area_Is_Outlier` — flag for area outliers
- `Price_Is_Outlier` — flag for price outliers
- `Predicted_Price` — model output from Python regression
- `Price_Difference` — residual between actual and predicted price
- Boolean-coded columns (`basement_bool`, `mainroad_bool`, `prefarea_bool`, `guestroom_bool`, `hotwaterheating_bool`, `airconditioning_bool`, `furnishingcoded`)

**Supporting Tables**
- `MeasureTable` — centralized DAX measures
- `MeauseTable` — descriptive statistics measures (Count, Distinct, Min, Max, Median, Average, Std Dev, Missing)
- `SummaryColumns` — column reference table for the statistics pivot

---

## 🧮 DAX Measures

| Measure | Description |
|---|---|
| `Average_price` | Mean property price |
| `Avg_price` | Average price for combo charts |
| `Max_price` | Maximum listed property price |
| `Min_price` | Minimum listed property price |
| `AC Premium` | Price premium for air-conditioned properties |
| `Main Road Premium` | Price premium for main road-facing properties |
| `Price_Frequency` | Count of properties per price bin |
| `Area_Frequency` | Count of properties per area bin |
| `Bedroom_Frequency` | Count of properties per bedroom count |
| `Outlier_Count` | Total price outliers detected |
| `Area_Outlier_Count` | Total area outliers detected |
| `MAE` | Mean Absolute Error of prediction model |
| `RMSE` | Root Mean Squared Error of prediction model |
| `Max_Residual` | Maximum prediction error |
| `Average` / `Count` / `Distinct` / `Min` / `Max` / `Median` / `Standard Deviation` / `Missing` | Full descriptive statistics suite |

---

## 📋 Report Pages

### 1. 🗂️ Summary Statistics
![Summary Statistics](screenshots/slide_1.png)

High-level statistical overview of the housing dataset:
- Descriptive statistics pivot (Count, Distinct, Min, Max, Median, Mean, Std Dev, Missing) for all features
- KPI cards: **Total Properties**, **Average Price**, **Maximum Price**, **Minimum Price**
- Basement & Guestroom availability (donut charts)
- Properties on main road vs. not (bar chart)
- Properties in preferred area vs. not (bar chart)
- Slicers: Price range, Furnishing status, Parking, Air Conditioning, Hot Water Heating

---

### 2. 📊 Frequency Distribution
![Frequency Distribution](screenshots/slide_2.png)

Distribution analysis across key numeric features:
- **Price** frequency distribution (histogram)
- **Area** frequency distribution (histogram)
- **Number of Stories** frequency distribution (clustered column chart)
- **Bedrooms** frequency distribution (column chart)
- Slicers for dynamic filtering across all charts

---

### 3. 🔍 Outlier Detection
![Outlier Detection](screenshots/slide_3.png)

Statistical outlier identification using scatter plots:
- **Price Outlier Detection** — scatter chart flagging price outliers
- **Area Outlier Detection** — scatter chart flagging area outliers
- KPI cards: **Total Outliers in Price**, **Total Outliers in Area**
- Slicers for drilling into outlier subsets by furnishing, parking, AC, and heating

---

### 4. 💰 Price Analysis by Features
![Price Analysis by Features](screenshots/slide_4.png)

Feature-by-feature price impact analysis:
- Average price by **Bedrooms** and **Main Road** presence (clustered column)
- Average price by **Bathrooms** and **Preferred Area** (clustered column)
- Average price by **Stories** (funnel chart)
- Average price by **Parking** spaces (funnel chart)
- Average price by **Furnishing Status** (funnel chart)
- KPI cards: **AC Premium**, **Main Road Premium**
- Slicers: Basement, Guestroom, Preferred Area, Main Road, Stories

---

### 5. 📉 Correlation of Price with Other Features
![Correlation Analysis](screenshots/slide_5.png)

Bivariate analysis between price and property characteristics:
- **Correlation Matrix** (Python visual) — price vs. all numeric and binary features
- Average house price by **Area** (combo chart)
- Average house price by **Bathrooms** (combo chart)
- Slicers for filtering by furnishing, parking, AC, and heating

---

### 6. 🔗 Feature Correlation & Multicollinearity
![Feature Correlation & Multicollinearity](screenshots/slide_6.png)

Advanced statistical analysis of inter-feature relationships:
- **Heatmap by Powerviz** — full feature-to-feature correlation matrix
- **Python visual** — multicollinearity detection (VIF analysis or pairplot)
- Slicers for subsetting the correlation analysis

---

### 7. 🤖 Price Prediction Model
![Price Prediction Model](screenshots/slide_7.png)

Machine learning regression model built with Python integration:
- **Python visual** — regression model (Linear Regression / Random Forest) trained on housing features
- Coefficients and feature importance displayed
- Model summary including key predictors
- Slicers for filtering training data subsets

---

### 8. 📈 Predictive Model Insights
![Predictive Model Insights](screenshots/slide_8.png)

Model evaluation and residual analysis:
- **Actual vs. Predicted Price by Furnishing Status** (scatter chart)
- **Actual vs. Predicted Price by Area** (scatter chart)
- **Actual vs. Predicted Price by Bedrooms** (scatter chart)
- KPI cards: **MAE**, **RMSE**, **Maximum Error**
- Slicers for exploring prediction accuracy by property subset

---

## ⚙️ Power Query Transformations

- Loaded and cleaned raw housing CSV data
- Encoded categorical columns to boolean (`basement_bool`, `mainroad_bool`, `prefarea_bool`, etc.)
- Created `furnishingcoded` numeric encoding for furnishing status
- Built `Price_Bins` and `Area_Bins` for frequency distribution visuals
- Computed outlier flags (`Price_Is_Outlier`, `Area_Is_Outlier`) using IQR or Z-score logic
- Integrated Python script outputs (`Predicted_Price`, `Price_Difference`) back into the data model

---

## 🔑 Key Insights

- Properties on the **main road** and in **preferred areas** command significant price premiums
- **Air conditioning** and **hot water heating** are among the strongest price-driving amenities
- Outlier detection identified a small cluster of high-area properties with disproportionately high prices
- **Bathroom count** shows a stronger correlation with price than bedroom count
- The predictive model (MAE and RMSE measured on the Insights page) demonstrates reliable price estimation from property features
- **Furnished properties** cluster at the upper price range across all story counts

---

## 🚀 How to View

**Option 1 — Live (Recommended):**
Click the Power BI Service link above to interact with the live dashboard.

**Option 2 — Download & Open Locally:**
1. Download `Real_Estate_Management-Detailed_Analysis.pbix`
2. Open with [Power BI Desktop](https://powerbi.microsoft.com/desktop) (free)
3. Note: Python visuals require a local Python environment with `pandas`, `scikit-learn`, `matplotlib`, and `seaborn` installed

---

## 🛠️ Tools & Technologies

- **Power BI Desktop** — report authoring and data modeling
- **Power Query (M)** — data cleaning, encoding, and feature engineering
- **DAX** — 15+ measures including descriptive statistics, price premiums, and model evaluation metrics
- **Python** — correlation matrix, multicollinearity (VIF), and price prediction model integrated via Power BI Python visuals
- **Custom Visuals** — Histogram Chart, Box and Whisker by MAQ Software, Heatmap by Powerviz, Inforiver Analytics+
- **Excel / CSV** — data source
- **Power BI Service** — cloud publishing and sharing

---

## 👤 Author

**Simran Kaur**
📧 skaurprofessional@gmail.com
🔗 [LinkedIn Profile](#)
🐙 [GitHub Profile](#)

---

*Feel free to fork this project, explore the data model, or reach out with any questions!*
