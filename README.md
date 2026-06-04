# Loan Default Pattern Analytics
### End to End Risk pipeling | SQL . Python . Power BI | BFSI Domain
---
### About this Project

I built this project to demonstrate how a data analyst thinks inside a environment - not just technically, but commercially.

MY background is in operations at Amazon and Sutherland, where I worked with structured data daily like CRM records, performance reports, SLA tracking, compilance workflows. I understand what it means, when data is messy, when deadlines are real, and when the output needs to be understood by someone who does not read code.

This project replicates the kind og work a junior analyst would do inside a retail bank's credit operations team. The tools are the same. The thinking is the same. The output is something a risk manager could actually act on.

The Business Problem
A retail bank has 1,50,000 loan recoreds and a rising default rate.
The risk team needs to know:
- Which customers segments carry the highest default risk?
- What financial signals predict default  most reliably?
- Are there suspicicious profiles the standard approval process is missing?
-  What specific policy changes would reduce default exposure?

  ### Pipeline Architecture

  RAW DATA (1,50,000)
  |
  Stage 1 - SQL: Extract < Segment < Query
  |
  Stage 2 - Python: Clean < Engineer features < Detect anaomalies
  |
  stage 3 - Power BI: Interactive dashboard for business users

  Each stage has a clear job and passes its output to the next.
  This mirrors how real data teams are strcutcured in Indian BFSI firms.

  ---

  ### Key Findings

  **Finding 1 - Age is an independent risk factor**
  Borrowers under 30 default at 10.52% vrsus 4.02% for borrower over 50.
  This gap hold even after controlling for icnome - age carries risk 
  Information taht income alone does not capture.

  **Finding 2 - Revolving utilization is the strongest predictor**
  I expected income to matter most. It did not.
  Customers using more than 70% of their available credit defaulted at nearly 3x the rate of low utilization customers.
  This single variable has a correlation of 0.25 with default of the highest in dataset.

  **Finding 3 - The anomaly cluster**

Isolation Forest flagged 7,252 accounts (5% of data) as anomalous
These are customers who looks acceptable on any sinle measure but are statisticallt unusual in combination of high debt, low income, late payments, high utlization, all at once.
Cross vaidated with z score analysis: 924 accounts flagged by both methods. These are highest confidence risk cases.

**Finding 4 - Income has a threshold effect**
Default rates drop sharply abve $3,500/month income.
Above that additional income provides diminshing protection.
A minimum financial floor mattrs more than maximising income.

---

### Business Recommendations

**1. Age tiered approval criteria**
Borrowers under 28 with less than 2 years of credit history should face additional verifications not automatic rejection but a second looks. The default rate in this segment is too high to treat the same as mid career borrowers.

Expected impact: 20-25% reduction in defaults for the under 30 segment.

**2. Anomaly review queue**
Any application flagged as anomalous by teh model should go to human review before disbursement. Routing 5% of appications for a second look is far cheaper than absorbing the defaults that slip through.

Expected impact: If 40% of flagged loans are restructured or declined portofolio default rate drops by aproximately 2.5% 

**3. Revolving utilization hard limit**
Customers currently using more than 75% of their revolving credit should not receive new loans unless income exceeds $60,000/month. This is the single highest signal policy change the data supports.

Expected impact: 18% reduction in default volume.

---

### Technical Work

#### Data Cleaning
- 1.50,000 raw recordds -> 1,45,038 clean records after removing impossible vlaues
- 29.731 missing Monthly Income vlaues filled using median imputation
- 3.924 missing Number of Dependents vaues filled using mode
- Removed records with age below 18, income of zero and credit utilization above 100%

  ####Feature Engineering
  Three new features created to improve analysis depth:
  - **emi_burden** - debt ratio relative to income
  - **risk_score** - weighted combination of debt ratio and utilization
  - **age_group** - Young / Mid / Senior segmentation

  #### Anomaly Detection
  - Primary method: Isolation Forest (scikit - learn) with contamination=0.05
  - Secondary validation: z-score with threshold of 3 standard deviations
  - Result: 7,252 flagged by Isolation Forest | 924 confirmed by both methods

  ---

  ### Tools and Technologies
  | Tool | Purpose |
  |------|----------|
  | PostgreSQL / SQLite | Data extraction and segmentation |
  | Python - pandas, Numpy | Cleaning and feature engineering |
  | Python - sickit-learn | Isolation Forest anomaly detection |
  | Python - matplotlib, seaborn | Exploratory visulaization |
  | Power BI | Interactive business dashboard |
  | Jupyter Notebook | Analysis and documentation |
  | Github | Version control and portofolio|

  ---

  ### What This Project Demonstrates

  - End to end pipeing thinking and not just one tool in isolation
  -  Domain knowledge of BFSI risk workflows
  -  Ability to translate technical findigns into business perspective
  -  ML application beyond standard EDA
  -  The kidn of output a risk manager or operatins head can act on
 
  ---

  ### Dataset
  **Source:** Kaggle - Give me some credit competition
  **Size:** 1,50,000 rows | 12 coloumns
  **Target:** SeriousDlqin2yrs (1 = defaulted, 0 = did not default)
  **License:** Free for educational and portfolio use

  ---

  ### How to Run
  1. Download cs-training.csv from kaggle (Give Me Some Credit)
  2. Run notebooks inn order: 01 -> 02 -> 03 -> 04
  3. Output CSVs generate automatically in folder
  4. Open Power BI file from powerbi folder

  ---

  ### About Me

  MBA in Business Analytics | SRM University, Chennai (2024)
  Operations background at Amazon and Sutherland Global Services
  Targeting Data Analyst | Operations Analyst | MIS Analyst roles
  Chennai | Hybrid | Remote

  This project is part of my portofolio demonstrating end to end analytics capability for entry level data analyst roles.
