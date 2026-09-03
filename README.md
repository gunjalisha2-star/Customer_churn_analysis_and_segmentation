# Customer Churn Risk Analysis & Segmentation

## 📌 Project Overview

This project analyzes subscription-based customer data to identify customer churn patterns, revenue at risk, and high-risk customer segments.

The objective is to help businesses understand why customers churn and identify customers who should be prioritized for retention strategies.

The project follows a complete data analytics workflow:

**Extract → Clean → Merge → Feature Engineering → Analyze → Visualize → Segment → Report**

---

## 🎯 Business Objective

The main objectives of this project are:

* Analyze customer churn patterns.
* Calculate the overall churn rate.
* Identify customer segments with a higher risk of churn.
* Analyze churn based on subscription plans.
* Identify the impact of customer acquisition sources.
* Calculate revenue at risk from churned customers.
* Analyze customer complaints and escalations.
* Segment customers into Low, Medium, and High churn-risk categories.

---

## 🛠️ Tools & Technologies Used

* Python
* Pandas
* NumPy
* SQLite
* Matplotlib
* Seaborn
* Jupyter Notebook

---

## 📂 Dataset Description

The project uses an SQLite database named:

```text
customer_churn.db
```

The database contains three tables.

### 1️⃣ db_customer

Contains customer demographic information.

| Column Information |
| ------------------ |
| Customer ID        |
| Customer Name      |
| Country            |
| State              |
| Gender             |
| Date of Birth      |
| Interests          |
| Pincode            |

---

### 2️⃣ db_subscription

Contains subscription and billing information.

| Column Information      |
| ----------------------- |
| Customer ID             |
| Plan Type               |
| Contract Type           |
| Monthly Charges         |
| Customer Lifetime Value |
| Churn Score             |
| Cancellation Date       |
| Cancellation Reason     |

---

### 3️⃣ db_support

Contains customer support interaction data.

| Column Information |
| ------------------ |
| Customer ID        |
| Complaint Date     |
| Escalation Flag    |
| CSAT Score         |
| Customer Comments  |

---

# 🔄 Project Workflow

## 1. Data Extraction

The data was extracted directly from the SQLite database using:

```python
sqlite3
pd.read_sql()
```

The database tables were identified dynamically using the SQLite `sqlite_master` table.

---

## 2. Data Cleaning

The following data-cleaning steps were performed:

* Renamed the `name` column to `customer_name`.
* Removed irrelevant columns such as `interests` and `pincode`.
* Converted the `dob` column into datetime format.
* Standardized gender values.
* Filled missing country values using state-to-country mapping.
* Identified and handled duplicate support records.
* Preserved complaint frequency using `complaint_count`.

---

## 3. Data Merging

The three tables were merged using `customerid`.

The subscription table was used as the base table because every customer had a subscription record.

A left join was used to ensure customers without support interactions were not removed from the analysis.

---

## 4. Feature Engineering

The following features were created:

### Churn Flag

Customers with a cancellation date were marked as churned.

```text
1 = Churned
0 = Active
```

---

### Customer Age

Customer age was calculated using the date of birth.

---

### Tenure Days

Customer tenure was calculated using:

```text
Cancellation Date - Subscription Start Date
```

For active customers:

```text
Current Date - Subscription Start Date
```

---

### Churn Risk

Customers were segmented based on their churn score.

| Churn Score  | Risk Category |
| ------------ | ------------- |
| Below 50     | Low Risk      |
| 50–69        | Medium Risk   |
| 70 and Above | High Risk     |

---

### Complaint Count

The number of complaints made by each customer was calculated before removing duplicate support records.

---

# 📊 Key Performance Indicators

The following KPIs were calculated:

* Overall Churn Rate
* Retention Rate
* Churn Rate by Plan Type
* Churn Rate by State
* Churn Rate by Subscription Source
* Average Revenue Per User (ARPU)
* Average Customer Tenure
* Revenue at Risk
* Escalation Rate
* Average Complaints per Customer

---

# 📈 Key Findings

### 🔴 Overall Churn Rate

**28.57%**

Nearly 3 out of every 10 customers have churned.

---

### 🟢 Retention Rate

**71.43%**

Most customers remain active, but the churn rate indicates a need for stronger retention strategies.

---

### 📉 Churn by Plan Type

| Plan Type | Churn Rate |
| --------- | ---------- |
| Basic     | 60%        |
| Standard  | 22.2%      |
| Premium   | 14.3%      |

