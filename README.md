# Loan-Performance-Risk-assessment-Performance-

# Table of Contents

- [Introduction](#introduction)
- [Problem Statement](#problem-statement)
- [Dataset Overview](#dataset-overview)
- [Data Description](#data-description)
- [Data Cleaning](#data-cleaning)
- [Feature Engineering](#feature-engineering)
- [Data Modeling (Schema & Relationships)](#data-modeling-schema--relationships)
- [DAX Measures (Power BI Calculations)](#dax-measures-power-bi-calculations)
- [Dashboard Development (Pages & Visuals)](#dashboard-development-pages--visuals)
- [Key Insights](#key-insights)
- [Recommendations](#recommendations)
- [Conclusion (optional)](#conclusion-optional)

## Introduction

This project analyzes customer financial behavior and loan performance using multiple datasets. By combining customer demographics, loan details, credit scores, payment history, and risk assessments, it provides insights for financial decision-making and risk management.

**Key datasets include:**

- **Customer Data:** Demographics, income, employment, and location  
- **Loan Data:** Loan amounts, terms, interest rates, and status  
- **Credit Score Data:** Customer credit scores over time  
- **Payment History:** Loan payments and their statuses  
- **Risk Assessment:** Risk levels for loans based on credit and loan data  

**Project Goal:**  
Understand customer profiles, evaluate creditworthiness, identify high-risk loans, and provide actionable recommendations for lenders.


## Problem Statement

Financial institutions rely on accurate risk assessment to make informed lending decisions. However, predicting loan defaults and identifying high-risk customers is a complex task due to the multifaceted nature of customer behavior. Factors such as demographics, income, employment status, credit history, loan terms, and payment behavior interact in ways that make risk prediction challenging.

Ineffective assessment can lead to financial losses, higher default rates, and missed opportunities for profitable lending. Therefore, there is a critical need for a comprehensive, data-driven approach to evaluate customer creditworthiness, monitor repayment patterns, and assess overall loan risk.

This project aims to address these challenges by analyzing multiple interconnected datasets, including customer profiles, loan information, credit scores, payment histories, and risk assessments. The specific objectives are to:  
- Evaluate customer creditworthiness using demographic and financial data  
- Identify trends and patterns in loan application and repayment behavior  
- Detect high-risk loans and customers proactively to minimize defaults  
- Generate actionable insights to improve lending strategies and risk management processes
## Dataset Overview

| Dataset Name | Description | Key Columns | Purpose |
|--------------|-------------|------------|---------|
| **Customer Data (`customer_data`)** | Demographic and personal information for each customer | `customer_id`, `name`, `age`, `gender`, `income`, `employment_status`, `marital_status`, `address`, `city` | Understand customer profiles and their potential impact on loan behavior |
| **Loan Data (`loan_data`)** | Details of loans taken by customers | `loan_id`, `customer_id`, `loan_amount`, `loan_term`, `interest_rate`, `loan_status` | Analyze loan distribution, repayment behavior, and financial exposure |
| **Credit Score Data (`credit_score_data`)** | Tracks customer credit scores over time | `customer_id`, `credit_score`, `score_date` | Evaluate financial reliability and creditworthiness |
| **Payment History (`payment_history`)** | Records of individual loan payments | `payment_id`, `loan_id`, `payment_date`, `amount_paid`, `payment_status` | Assess repayment behavior and detect delinquencies |
| **Risk Assessment (`risk_assessment`)** | Risk evaluations for loans and customers | `assessment_id`, `customer_id`, `loan_id`, `credit_score`, `loan_amount`, `risk_level` | Support proactive risk management and informed loan decisions |


## Data Cleaning

Data cleaning and preparation were performed in **Power BI** using **Power Query** to ensure accurate, consistent, and analysis-ready datasets. The following steps were applied:

1. **Loading Data**  
   - Imported all five datasets (`customer_data`, `loan_data`, `credit_score_data`, `payment_history`, `risk_assessment`) into Power BI.  
   - Ensured proper connection types and relationships between tables for consistent analysis.

2. **Removing Duplicates**  
   - Identified and removed duplicate records in each dataset using Power Query’s `Remove Duplicates` function.  
   - Example: Duplicate `customer_id` entries in `customer_data` or repeated `loan_id` in `loan_data` were removed to avoid skewed results.

3. **Correcting Data Types**  
   - Used Power Query to convert columns to appropriate data types:  
     - `Date/Time` for date fields (`payment_date`, `score_date`)  
     - `Decimal Number` for numerical fields (`income`, `loan_amount`)  
     - `Text` for categorical fields (`gender`, `loan_status`, `risk_level`)  
   - This ensures calculations, aggregations, and visuals work correctly in Power BI.

4. **Standardizing Data**  
   - Ensured consistent formats and naming conventions across datasets:  
     - Corrected capitalization and spelling (`Male` instead of `male`, `Approved` instead of `approved`).  
     - Standardized categorical values like employment status, marital status, and city names.

5. **Handling Missing Values**  
   - Applied Power Query transformations to handle nulls:  
     - Replaced missing numeric values with average, median, or 0 depending on the context.  
     - Filled missing categorical values with `Unknown` or most frequent value.  
     - Removed rows with missing primary identifiers (`customer_id` or `loan_id`) to maintain relational integrity.

6. **Validating Data Relationships**  
   - Verified that relationships between tables were consistent:  
     - Each `loan_id` in `payment_history` exists in `loan_data`.  
     - Each `customer_id` in `loan_data` exists in `customer_data`.  

By using Power Query, all data transformations were **applied systematically and reproducibly**, ensuring that the datasets are clean, consistent, and ready for feature engineering, modeling, and dashboard development in Power BI.



