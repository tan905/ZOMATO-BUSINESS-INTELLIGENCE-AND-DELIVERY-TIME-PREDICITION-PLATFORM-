# ZOMATO-BUSINESS-INTELLIGENCE-AND-DELIVERY-TIME-PREDICITION-PLATFORM-
A comprehensive Business Intelligence and machine learning project where an end to end analytics solution for Zomato by cleaning and analyzing operational data using python, SQL and Power BI while developing predictive model to generate actionable business insights.

An end-to-end data engineering, statistical exploratory analysis, machine learning, and 6-page interactive business intelligence project built on multi-table Zomato operational data. The workflow spans raw data ingestion and SQL source-of-truth validation, Python data wrangling and predictive modeling, and interactive Power BI reporting.

---

## 📌 Project Overview

Food delivery platforms generate high-velocity data across orders, customers, restaurants, menu items, delivery partners, payment gateways, promotions, traffic, and weather. This project builds a complete analytical pipeline to answer both descriptive and predictive business questions:
- Which cities, years, and months drive revenue growth and order volume?
- How do customer tenure, repeat ordering, and order patterns relate to retention and churn?
- How do peak hours, traffic levels, and weather conditions impact delivery duration and efficiency?
- Which promotional campaigns lift Average Order Value (AOV) and where do payment failures occur?
- Can we predict **delivery time** and **customer churn** reliably before operational issues escalate?

This project establishes a **single source of truth** and predictive analytics layer to:
- **Standardize KPIs** (`Active Customer`, `Late Order`, `Top Restaurant`) across Operations, Marketing, and Finance.
- **Pinpoint Controllable Delay Drivers** across restaurant prep, partner load, traffic, and rainfall.
- **Proactively Flag Churn Risk** within a 60-day window rather than reacting after customers go inactive.
- **Evaluate Restaurant Quality** via composite performance scores (ratings, cancellations, delivery delays).
  
---

## 🛠️ Tech Stack & Tools

- **Relational Database & SQL Analysis:** MySQL (Staging tables, relational joins, aggregations, and source-of-truth metric validation)
- **Data Manipulation & Numerical Computing:** Python, **Pandas**, **NumPy** (Data cleaning, schema normalization, missing-value handling, and feature engineering)
- **Exploratory Data Analysis & Visualization:** **Matplotlib**, **Seaborn** (Distribution plots, correlation heatmaps, outlier detection, and bivariate/multivariate EDA)
- **Machine Learning:** Scikit-learn / Python ML workflows (**Delivery Time Regression** and **Customer Churn Classification**, feature selection, train/test evaluation, and error analysis)
- **BI & Interactive Reporting:** Power Query (M) & Microsoft Power BI Desktop (Star Schema modeling, DAX measures, and a 6-page executive dashboard)

---

## 🗂️ Data Architecture & End-to-End Pipeline

The dataset connects **12 tables** around a central **`orders` fact table**:
- **Fact Table:** `orders`
- **Dimension & Operational Tables:** `customers`, `restaurants`, `menu`, `order_items`, `payments`, `promotions`, `delivery_partners`, `cities`, `customer_feedback`, `traffic`, `weather`

### 1. MySQL Staging & SQL Analysis
- Loaded raw CSV extracts into structured staging tables with appropriate relational keys and data types.
- Ran SQL queries for record counts, referential integrity checks, revenue and order reconciliations, city/restaurant rankings, and baseline KPI verification.
- Over 20 distinct SQL queries were developed in sql/business_queries.sql covering multi-table joins (INNER, LEFT, RIGHT, SELF, UNION), CASE WHEN bucketing, correlated subqueries, CTEs (WITH), window functions (ROW_NUMBER, RANK, DENSE_RANK, LAG, LEAD), reusable VIEWs, and performance-indexed lookups:
Top 10 revenue-generating restaurants over the trailing 6 months.
City-level average delivery time ranked from slowest to fastest.
Top 10% delivery partners ranked by completed deliveries and customer rating.
Cuisine-wise order cancellation rates and coupon discount ROI analysis.
Customer order recency (days since most recent order) using window functions.   

