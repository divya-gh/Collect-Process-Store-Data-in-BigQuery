# Collect-Process-Store-Data-in-BigQuery
## Cloud Data Analytics Capstone Project : Certification Capstone | Google Cloud | BigQuery | SQL

# 📌 Project Overview

### This capstone project demonstrates the first three stages of the data lifecycle in a cloud environment:

## Collect → Process → Store

### Using Google BigQuery, I built an end-to-end analytical workflow to support a fintech business use case. The objective was to help the Treasury department of a fictional company, TheLook Fintech, monitor financial performance and loan risk distribution using structured cloud data analytics.

#### This project showcases practical skills in:
- BigQuery environment setup
- SQL-based data exploration
- Data ingestion from Cloud Storage
- Table joins and transformations
- Nested & structured data handling
- Deduplication
- Aggregation and reporting
- Creating shareable analytical tables

# 🏢 Business Scenario
##### TheLook Fintech provides loans to independent online store owners.

##### As a Cloud Data Analyst, I was tasked with helping the Treasury team answer three key business questions:

1. 💰 How can we monitor cash flow to ensure loans issued do not exceed incoming payments?
2. 📊 What are the top reasons customers take out loans?
3. 🌎 How are loans distributed geographically to manage regional risk exposure?

# 🛠️ Tools & Technologies
* Google BigQuery
* SQL (Standard SQL)
* Google Cloud Storage
* Connected Sheets
* Cloud Console
* Nested & Structured Data (RECORD types)

#🔄 Project Workflow

## 1️⃣ Explore & Understand the Dataset
- Navigated the fintech dataset
- Identified key business fields:
- loan_amount
- issue_year
- int_rate
- application.purpose
- Inspected schemas and previewed data
- Identified nested RECORD structures

## 2️⃣ Collect External Data (Cloud Storage → BigQuery)

#### Imported a regional classification CSV from Cloud Storage:

LOAD DATA OVERWRITE fintech.state_region
(
state STRING,
subregion STRING,
region STRING
)
FROM FILES (
format = 'CSV',
uris = ['gs://.../state_region_*.csv']);

✔ Created a structured BigQuery table
✔ Validated data import
✔ Prepared data for regional analysis

## 3️⃣ Process Data (Joins & Transformations)
#### Joined loan and regional data:

SELECT
lo.loan_id,
lo.loan_amount,
sr.region
FROM fintech.loan lo
INNER JOIN fintech.state_region sr
ON lo.state = sr.state;

✔ Combined datasets
✔ Ensured referential accuracy
✔ Prepared report-ready dataset

## 4️⃣ Create Analytical Tables (CTAS)
#### Used CREATE TABLE AS SELECT (CTAS) to persist results:

CREATE OR REPLACE TABLE fintech.loan_with_region AS
SELECT ...

✔ Enabled downstream reporting
✔ Created reusable analytical layer
✔ Connected results to Google Sheets

## 5️⃣ Work with Nested Data
#### Extracted nested loan application details:

SELECT loan_id, application.purpose
FROM fintech.loan;

✔ Demonstrated understanding of STRUCT / RECORD types
✔ Used dot notation for nested field access

## 6️⃣ Deduplicate Data
#### Removed duplicate loan purposes:

SELECT DISTINCT application.purpose
FROM fintech.loan;

✔ Created clean reference table
✔ Improved analytical accuracy

## 7️⃣ Aggregate & Report
#### Generated annual loan totals:

SELECT issue_year,
SUM(loan_amount) AS total_amount
FROM fintech.loan
GROUP BY issue_year;

✔ Performed grouped aggregation
✔ Delivered executive-ready financial summary

## 📊 Key Deliverables

✔ Loan report by region
✔ Clean loan purpose reference table
✔ Annual total loan issuance report
✔ Loan count by year table
✔ Connected Sheets integration for stakeholders

## 🎯 Skills Demonstrated
- Cloud-based data ingestion
- Data modeling in BigQuery
- SQL joins and aggregation
- Nested data querying
- Deduplication strategies
- CTAS table creation
- Business metric translation into SQL
- Analytical storytelling for stakeholders

## 🧠 What This Project Proves
#### This capstone demonstrates my ability to:
 - Translate business questions into analytical SQL
 - Work confidently in a cloud-native data warehouse
 - Transform raw data into structured reporting assets
 - Handle nested data and schema exploration
 - Create scalable, shareable reporting datasets

## 📸 Portfolio Note
 - Screenshots of:
    * Query results
    * Table schemas
    * Connected Sheets reports
    * Final aggregated outputs
are included in this repository under /screenshots.

## 🚀 Next Steps
#### Future enhancements could include:
- Implementing BigQuery partitioned tables
- Creating materialized views for performance optimization
- Building dashboard visualization (Looker / Data Studio)
- Adding anomaly detection for cash flow monitoring

## 📌 Certification
#### Cloud Data Analytics Certification – Capstone Project
#### Demonstrating proficiency in collecting, processing, and storing cloud data using BigQuery.
