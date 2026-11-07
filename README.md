# IKEA Gifting — Customer Segmentation & Churn Analysis

## Disclaimer

**IKEA Gifting** is a fictional company created for this educational portfolio project. It is not affiliated with, endorsed by, or representative of IKEA. All financial figures, customer counts, and business metrics are based on a public, anonymized dataset and do not represent IKEA's actual business performance. IKEA-inspired branding is used only for dashboard design and storytelling.

---

## Project Overview

This project focuses on customer segmentation, purchasing behaviour, and churn analysis for a fictional UK-based gifting and home décor e-commerce business, **IKEA Gifting**.

The objective is to analyse customer purchasing patterns, identify high-value customers, understand customer inactivity, and provide insights that can support better customer retention strategies.

I used SQL Server for data cleaning and exploration, Python for RFM analysis and customer segmentation, and Power BI to build an interactive dashboard.

The project follows an end-to-end data analytics workflow, from raw transactional data to business insights and visual reporting.

## Business Problem

The business wants to understand its customers better, identify its most valuable customers, and find customers who may stop purchasing.

Without proper customer segmentation and retention analysis, the business may struggle to identify important customers and make informed marketing decisions.

## Business Questions

- Who are the most valuable customers?
- Which customers contribute the most revenue?
- Which customers are at risk of becoming inactive?
- How does customer purchasing behaviour change over time?
- Which customer segments generate the highest revenue?
- How does customer value and churn vary across countries?
- What actions can the business take to improve customer retention?

---

## Key Findings

- Champions account for approximately **22% of customers** and contribute close to **68% of total revenue**.
- Overall customer churn is approximately **50.86%**, using a 90-day inactivity threshold.
- Customer value varies significantly across segments, with Champions contributing substantially more revenue than Lost customers.
- Revenue shows seasonal increases during Q4, highlighting the importance of seasonal purchasing patterns.

*Note: These figures are based on the analysis performed in this project.*

---

## Data Source

**Online Retail II Dataset — UCI Machine Learning Repository**

The dataset contains anonymized transactional records from a UK-based online retailer selling giftware.

- Source: UCI Machine Learning Repository
- Period: December 2009 – December 2011
- Raw records: Approximately 1,067,371
- Data type: Customer transactions and purchasing information

The dataset includes invoice details, product information, quantities, prices, customer IDs, and countries.

---

## Tools & Technologies

| Tool | Purpose |
|---|---|
| SQL Server / SSMS | Data cleaning, data validation, deduplication, and exploratory analysis |
| Python | RFM analysis, customer scoring, segmentation, and churn identification |
| Pandas | Data manipulation, cleaning, and calculations |
| Jupyter Notebook | Python development and analysis |
| Power BI | Interactive dashboard development |
| DAX | Business measures and KPI calculations |

---

## Core Concepts Demonstrated

- **Data Cleaning:** Handling missing values, invalid records, duplicate transactions, and date-format inconsistencies.
- **SQL Analysis:** Using SQL queries, data type conversion, aggregation, and window functions.
- **RFM Analysis:** Evaluating customers based on Recency, Frequency, and Monetary value.
- **Customer Segmentation:** Grouping customers into meaningful categories based on purchasing behaviour.
- **Churn Analysis:** Identifying inactive customers using a 90-day inactivity threshold.
- **Data Visualization:** Building interactive dashboards to communicate business insights.
- **DAX:** Creating measures for revenue, customer counts, churn percentage, and average customer value.

---

## Project Workflow

### Step 1 — Data Import & Cleaning (SQL Server)

- Imported the Online Retail II dataset into SQL Server.
- Combined transactional data from both source sheets.
- Handled mixed date formats and converted columns into appropriate data types.
- Removed duplicate transactions.
- Checked missing customer IDs and invalid transaction records.
- Performed data validation and exploratory analysis.

### Step 2 — Customer Analysis (Python)

- Loaded the cleaned transactional dataset into Python using Pandas.
- Removed records with missing customer IDs and invalid quantities.
- Calculated customer Recency, Frequency, and Monetary values.
- Applied quintile-based scoring from 1 to 5.
- Created customer segments based on RFM scores.
- Identified inactive customers using a 90-day threshold.

### Step 3 — Data Preparation & Integration

- Merged customer-level RFM results with transaction-level data using `customer_id`.
- Added calculated columns such as Invoice Month and Revenue.
- Prepared a unified dataset for Power BI.
- Exported the final dataset to Excel.

### Step 4 — Dashboard Development (Power BI)

- Created interactive KPI cards.
- Analysed customer distribution and revenue by segment.
- Compared customer value across different segments.
- Analysed churn trends and purchasing patterns.
- Added filters for country, month, year, customer segment, and churn status.

---

## Dashboard Structure

### Page 1 — Home
- Project introduction.
- Dashboard navigation.
- Definitions of key analytical terms.

### Page 2 — Business Overview
- Total Customers
- Total Revenue
- Customer Churn %
- Average Customer Value
- Revenue and customer trends.
- Customer segment distribution.
- Country-level analysis.

### Page 3 — RFM Analysis
- Customer count by segment.
- Revenue contribution by segment.
- Average RFM scores.
- Average customer value by segment.
- Customer churn analysis.

---

## Sample SQL — Handling Mixed Date Formats

```sql
SELECT
    invoice,
    stockcode,
    description,
    quantity,
    COALESCE(
        TRY_CONVERT(datetime2, invoicedate, 120),
        TRY_CONVERT(datetime2, invoicedate, 105)
    ) AS invoicedate,
    TRY_CONVERT(decimal(10,2), price) AS price,
    customer_id,
    country
INTO dbo.RetailCombined
FROM dbo.[Year 2009-2010];
```

## Sample Python — RFM Scoring

```python
rfm['R_Score'] = pd.qcut(
    rfm['Recency'],
    5,
    labels=[5, 4, 3, 2, 1]
).astype(int)

rfm['F_Score'] = pd.qcut(
    rfm['Frequency'].rank(method='first'),
    5,
    labels=[1, 2, 3, 4, 5]
).astype(int)

rfm['M_Score'] = pd.qcut(
    rfm['Monetary'],
    5,
    labels=[1, 2, 3, 4, 5]
).astype(int)
```

---

## How to Reproduce This Project

1. Download the Online Retail II dataset from the UCI Machine Learning Repository.
2. Run the SQL scripts to import, clean, and prepare the transactional data.
3. Export the cleaned dataset and load it into the Jupyter Notebook.
4. Run the Python notebook to calculate RFM scores, customer segments, and churn flags.
5. Export the final dataset to Excel.
6. Open the Power BI report and connect it to the exported dataset.
7. Refresh the report to explore the interactive dashboard.

---

## Project Objective

This project demonstrates how SQL, Python, and Power BI can work together to solve a business problem.

It focuses on turning raw transactional data into meaningful customer insights that can help businesses understand customer value, identify inactive customers, and make better retention decisions.
