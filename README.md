# Bank Customer Insight & Analytics (CH08)

> **DS Sprint – Skill Based Assessment 2**  
> **Course:** Data Science (U23AD491) | **Institution:** Sri Eshwar College of Engineering  
> **Case Study:** TrustWave Bank – Customer 360 & Service Delivery Analytics

---

## 📌 Project Overview
An end-to-end data analytics and machine learning solution for **TrustWave Bank**. It unifies fragmented operational data across 1,000 customers, diagnoses a severe 58% commercial transaction drop, isolates regional support bottlenecks, and predicts at-risk customer complaints with **97.0% recall**.

---

## 📂 Repository Structure

```text
CH08_Bank_Customer_Insight/
├── data/                             # Raw relational CSV datasets
│   ├── customers.csv                 # Customer demographics, region & segment
│   ├── accounts.csv                  # Account types, balances & status
│   ├── transactions.csv              # Transaction records, amounts & channels
│   ├── channels.csv                  # Monthly branch, ATM, web & mobile logins
│   └── service.csv                   # Support tickets, repeat flags & complaints
├── outputs/
│   ├── charts/                       # 6 High-resolution analytical charts (PNG)
│   └── cleaned_data/                 # Cleaned datasets & customer_360_analysis.csv
├── Bank_Customer_Analysis.xlsx       # Dynamic 8-sheet Excel Dashboard with formulas
├── CH08_Bank_Customer_Insight.ipynb  # Master Jupyter Notebook (EDA, ML & Excel generation)
└── README.md                         # Project documentation
```

---

## 🔍 Key Findings (6 Analytical Questions)

| # | Business Question | Core Finding | Output Chart |
|:--|:---|:---|:---|
| **1** | **Top Channels Used** | **Mobile Banking** leads with 45.8% volume (35,463 tx), while physical branches account for only 8.2%. | `chart1_channel_usage.png` |
| **2** | **Channel Use by Age** | Youth (18–40) are >72% digital. Seniors (60+) rely heavily on Branches (18 visits/mo) and ATMs (16/mo). | `chart2_channel_by_age.png` |
| **3** | **Declining Account Types** | **Current Accounts** suffered a **58% volume drop** in 2025 (falling from 280 tx/mo in Jan to 118 in Dec). | `chart3_account_activity_trend.png` |
| **4** | **Regional Complaints** | **North Region** is the top hotspot with 148 complaints (42.1% complaint rate vs. 22% bank average) and a 40% backlog. | `chart4_complaints_by_region.png` |
| **5** | **Balance by Segment** | Corporate (median $105k) and Wealth (median $62k) hold 84% of total deposits. Retail median balance is $2,450. | `chart5_balance_by_segment.png` |
| **6** | **Repeat Service Drivers** | **Password Reset** (61.3% repeat rate) and **Disputed Charges** (48.5%) generate over 50% of support overhead. | `chart6_repeat_service_requests.png` |

---

## 🤖 Machine Learning Model Performance

Predicting dissatisfied customers (`has_complaint`) using a **Random Forest Classifier** (`n_estimators=120`, `max_depth=6`, `class_weight='balanced'`):

| Metric | Score | Key Interpretation |
|:---|:---:|:---|
| **Recall** | **97.0%** | Captures 65 out of 67 actual at-risk complaint customers |
| **ROC-AUC** | **0.8866** | Strong discriminative ability between complaint & non-complaint profiles |
| **Accuracy** | **73.2%** | Solid overall classification accuracy on held-out test data |
| **F1-Score** | **0.6599** | Balanced trade-off under high class imbalance |
| **Precision** | **50.0%** | 1 in 2 flagged customers is a verified complaint risk |

* **Key Predictors:** `service_request_count`, `days_since_last_tx`, `region_North`, `mobile_usage`, `tx_total_amount`.

---

## 📊 Excel Analytics Workbook (`Bank_Customer_Analysis.xlsx`)

Built with native Excel formulas and formatting across **8 structured worksheets**:
1. `Summary_Dashboard`: KPI Cards, visual executive summary & embedded charts.
2. `Cleaned_Data`: Master Customer 360 dataset (1,000 records × 19 fields).
3. `Statistical_Summary`: Automated statistical formulas (`COUNT`, `AVERAGE`, `MEDIAN`, `STDEV.S`, `COUNTIF`).
4. `Channel_Analysis`: Cross-tabulated channel adoption and age demographics.
5. `Account_Activity`: Monthly transaction volume tracking commercial account decline.
6. `Complaint_Analysis`: Regional breakdown, unresolved rates, and risk ratings (`COUNTIF`).
7. `Balance_Analysis`: Segment deposit distribution and share of wallet (`SUMIF`, `AVERAGEIF`).
8. `Service_Requests`: Ticket volumes, repeat rates, and service friction metrics.

---

## 💡 Strategic Recommendations

1. **North Region Task Force:** Deploy a dedicated Tier-2 dispute resolution pod for North branches targeting a 48-hour resolution SLA to clear the 40% backlog.
2. **Self-Service & Senior Support:** Roll out in-app biometric password recovery to eliminate the 61.3% repeat reset calls, and establish "Digital Concierge" desks in branches to guide senior customers.

---

## 🚀 How to Run

1. Open the project folder in **VS Code**.
2. Open [`CH08_Bank_Customer_Insight.ipynb`](CH08_Bank_Customer_Insight.ipynb).
3. Select your **Python 3.14** kernel and click **Run All**.
   * It performs EDA, cleans data, trains the ML model, outputs the 6 charts to `outputs/charts/`, and generates `Bank_Customer_Analysis.xlsx`.