### Insight

Basic plan customers have the highest churn rate.

This indicates that plan type may be strongly associated with customer retention.

---

### 💰 Average Revenue Per User (ARPU)

**$18.85**

This provides a benchmark for average monthly customer revenue.

---

### ⚠️ Revenue at Risk

**$73.94 per month**

This represents monthly revenue associated with churned customers.

---

### 📞 Customer Support Insights

* Escalation Rate: **19.05%**
* Average Complaints per User: **0.43**

Customer complaints and escalations can be useful indicators for identifying potential churn risk.

---

# 👥 Customer Segmentation

Customers were segmented into three churn-risk categories:

🟢 **Low Risk**

🟡 **Medium Risk**

🔴 **High Risk**

This segmentation can help the business prioritize retention efforts.

High-risk customers should receive targeted actions such as:

* Personalized offers
* Customer support follow-ups
* Subscription discounts
* Loyalty benefits
* Proactive issue resolution

---

# 📊 Visualizations

The project includes the following visualizations:

* Monthly Churn Trend
* Churn Rate by Plan Type
* Churn Rate by State
* Correlation Heatmap
* Pairplot Analysis
* Customer Risk Segmentation
* Plan Type vs Monthly Charges Analysis

---

# 💡 Business Recommendations

Based on the analysis, the following actions are recommended:

### 1. Focus on Basic Plan Customers

Basic plan customers have the highest churn rate.

The business should investigate:

* Pricing
* Features
* Customer satisfaction
* Value perception

---

### 2. Investigate Referral Customers

Referral-sourced customers showed a higher churn rate compared to organically acquired customers.

The business should evaluate:

* Referral program quality
* Customer targeting
* Customer expectations

---

### 3. Prioritize High-Risk Customers

Customers classified as High Risk should be targeted first for retention campaigns.

Possible actions include:

* Personalized offers
* Discounts
* Proactive customer support
* Loyalty programs

---

### 4. Improve Support Issue Resolution

Customer complaints and escalations should be monitored regularly.

Faster issue resolution may help reduce customer dissatisfaction and potential churn.

---

# ⚠️ Project Limitations

### Small Dataset

The dataset contains only **21 customers**.

Therefore, the findings should be considered directional and exploratory rather than statistically conclusive.

---

### Escalation-Churn Correlation

The escalation column requires conversion from categorical values to numeric values before correlation analysis.

Example:

```python
df['escalations'] = np.where(
    df['escalations'] == 'Y',
    1,
    0
)
```

---

### Risk Segmentation

The current segmentation is based on predefined churn score thresholds.

Future improvements could include machine learning models such as:

* Logistic Regression
* Decision Tree
* Random Forest
* K-Means Clustering

---

# 🚀 Future Improvements

Future versions of this project could include:

* Larger customer datasets.
* Predictive churn modeling.
* Machine learning algorithms.
* Interactive Power BI dashboards.
* Customer Lifetime Value prediction.
* Automated retention recommendations.
* Real-time churn monitoring.

---

# 📁 Repository Structure

```text
Customer-Churn-Risk-Analysis/
│
├── README.md
├── Customer_Churn_Analysis.ipynb
├── customer_churn.db
├── requirements.txt
│
├── reports/
│   ├── Customer_Churn_Project_Report.pdf
│   └── Database_Schema.pdf
│
├── images/
│   ├── monthly_churn_trend.png
│   ├── churn_by_plan.png
│   ├── churn_by_state.png
│   └── correlation_heatmap.png
│
└── data/
    └── merged_customer_churn_data.csv
```

---

# ▶️ How to Run the Project

### Clone the Repository

```bash
git clone <repository-url>
```

### Install Required Libraries

```bash
pip install -r requirements.txt
```

### Open Jupyter Notebook

```bash
jupyter notebook
```

Then open:

```text
Customer_Churn_Analysis.ipynb
```

---

# 📌 Key Takeaway

This project demonstrates an end-to-end customer churn analytics workflow using Python and SQLite.

The analysis identifies churn patterns, customer segments, revenue at risk, and potential retention opportunities.

The project also demonstrates skills in:

* Data Extraction
* Data Cleaning
* Data Transformation
* SQL and SQLite
* Feature Engineering
* Exploratory Data Analysis
* Customer Segmentation
* Data Visualization
* Business Insights

---

## 👩‍💻 Author

**Isha Gunjal**

Aspiring Data Analyst | Python | SQL | Data Analytics | Power BI