### 2. Python Data Cleaning & Feature Engineering (`NumPy` & `Pandas`)
- Standardized inconsistent date strings across mixed formats (`YYYY.MM.DD`, `DD/MM/YYYY`, `DD-MM-YYYY`, and `YYYY-MM-DD`) and converted timestamps/numeric fields cleanly.
- Handled missing values, invalid entries, and extreme outliers using `Pandas` and `NumPy`.
- Engineered analytical and modeling features including:
  - `OrderYear` & monthly time attributes
  - `PeakHour` (lunch and dinner rush windows)
  - `WeekendOrder`
  - `CustomerTenure`
  - `DeliveryEfficiency`
- Data Cleaning: Resolved ≥ 95% of logged data anomalies including duplicate exports, inconsistent city names ("Bengaluru" / "Bangalore" / "bangalore "), whitespace padding, mixed date formats (DD-MM-YYYY, MM/DD/YYYY, YYYY.MM.DD), malformed phone numbers/pincodes, negative financial/duration values, IQR/z-score outliers, and orphaned foreign keys.

### 3. Exploratory Data Analysis (`Matplotlib` & `Seaborn`)
- Analyzed revenue distributions, seasonal trends, order value spread, and delivery time variance across cities, traffic tiers, and weather conditions.
- Built correlation matrices, box/violin plots, and count/bar visuals to inspect relationships between delivery speed, discounts, payment status, and customer ratings.
- Conducted comprehensive univariate, bivariate, and multivariate analysis across 30+ visualizations (15+ Matplotlib charts and 15+ Seaborn statistical plots)
- Revenue & Seasonality: Bar, line, stacked bar, and cumulative area charts tracking city-level growth, cuisine share, and monthly order trends.
- Operational Bottlenecks: Violin plots, box plots, scatter plots, and regression plots evaluating DeliveryTimeMinutes across vehicle types, city tiers, peak hours, TrafficLevel, and Rainfall.
- Customer & Payment Behavior: Correlation heatmaps, pairplots, KDE distributions, and countplots comparing repeat vs. one-time buyers, membership tier basket sizes, and payment method shares.   

### 4. Machine Learning Models
- **Delivery Time Regression:**
  `Predictors`: TrafficScore, RainImpact, PeakHour, WeekendOrder, Haversine restaurant-to-customer distance (Latitude/Longitude), DeliveryEfficiency, and basket size.   Algorithms Compared: Linear Regression, Decision Tree Regressor, Random Forest Regressor, Gradient Boosting Regressor, and XGBoost.
  `Validation & Tuning`: 80/20 train-test split, k-fold cross-validation, and GridSearchCV / RandomizedSearchCV hyperparameter optimization.   Evaluation Targets & Metrics: Evaluated via MAE, MSE, RMSE ($\le 6\text{ mins}$ target), and $R^2$ ($\ge 0.75$ target) alongside residual diagnostics and tree-based feature importance.
    
- **Customer Churn Classification:** Identifies customers at risk of churning using ordering behavior, tenure, spend/order frequency, and service experience features; evaluated using classification metrics such as Precision, Recall, F1-score, and ROC-AUC.
  `Algorithms Compared`: Logistic Regression, Decision Tree, Random Forest, and Gradient Boosting Classifiers.
  `Imbalance & Evaluation`: Explicit class imbalance handling (class weighting / resampling) evaluated via Accuracy, Precision, Recall, F1-score ($\ge 0.70$ target), ROC-AUC curve, and Confusion Matrix, surfacing the top 10 churn risk drivers.

  
### 5. Power BI Star Schema & 6-Page Dashboard
- Modeled `orders` as the central fact table linked to dimension/lookup tables with clean relationships and DAX measures (`Total Customers`, `Repeat Customer Rate %`, `Avg Orders per Customer`, `Avg Delivery Time`, `On-Time Delivery %`, `Promo Spend`, `Payment Success Rate %`, `Avg Order Value`, `Negative Review Rate %`).
- **Page 1 — Executive Summary:** Year-wise revenue bar chart, monthly revenue trend line chart, city breakdown, and core KPIs.
- **Page 2 — Customer Analytics:** Customer counts, repeat customer rate, average orders per customer, city customer distribution, and Top 10 high-value customers table.
- **Page 3 — Delivery & Operations:** Average delivery time, on-time delivery rate, active partners, city/peak-hour delivery performance, and partner leaderboard.
- **Page 4 — Payments & Promotions:** Payment method mix (donut chart), Promo Orders vs. AOV (combo chart), and Payment Failure Rate by method (stacked bar chart).
- **Page 5 — Restaurant & Menu Performance:** Active restaurants, items sold, average rating, cuisine treemap, Top 10 menu items, and top restaurants table.
- **Page 6 — Customer Feedback & Experience:** Average rating, review count, negative review rate (1–2 stars), rating distribution, delivery time vs. rating combo chart, and low-rated order audit table.

