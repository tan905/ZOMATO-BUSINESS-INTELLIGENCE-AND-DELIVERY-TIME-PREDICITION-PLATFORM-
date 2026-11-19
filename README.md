# ZOMATO-BUSINESS-INTELLIGENCE-AND-DELIVERY-TIME-PREDICITION-PLATFORM-
A comprehensive Business Intelligence and machine learning project where an end to end analytics solution for Zomato by cleaning and analyzing operational data using python, SQL and Power BI while developing predictive model to generate actionable business insights.
<img width="1366" height="768" alt="Screenshot (106)" src="https://github.com/user-attachments/assets/e37a5c67-94a6-4d86-ae35-ccb396886827" />
<img width="1366" height="768" alt="Screenshot (105)" src="https://github.com/user-attachments/assets/575f85b0-3330-4528-b8ed-f9b2c9ad7864" />
<img width="1366" height="768" alt="Screenshot (104)" src="https://github.com/user-attachments/assets/4b87eee3-04a3-4276-a345-bdbb721b9fcc" />
<img width="1366" height="768" alt="Screenshot (103)" src="https://github.com/user-attachments/assets/ae82bda9-f933-4405-b791-b50cda620f18" />
<img width="1366" height="768" alt="Screenshot (102)" src="https://github.com/user-attachments/assets/cfda56e2-401e-428c-83bd-b254a9d10602" />
<img width="1366" height="768" alt="Screenshot (101)" src="https://github.com/user-attachments/assets/6311cc5b-3a2e-400e-8aa4-733ec4e6409f" />

An end-to-end data engineering, statistical exploratory analysis, machine learning, and 6-page interactive business intelligence project built on multi-table Zomato operational data. The workflow spans raw data ingestion and SQL source-of-truth validation, Python data wrangling and predictive modeling, and interactive Power BI reporting.

---

## 📌 Project Overview

Food delivery platforms generate high-velocity data across orders, customers, restaurants, menu items, delivery partners, payment gateways, promotions, traffic, and weather. This project builds a complete analytical pipeline to answer both descriptive and predictive business questions:
- Which cities, years, and months drive revenue growth and order volume?
- How do customer tenure, repeat ordering, and order patterns relate to retention and churn?
- How do peak hours, traffic levels, and weather conditions impact delivery duration and efficiency?
- Which promotional campaigns lift Average Order Value (AOV) and where do payment failures occur?
- Can we predict **delivery time** and **customer churn** reliably before operational issues escalate?

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

### 2. Python Data Cleaning & Feature Engineering (`NumPy` & `Pandas`)
- Standardized inconsistent date strings across mixed formats (`YYYY.MM.DD`, `DD/MM/YYYY`, `DD-MM-YYYY`, and `YYYY-MM-DD`) and converted timestamps/numeric fields cleanly.
- Handled missing values, invalid entries, and extreme outliers using `Pandas` and `NumPy`.
- Engineered analytical and modeling features including:
  - `OrderYear` & monthly time attributes
  - `PeakHour` (lunch and dinner rush windows)
  - `WeekendOrder`
  - `CustomerTenure`
  - `DeliveryEfficiency`

### 3. Exploratory Data Analysis (`Matplotlib` & `Seaborn`)
- Analyzed revenue distributions, seasonal trends, order value spread, and delivery time variance across cities, traffic tiers, and weather conditions.
- Built correlation matrices, box/violin plots, and count/bar visuals to inspect relationships between delivery speed, discounts, payment status, and customer ratings.

### 4. Machine Learning Models
- **Delivery Time Regression:** Predicts expected delivery duration from order context, logistics/operational features, traffic/weather signals, and engineered time features; evaluated using regression metrics such as MAE, RMSE, and $R^2$.
- **Customer Churn Classification:** Identifies customers at risk of churning using ordering behavior, tenure, spend/order frequency, and service experience features; evaluated using classification metrics such as Precision, Recall, F1-score, and ROC-AUC.

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
    </td>
    <td width="50%" align="center">
      <b>Page 2: Customer Analytics</b><br/>
      <img src="assets/page2_customer.png" alt="Page 2: Customer Analytics" width="100%"/>
    </td>
  </tr>
  <tr>
    <td width="50%" align="center">
      <b>Page 3: Delivery & Operations</b><br/>
      <img src="assets/page3_delivery.png" alt="Page 3: Delivery & Operations" width="100%"/>
    </td>
    <td width="50%" align="center">
      <b>Page 4: Payments & Promotions</b><br/>
      <img src="assets/page4_payments.png" alt="Page 4: Payments & Promotions" width="100%"/>
    </td>
  </tr>
  <tr>
    <td width="50%" align="center">
      <b>Page 5: Restaurant & Menu</b><br/>
      <img src="assets/page5_restaurant.png" alt="Page 5: Restaurant & Menu" width="100%"/>
    </td>
    <td width="50%" align="center">
      <b>Page 6: Customer Feedback</b><br/>
      <img src="assets/page6_feedback.png" alt="Page 6: Customer Feedback" width="100%"/>
    </td>
  </tr>
</table>

---

## 📐 Sample SQL, Python & DAX Snippets

### SQL Validation (City Revenue & Order Volume)
```sql
SELECT
    c.City,
    COUNT(o.OrderID) AS total_orders,
    SUM(o.TotalAmount) AS total_revenue
FROM orders o
JOIN cities c ON o.CityID = c.CityID
GROUP BY c.City
ORDER BY total_revenue DESC;

