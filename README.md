# Data Professionals Survey Dashboard

## Project Overview

This repository contains an end-to-end Power BI data analysis project based on a real-world survey of over 600 data professionals collected across platforms like LinkedIn and Twitter. The project covers the entire business intelligence workflow: data ingestion, rigorous data cleaning via Power Query, custom data transformation using DAX, dashboard layout architecture, and interactive report design.

The primary objective of this dashboard is to provide a high-level breakdown of the data professional landscape, exploring salaries, programming language preferences, demographics, and workplace happiness across different roles and geographic regions.

---

## Repository Structure

The repository consists of the following key files:

* **`Power BI - Final Project.xlsx`**: The raw, uncleaned dataset containing anonymized survey responses from 630+ data professionals.
* **`Data Professionals Survey Project.pbix`**: The finalized Power BI report containing the data models, Power Query transformations, and interactive visualizations.

---

## Data Transformation & Cleaning (Power Query)

The raw survey data contained significant noise, free-text entries, and unformatted numeric ranges. The following processing steps were performed inside the Power Query Editor to prepare the dataset for analysis:

### 1. Schema Optimization

* Removed non-essential columns tracking metadata (e.g., browser types, referral links, and timestamps) to optimize data model performance.

### 2. Job Title & Language Standardization

* **Job Titles**: The "Other (please specify)" option introduced hundreds of unique text variations. To prevent visualization clutter, a split column operation was applied using the leftmost open parenthesis `(` as a delimiter, effectively grouping messy variants into standard buckets: Data Analyst, Data Engineer, Data Scientist, Data Architect, Database Developer, Student, or Other.
* **Programming Languages**: Cleaned the favorite programming language column by splitting text entries using a colon `:` delimiter to isolate primary pre-selected answers from free-text specifications.

### 3. Salary Range Monetization Technique

The original salary data was collected in text-based ranges (e.g., "106k-125k"). To make this data numerically actionable, the following steps were taken:

* Duplicated the raw salary column to preserve original contexts.
* Split the column by digit to non-digit transitions to strip characters like "K", "-", and "+".
* Replaced nulls and formatted out-of-bound entries (e.g., converting "225k+" to a static baseline).
* Changed data types to whole numbers and applied a custom column formula to calculate the **Average Salary** for each respondent group:

$$\text{Average Salary} = \frac{\text{Minimum Range Baseline} + \text{Maximum Range Baseline}}{2}$$

---

## Dashboard Features & Visualizations

The final dashboard layout was designed with a scannable, user-friendly hierarchy, utilizing customized color themes (e.g., muted professional tones) for better visual appeal.

### High-Level KPI Cards

* **Count of Survey Takers**: Displays the total population size ($N = 630$).
* **Average Age**: Shows the central demographic age of the survey participants (approximately 30 years old).

### Core Insights & Visualizations

* **Average Salary by Job Title (Stacked Bar Chart)**: Compares average earnings across distinct roles. Data Scientists lead the cohort with an average salary of ~$93,000, followed by Data Engineers and Architects, with Data Analysts averaging ~$55,000.
* **Favorite Programming Language (Clustered Column Chart)**: Tracks language popularity, showing Python as the dominant favorite among data professionals, further cross-filtered by job title roles in the legend.
* **Geographic Demographics (Tree Map)**: Breaks down respondents by country (United States, India, United Kingdom, Canada, and Other). This visual acts as a strategic master-filter, allowing users to instantly observe how regional costs of living alter average salaries globally.
* **Workplace Sentiment (Gauges)**: Utilizes configured minimum (0) and maximum (10) bounds to track the average happiness score of professionals regarding both **Salary** and **WorkLife Balance**.
* **Avg Salary differences based on sex**