---

## 🖼️ Dashboard Preview

<table>
  <tr>
    <td width="50%" align="center">
      <b>Page 1: Executive Summary</b><br/>
      <img src="assets/page1_executive.png" alt="Page 1: Executive Summary" width="100%"/>
      <img width="1366" height="768" alt="Screenshot (101)" src="https://github.com/user-attachments/assets/6311cc5b-3a2e-400e-8aa4-733ec4e6409f" />
    </td>
    <td width="50%" align="center">
      <b>Page 2: Customer Analytics</b><br/>
      <img src="assets/page2_customer.png" alt="Page 2: Customer Analytics" width="100%"/>
      <img width="1366" height="768" alt="Screenshot (102)" src="https://github.com/user-attachments/assets/cfda56e2-401e-428c-83bd-b254a9d10602" />

  </td>
  </tr>
  <tr>
    <td width="50%" align="center">
      <b>Page 3: Delivery & Operations</b><br/>
      <img src="assets/page3_delivery.png" alt="Page 3: Delivery & Operations" width="100%"/>
      <img width="1366" height="768" alt="Screenshot (103)" src="https://github.com/user-attachments/assets/ae82bda9-f933-4405-b791-b50cda620f18" />
    </td>
    <td width="50%" align="center">
      <b>Page 4: Payments & Promotions</b><br/>
      <img src="assets/page4_payments.png" alt="Page 4: Payments & Promotions" width="100%"/>
      <img width="1366" height="768" alt="Screenshot (104)" src="https://github.com/user-attachments/assets/4b87eee3-04a3-4276-a345-bdbb721b9fcc" />
    </td>
  </tr>
  <tr>
    <td width="50%" align="center">
      <b>Page 5: Restaurant & Menu</b><br/>
      <img src="assets/page5_restaurant.png" alt="Page 5: Restaurant & Menu" width="100%"/>
      <img width="1366" height="768" alt="Screenshot (105)" src="https://github.com/user-attachments/assets/575f85b0-3330-4528-b8ed-f9b2c9ad7864" />
    </td>
    <td width="50%" align="center">
      <b>Page 6: Customer Feedback</b><br/>
      <img src="assets/page6_feedback.png" alt="Page 6: Customer Feedback" width="100%"/>
      <img width="1366" height="768" alt="Screenshot (106)" src="https://github.com/user-attachments/assets/e37a5c67-94a6-4d86-ae35-ccb396886827" />
    </td>
  </tr>
</table>

---
## PROJECT STRUCTURE 
Zomato_Business_Intelligence_Project/
├── data/
│   ├── raw/
│   └── cleaned/
├── sql/
│   ├── schema.sql
│   └── business_queries.sql
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_delivery_time_model.ipynb
│   └── 05_churn_model.ipynb
├── src/
│   ├── ingest.py
│   ├── clean.py
│   ├── features.py
│   ├── model_delivery.py
│   └── model_churn.py
├── models/
│   ├── delivery_time_best_model.pkl
│   └── churn_best_model.pkl
├── reports/
│   ├── eda_report.pdf
│   └── business_insights_report.pdf
├── powerbi/
│   └── zomato_dashboard.pbix
├── documentation/
│   └── prd.docx
├── README.md

## Future Improvements
Real-Time Inference API: Expose the trained delivery time regression and churn classification models via a FastAPI / Flask REST endpoint for live order ETA updates[cite: 1].

Automated Orchestration: Schedule daily ETL and model retraining pipelines using Apache Airflow or Prefect.

Geospatial Routing Integration: Incorporate live road-network travel distances and dynamic surge-pricing features to further reduce delivery time RMSE.

A/B Testing Framework: Measure real-world retention lift from targeted coupons dispatched to high-churn-probability customer cohorts[cite: 1].
