# Loan-Performance-Risk-assessment-Performance-

# Table of Contents

- [Introduction](#introduction)
- [Problem Statement](#problem-statement)
- [Dataset Overview](#dataset-overview)
- [Data Description](#data-description)
- [Data Cleaning](#data-cleaning)
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


## 7. Data Modeling

The project uses a **star-schema data model**, connecting loan, customer, payment, credit score, and risk assessment data to enable smooth analysis and cross-filtering across visuals.

---

### 📁 Tables in the Data Model

#### **1. `customer_data` (Fact)**
- `customer_id`
- `age`
- `city`
- `address`
- `Age Group`

#### **2. `LoanPerformance`**
- `loan_id`
- `customer_id`
- `loan_amount`
- `loan_term`
- `interest_rate`
- `loan_status`

#### **3. `payment_history`**
- `payment_id`
- `loan_id`
- `payment_date`
- `amount_paid`
- `payment_status`

#### **4. `credit_score_data`**
- `customer_id`
- `credit_score`
- `score_date`
- *Latest Credit Score* (calculated)

#### **5. `risk_assessment`**
- `assessment_id`
- `customer_id`
- `loan_amount`
- `credit_score`

---

### 🔗 Relationship Structure

- **customer_data (1)** → **LoanPerformance (*)**
- **LoanPerformance (1)** → **payment_history (*)**
- **customer_data (1)** → **credit_score_data (*)**
- **customer_data (1)** → **risk_assessment (*)**

These relationships allow:
- Customer-level filtering across all tables  
- Linking loan records to payment history  
- Tracking credit score trends  
- Assessing loan risk per customer  

---
<img width="1138" height="726" alt="image" src="https://github.com/user-attachments/assets/b8d43cce-a364-4fcf-b318-63c2e59b695e" />

### 📌 Summary

The modeling structure supports:
- Customer profiling  
- Loan lifecycle tracking  
- Default and risk analysis  
- Credit score monitoring  
- Drill-through capabilities  

---
## 8. DAX Measures

This project uses several DAX measures to compute KPIs, aggregations, default metrics, credit score calculations, and risk levels.  
These measures help drive the analytical visuals in the Loan Risk Assessment Dashboard.

---

### 🔹 **1. Total Loan Amount**
Total Loan Amount = SUM(LoanPerformance[loan_amount])

Age Group = SWITCH(TRUE(),
  'customer_data (Fact)'[age] < 25, "<25",
  'customer_data (Fact)'[age] <= 34, "25-34",
  'customer_data (Fact)'[age] <= 44, "35-44",
  'customer_data (Fact)'[age]<= 54, "45-54",
   'customer_data (Fact)'[age]<= 64, "55-64",
  "65+"
)

Highest_Default_Age = 
CALCULATE(
    MAX('customer_data (Fact)'[Age Group]),
    FILTER(
        'LoanPerformance',
        'LoanPerformance'[loan_status] = "Defaulted"
    )
)
female = CALCULATE(COUNTROWS('customer_data (Fact)'),FILTER('customer_data (Fact)','customer_data (Fact)'[gender] = "Female"))
male = CALCULATE(COUNTROWS('customer_data (Fact)'),FILTER('customer_data (Fact)','customer_data (Fact)'[gender] = "Male"))


Highest_Default_Age = 
CALCULATE(
    MAX('customer_data (Fact)'[Age Group]),
    FILTER(
        'LoanPerformance',
        'LoanPerformance'[loan_status] = "Defaulted"
    )
)

Income Range = 
SWITCH(
    TRUE(),
    'customer_data (Fact)'[income] <= 2000, "0–2K",
    'customer_data (Fact)'[income] <= 4000, "2K–4K",
    'customer_data (Fact)'[income] <= 6000, "4K–6K",
    'customer_data (Fact)'[income] <= 8000, "6K–8K",
    'customer_data (Fact)'[income] <= 10000, "8K–10K",
    'customer_data (Fact)'[income] <= 12000, "10K–12K",
    'customer_data (Fact)'[income] <= 14000, "12K–14K",
    'customer_data (Fact)'[income] <= 16000, "14K–16K",
    "16K+"
)

Avg_Loan_Term = AVERAGE('LoanPerformance'[loan_term])

Default  Percentage = 
DIVIDE(
    [Defaulted Count], 
    COUNTROWS('LoanPerformance'), 
    0
) * 100

Defaulted Count = CALCULATE(COUNTROWS('LoanPerformance'),'LoanPerformance'[loan_status] = "Defaulted")

paid of count = CALCULATE(COUNTROWS('LoanPerformance'),'LoanPerformance'[loan_status]= "Paid off")

Paid off  Percentage = 
DIVIDE(
    [paid of count], 
    COUNTROWS('LoanPerformance'), 
    0
) * 100

Total Defaulted Amount = 
CALCULATE(
    SUM('LoanPerformance'[Loan_amount]),
    'LoanPerformance'[loan_status] = "Defaulted"
)

Total Missed Amount = 
CALCULATE(
    SUM('LoanPerformance'[Loan_amount]),
    'LoanPerformance'[loan_status] = "Missed"
)

Total PaidOff Amount = 
CALCULATE(
    SUM('risk_assessment'[loan_amount]),
    'LoanPerformance'[Loan_status] = "Paid Off"
)

% High Risk = 
DIVIDE(
    [High Risk Count],
    CALCULATE(COUNTROWS(risk_assessment))
)

High Risk Count = 
CALCULATE(
    COUNTROWS(risk_assessment),
    risk_assessment[risk_level]= "High"
)


High Risk Customers = 
CALCULATE(COUNT(risk_assessment[customer_id]), risk_assessment[risk_level] = "High")


## 9. Dashboard Development

The dashboard was designed in **Power BI** to provide a complete view of loan performance, customer behavior, payment history, credit scoring, and risk levels.  
It consists of **multiple visuals** arranged to deliver insights in a clean and business-focused layout.

---

### 🎨 **Dashboard Pages**

#### **1. Loan Overview Dashboard**
This main page provides a high-level summary of loan KPIs and performance metrics.

---

### 📊 **Visuals Included**

#### **🔹 KPI Cards**
- **Average Interest Rate**
- **Total Loan Amount**
- **Total Customers**
- **Defaulted Count**
- **Average Loan Term**

These KPIs give a quick snapshot of overall loan portfolio performance.

---

### 🔹 **Monthly Paid Amount (Line Chart)**
Shows monthly payment trends to identify:
- High payment months  
- Seasonal trends  
- Fluctuations in loan repayment behavior  

---

### 🔹 **Loan Applications by Age Group (Bar Chart)**
Displays how different age groups contribute to loan applications.  
Helps understand customer demographic distribution.

---

### 🔹 **Loan Status (Donut Chart)**
Breakdown of:
- Approved  
- Paid Off  
- Rejected  
- Defaulted  

Provides a clear picture of the loan lifecycle.

---

### 🔹 **Risk Level Ratio (Donut Chart)**
Displays:
- High Risk  
- Medium Risk  
- Low Risk  

Helps in portfolio risk segmentation.

---

### 🔹 **Default Percentage by Loan Term (Scatter Plot)**
Shows the relationship between:
- Loan terms  
- Default percentages  

Helps identify whether longer terms have higher default probability.

---

### 🔹 **Customer Credit Score Integration**
Using DAX, the dashboard shows:
- Latest Credit Score  
- Risk classification  
- Customer-level filtering  

This enhances customer scoring and default prediction analysis.

---

### 🔹 **Filter / Slicer Panel**
Includes dynamic filters:
- **Month**
- **Payment Status**
- **Loan ID / Loan Amount List**
- **Drill Through Options**

These allow the user to interactively explore loan records.

---

### 📌 **Dashboard Design Notes**
- Dark theme for modern & clean look  
- Teal accent color for highlights  
- Consistent spacing and layout  
- Simple icons for clarity  
- Visuals aligned for readability  

---

### 📥 **PBIX File Location**

The full interactive dashboard is stored in:
<img width="1156" height="691" alt="image" src="https://github.com/user-attachments/assets/393c5354-fcd5-485c-bc53-aa5a545d006d" />

<img width="1129" height="732" alt="image" src="https://github.com/user-attachments/assets/200db4a3-2bda-44bf-a4c8-971e6719beab" />

<img width="1264" height="692" alt="image" src="https://github.com/user-attachments/assets/46aa7eb0-d58b-48f5-92bb-70453a34bd30" />


Drill Through Page 
<img width="652" height="499" alt="image" src="https://github.com/user-attachments/assets/2eb376c9-f2b9-409f-8c8e-6edaaf7bd90b" />




