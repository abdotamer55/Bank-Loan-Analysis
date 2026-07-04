# Bank Loan Analytics Dashboard & Database Project

## 📌 Project Overview
This project is an end-to-end data analytics solution designed to monitor and assess bank loan performance. It combines a relational database setup with advanced SQL querying for deep risk analysis alongside an interactive Power BI dashboard for executive Key Performance Indicators (KPIs) and trend tracking. 

The primary objective is to evaluate loan applications, distinguish between good and bad financial risks, track monthly trends, and provide actionable segment insights using both database modeling and visual reporting.

---

## 🛠️ Tools & Technologies Used
* **Power BI Desktop:** For data transformation, DAX modeling, and visual dashboard design.
* **SQL Server / Relational Database:** For writing structured analytical queries and data extraction.
* **Power Query (M Language):** For data cleanup and ETL processes.
* **DAX (Data Analysis Expressions):** For dynamic business metrics and custom KPIs.

---

## 💾 Database Structure & Data Dictionary
The core dataset is built around the `bank_loan_data` table inside the `BankLoanDB` database. Below is the structure used for analytical queries:

| Column Name | Data Type / Format | Description & Purpose |
| :--- | :--- | :--- |
| `id` | Unique ID | Unique identifier for each loan application used in counting. |
| `issue_date` | Date | The date the loan was officially issued, used for time filtering. |
| `loan_amount` | Numeric | The total funded loan amount approved by the bank. |
| `total_payment` | Numeric | The total amount paid back by the borrower so far. |
| `int_rate` | Decimal (Percentage) | The interest rate applied to the loan. |
| `dti` | Decimal (Ratio) | Debt-to-Income ratio measuring the borrower's financial risk. |
| `loan_status` | Text / Categorical | Current state of the loan (e.g., `Fully Paid`, `Current`, `Charged Off`). |
| `term` | Text / Categorical | The duration of the loan agreement (e.g., 36 or 60 months). |
| `emp_length` | Text / Categorical | Employment duration of the applicant. |
| `home_ownership`| Text / Categorical | Residential status (e.g., `Mortgage`, `Own`, `Rent`). |
| `grade` | Text / Categorical | Credit quality rating category assignment (e.g., Grade `A`). |
| `purpose` | Text / Categorical | The explicit reason the borrower applied for the loan. |

---

## 🔍 SQL Portfolio (Risk & Trend Analysis)
The SQL scripts execute robust operations categorized into distinct stages:
1. **Basic KPI Tracking:** Calculating total loan applications, Month-to-Date (MTD), and Previous Month-to-Date (PMTD) metrics for funded amounts and payments received.
2. **Credit Risk Segmentation:**
   * **Good Loans:** Evaluating applications classified as `Fully Paid` or `Current` to figure out percentage metrics and total financial returns.
   * **Bad Loans:** Quantifying defaults and financial write-offs (`Charged Off` status) to measure risk exposure.
3. **Multi-Dimensional Grouping:** Synthesizing performance tables grouped by loan status, monthly issuance timelines, employment tenure gaps, regional homeownership dynamics, and loan motivations.

---

## 📊 Power BI Lifecycle Implementation

### 1. Data ETL & Quality Assurance
* Data connection validation and source configuration mappings.
* Rigorous cleanup steps via Power Query: Handled missing entries, stripped out duplicates, validated data types, and filtered null fields to preserve dataset integrity.

### 2. Data Modeling & Star Schema Architecture
* Arranged data entities into normalized layouts using structured schema rules.
* Built reliable data relationships with strict cardinality rules:
  * `Customers[CustomerID]` $\rightarrow$ `Orders[CustomerID]` (One-to-Many / Single Direction)
  * `Orders[OrderID]` $\rightarrow$ `Reviews[OrderID]` (One-to-Many / Single Direction)

### 3. DAX Metric Development
Custom enterprise business metrics developed include:
* **Total Revenue:** `SUM(Orders[Revenue])` - Sum of all sales.
* **Total Orders:** `COUNT(Orders[OrderID])` - Count of orders.
* **Average Order Value (AOV):** `DIVIDE([Total Revenue], [Total Orders])` - Average revenue per order.
* **Net Revenue:** `CALCULATE([Total Revenue], Orders[Status] = "Delivered")` - Revenue only from completed deliveries.
* **Review Rate:** `AVERAGE(Reviews[Rating])` - General average rating.

### 4. Interactive Report Visuals
The frontend dashboard consists of three highly tailored diagnostic views:
* **Revenue Overview:** Focused on high-level executive KPI summaries for revenue and AOV.
* **Customer Ratings:** Showcases deep-dive product and customer insights.
* **Order Details:** Dedicated view tracking precise order completions and status counts.

---

## 📈 Dashboard Key Features
* **Advanced Slicers & Filters:** Implemented Page-level parameters (`Date` ranges, `Order Status` flags) and Report-level dropdown configurations (`Customer` names) for granular data exploration.
* **Performance Security:** Zero division errors achieved through secure `DIVIDE()` functions, accompanied by a verified structural loop check ensuring clean report calculations.
