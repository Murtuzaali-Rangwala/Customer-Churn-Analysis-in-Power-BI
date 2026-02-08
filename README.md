## Customer Churn Analysis – Power BI Dashboard

This project is an end‑to‑end **telecom customer churn analysis** built in Power BI. It covers data cleaning, data modelling with DAX, and interactive dashboard design to help a telecom provider understand **which customer segments are churning, why they are leaving, and where to focus retention efforts first**.

▶️ Video walkthrough: https://youtu.be/mjfSs-BJG94 

### Business problem

The business was facing high churn and needed to:  
- Identify which customer segments are most likely to churn.  
- Quantify churn by tenure, contract type, and services.  
- Prioritise data‑driven retention initiatives that protect recurring revenue.
 
### Data cleaning and quality fixes

Key data preparation steps:  
- Removed duplicate `customerID` rows to avoid overstating churn and revenue.  
- Standardised inconsistent text values (e.g., “month to month”, “month-to-month” → “Month-To-Month”) and applied Trim/Clean to prevent fragmented segment analysis.  
- Corrected data types for `tenure`, `MonthlyCharges`, and `TotalCharges` to ensure accurate aggregations.  
- Converted `TotalCharges` to decimal and replaced nulls with 0 only when `MonthlyCharges` had a value (very new customers), preventing DAX errors while preserving billing context.  
- Fixed logical contradictions:  
  - If `PhoneService = "No"` then `MultipleLines = "No"`.  
  - If `InternetService = "No"` then `StreamingTV = "No"`.  
These steps ensure all KPIs and visuals are built on consistent, trustworthy data.

### Modelling and DAX

The model uses a cleaned Telco Churn table as the main fact table with:  
- Measures:  
  - Total Customers, Churn Customers, Retained Customers, Churn Rate %.  
  - Average Monthly Charges, plus separate averages for churned vs retained customers.  
- Calculated columns:  
  - **Tenure Band** (0–6, 6–12, 12+ months).  
  - **Customer Type** (New vs Existing).  
  - **Risk Type** (High Risk vs Normal) based on month‑to‑month contract and low tenure.  

These calculations directly support questions such as “Which segment should we call first this month?”.

### Dashboard design

Single‑page, KPI‑first layout in Power BI:  
- Top: overall KPIs (Total Customers, Churn Rate %, Churn Customers).  
- Middle: drivers of churn (by Contract, Tenure Band, Online Security/Backup, Customer Type).  
- Bottom: retention overview and churn distribution.  
Visuals are chosen by analytical question (column charts for churn by tenure, bar charts for contract and revenue, donut for retention split) with a consistent dark theme for readability.

### Key insights

- Overall churn rate is ~26.5% (1,869 of 7,043 customers).  
- New customers (0–6 months) on **Month‑To‑Month** contracts churn at over 50% and drive most of the churn volume.  
- Churned customers have higher average monthly charges (mid‑70s) than retained customers (low‑60s).  
- Customers without Online Security / Online Backup churn more and account for disproportionate lost revenue.

### Recommended actions

- Targeted onboarding and save‑offers for new, month‑to‑month customers (0–6 months).  
- Plan and pricing reviews for high‑charge, short‑tenure, month‑to‑month customers.  
- Bundle Online Security and Online Backup in acquisition offers and track churn differences by bundle usage.

### Dashboard Snapshots

<img width="1437" height="807" alt="1" src="https://github.com/user-attachments/assets/62569c07-05f1-4b9d-803a-d61d98d56a9a" />
Dashboard

<img width="1435" height="803" alt="2" src="https://github.com/user-attachments/assets/a00a36d1-0582-4d01-aa0d-3b049abeb572" />
Filtered by – Retained Customers by Risk Type – “Normal”

<img width="1432" height="797" alt="3" src="https://github.com/user-attachments/assets/eb7900b1-3f5c-4ea7-a001-8e6e574f92b2" />
Filtered by – Retained Customers by Risk Type – “High Risk”

<img width="1431" height="802" alt="4" src="https://github.com/user-attachments/assets/63fd7797-331c-464e-8420-9adf3930d5bd" />
Filtered by – Customer Retention – “Churn = No” and Churn Customers by Contract – “Month-To-Month”
<br>
<br>
<br>



For this project I used synthetic data rather than a directly downloaded public dataset.
I used Perplexity with a clear prompt to generate a telco‑style churn dataset similar to the classic Telco Customer Churn data (contracts, tenure, charges, services, churn flag). I then treated it as raw operational data and did all the cleaning, modelling and dashboarding myself in Power BI including handling duplicates, inconsistent labels and a few intentional logical errors to mirror real‑world data issues.
