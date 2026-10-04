# Comprehensive Customer Churn Analysis (SQL & Python Workflow)

This repository contains an end-to-end data analysis project focused on understanding and predicting customer churn for a subscription-based service. The workflow demonstrates a critical integration of database management (SQLite) and advanced data manipulation and visualization using Python.

## 📊 Objective
The primary goal is to identify key drivers of customer attrition by analyzing the relationship between subscription plans, customer demographics, and service support interactions. The analysis quantifies financial risk and establishes a preliminary risk stratification model.

## 🛠️ Tech Stack
*   **Database Management:** SQLite (via `sqlite3` for Python)
*   **Language:** Python
*   **Libraries:**
    *   **Data Manipulation:** Pandas (heavy focus on merging, transformation, and pivot tables), NumPy (conditional logic, type conversion).
    *   **Visualization:** Matplotlib, Seaborn (Correlation Heatmap, Catplot), Plotly (Interactive setup—*note: the current script mainly uses standard plotting*).

## 📂 Data Workflow (Ingestion & ETL)
This project features a structured ETL pipeline entirely in Python:

1.  **Ingestion:** Programmatically connected to a SQLite database (`customer_churn.db`), queried the master table, and dynamically generated individual Pandas DataFrames for all operational tables (`db_customer`, `db_subscription`, `db_support`).
2.  **Cleaning & Standardization:**
    *   **`db_customer`:** Addressed missing geographical data (Nepal/Kathmandu), standardized `gender` inputs ('Men'/'Women' to 'Male'/'Female'), corrected data types (DOB), and dropped non-essential features (pincode, interests).
    *   **`db_support`:** Corrected complaint data types and removed placeholder columns. Addresssed multi-complaint scenarios by retaining only the *last* interaction point per customer.
3.  **Data Consolidation:** Executed complex, sequential left merges to combine subscription, customer, and support data into a singular, unified analytical dataset.

## ✨ Critical Feature Engineering & Analysis
Beyond basic descriptive statistics, this project engineered critical operational metrics:

*   **KPI Engineering:** Calculated system-wide Churn Rate (mean of target variable), Retention Rate, Average Revenue Per User (ARPU), and Average Complaint Rate.
*   **Tenure Calculation:** Programmatically calculated active customer tenure by benchmarking against `cancellation_date` vs. the current timestamp for active users.
*   **Financial Impact Assessment:** Defined "Revenue at Risk" by quantifying the total monthly charges lost from all churned users.
*   **Risk Stratification Model:** Engineered a custom categorical `churn_risk` feature ('low', 'medium', 'high') derived programmatically from percentile boundaries of existing `churn_score` metrics.
*   **Statistical Correlation Analysis:** Explicitly structured a correlation study, including a correlation coefficient calculation between `escalations` (mapped to binary) and `churn_date`, confirmed via a finalized subset analysis.

## 🚀 Visual Insights & Key Outcomes
*   **Statistical Breakdown (Pivots):** Used pivot tables to provide multi-dimensional aggregation summaries (churn rate, total users, sum of charges) segmented by Plan Type.
*   **Correlation Heatmap:** Engineered numerical codes for ordinal categorical data (Contract Type, Risk, Plan) to create a sophisticated, finalized heatmap visualizing dependencies with the churn target.
*   **Churn Driver (Support):** Analysis confirmed a finalized statistical relationship (Correlation Calculation) between support escalations ('Y' vs 'N') and eventual churn.

## 📁 Repository Structure
*   `customer_churn.db`: Raw SQLite Database file (Required for initial import logic).
*   `churn_analysis.py`: Finalized Python source code.
*   `customer_churn_data_raw.csv`: Programmatically exported consolidated dataset.
