# 📊 Ads Performance Optimization & Budget Allocation using Marketing Mix Modeling

This project implements **Marketing Mix Modeling (MMM)** using Python to evaluate the impact of various marketing channels on revenue. It enables data-driven budget allocation decisions, ROI measurement, and "What-If" scenario simulations for better marketing efficiency and strategic planning.

In addition to predictive modeling, **interactive Tableau dashboards** were developed to visualize marketing performance, channel efficiency, and regional trends, enabling business stakeholders to interpret model insights through intuitive analytics reporting.

---

## 🚀 Project Overview

Marketing Mix Modeling (MMM) is a regression-based technique that helps businesses quantify the impact of marketing activities on performance metrics such as revenue. This project builds a baseline MMM using Linear Regression and offers simulation capabilities to optimize marketing budgets.

To complement model outputs, Tableau dashboards translate analytical results into executive-ready visual insights for marketing performance monitoring and decision-making.

---

## 📁 Project Structure

- `MMM_Modeling.ipynb` – Full notebook with data cleaning, feature engineering, modeling, evaluation, and simulation
- `mmm_app.py` – Flask API to serve the trained model
- `linear_model.pkl` – Trained Linear Regression model
- `model_features.json` – Feature list used during model training
- `mmm_tableau_dataset.csv` – Analytics-ready dataset prepared for Tableau dashboards
- `Ads Performance Optimization Dashboard.twbx` – Tableau dashboard workbook
- `README.md` – Project documentation

---

## 🧠 Objectives

- Understand how different marketing channels impact revenue
- Calculate marketing Return on Investment (ROI)
- Simulate budget changes (e.g., "What if we increase YouTube ads by 20%?")
- Build an API for revenue prediction based on marketing input data
- Visualize marketing performance and efficiency using Tableau dashboards

---

## 🔍 Data Overview

- Multi-region ecommerce dataset with 132,759 rows and 50 columns
- Includes time series data across paid channels (Google, Meta, TikTok), engagement signals (clicks, impressions), and purchase data

---

## 🧼 Data Cleaning and Preparation

- Dropped channels with excessive missing data: TikTok, Google Video, Google Display, Meta Other
- Filled missing values in key spend and click columns with `0`
- Removed non-critical metadata columns such as verticals and sub-verticals
- Converted `DATE_DAY` to datetime format

---

## 🛠️ Feature Engineering

### Revenue Calculation
```
revenue = ALL_PURCHASES_ORIGINAL_PRICE - ALL_PURCHASES_GROSS_DISCOUNT
```

### Total Marketing Spend
```
total_spend = sum of all relevant ad spend columns
```

### ROI Calculation
```
roi = revenue / (total_spend + 1)
```

### Time Features Extracted
- `year`
- `month`
- `week`
- `day_of_week`

---

## 🎯 Model Setup

### Target Variable
- `revenue`

### Input Features
- `GOOGLE_PAID_SEARCH_SPEND`
- `GOOGLE_SHOPPING_SPEND`
- `GOOGLE_PMAX_SPEND`
- `META_FACEBOOK_SPEND`
- `META_INSTAGRAM_SPEND`
- `EMAIL_CLICKS`
- `ORGANIC_SEARCH_CLICKS`
- `DIRECT_CLICKS`
- `BRANDED_SEARCH_CLICKS`
- `year`
- `month`
- `day_of_week`

---

## 🧪 Train-Test Split

- Time-based split using cutoff date: `2023-12-31`
- Train set includes all data before 2024
- Test set includes data from 2024 onwards

---

## 🤖 Model Training

- Model: **Linear Regression** (via `scikit-learn`)
- Trained on pre-2024 data

---

## 📈 Model Evaluation

- **R² Score**: `0.789`
- **RMSE**: `246,748,035,379.62`
- Strong baseline performance for linear MMM

---

## 🔍 Feature Importance (Coefficients)

| Feature | Coefficient |
|---|---|
| `year` | +19,603.65 |
| `month` | +2,600.52 |
| `GOOGLE_PAID_SEARCH_SPEND` | +86.76 |
| `EMAIL_CLICKS` | +80.48 |
| `GOOGLE_SHOPPING_SPEND` | +46.87 |
| `META_INSTAGRAM_SPEND` | +14.36 |
| `META_FACEBOOK_SPEND` | +7.99 |
| `BRANDED_SEARCH_CLICKS` | +5.15 |
| `DIRECT_CLICKS` | -19.45 |
| `GOOGLE_PMAX_SPEND` | -23.38 |
| `day_of_week` | -1,347.36 |

---

## 🔄 ROI Analysis

ROI is calculated to evaluate marketing efficiency:

```
roi = revenue / (total_spend + 1)
```

Allows clear comparison of which channels drive the most revenue per unit spend.

---

## 📊 Tableau Dashboard Analytics

Interactive Tableau dashboards were created to complement the MMM model and provide business-friendly visualization of marketing performance.

### Dashboard Insights

- **Marketing Spend vs Purchases Trend**
  - Tracks how advertising investment translates into purchase growth over time.

- **Channel Performance Analysis**
  - Compares Google, Meta, and TikTok ecosystems to identify high-efficiency channels.

- **Marketing Efficiency Metrics**
  - Conversion rate, cost per purchase, and purchases per dollar spent enable ROI comparison.

- **Regional Performance Monitoring**
  - Territory-level analysis highlights regions with strong or weak marketing efficiency.

These dashboards simulate real-world marketing analytics reporting used by growth and performance marketing teams.

---

## 💡 What-If Simulation

### Scenario: Increase Google Paid Search Spend by 30%
```
scenario = X_test.copy()
scenario['GOOGLE_PAID_SEARCH_SPEND'] *= 1.3
```

### Result
```
Simulated change in revenue: +4.60%
```

---

## 🎯 Goal: Marketing Budget Optimization

This project enables marketers to:

- Simulate budget reallocations
- Identify top-performing channels
- Make data-backed investment decisions
- Predict ROI outcomes for future planning

---

## 🌐 Flask API

A lightweight API built with Flask to serve the trained model.

### Endpoints

#### `GET /`
Returns:
```
"MMM Model is running!"
```

#### `POST /predict`
Accepts JSON input and returns predicted revenue.

---

## ⚠️ Notes

- You may see a `scikit-learn` version warning. This is safe.
- Flask app is for development only; use Gunicorn/Docker for production.

---

## 🧰 Tech Stack

- Python 3.8+
- pandas, numpy, seaborn, matplotlib
- scikit-learn
- Flask
- Tableau (Business Intelligence Dashboards)
- joblib, json

---

## 🔮 Future Improvements

- Add regularized models (Ridge, Lasso, ElasticNet)
- Implement carryover and saturation effects
- Build optimization layer for automated budget allocation
- Deploy using Docker, Heroku, or Render
- Extend dashboards with real-time analytics integration
