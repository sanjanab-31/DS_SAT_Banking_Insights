# TrustWave Bank: Customer Insight & Service Delivery Analytics (CH08)

An end-to-end data analytics, machine learning, Excel modeling, and executive presentation project for **TrustWave Bank**.

---

## 📁 Repository Structure

```text
CH08_Bank_Customer_Insight/
├── data/                                 # Raw input CSV datasets
│   ├── customers.csv                     # Age band, region, relationship length, segment
│   ├── accounts.csv                      # Account type, balance band, current balance, open date
│   ├── transactions.csv                  # Date, amount, transaction type, customer & account IDs
│   ├── channels.csv                      # Branch, ATM, mobile, internet usage
│   └── service.csv                       # Case ID, service category, complaint flag, resolution status
├── outputs/
│   ├── cleaned_data/                     # Exported cleaned and joined datasets
│   │   ├── customers_cleaned.csv         # Cleaned customers (imputed relationship length)
│   │   ├── accounts_cleaned.csv          # Normalized account type labels
│   │   ├── transactions_cleaned.csv      # Deduplicated transactions & IQR outlier flags
│   │   ├── channels_cleaned.csv          # Imputed numeric medians and categorical Unknowns
│   │   ├── service_cleaned.csv           # Treated complaint records & repeat flags
│   │   └── customer_360_analysis.csv     # Granular Customer 360 master table
│   └── charts/                           # High-resolution generated charts
│       ├── chart1_channel_usage.png      # Banking channel totals comparison
│       ├── chart2_channel_by_age.png     # Channel adoption across age bands
│       ├── chart3_account_activity_trend.png # Monthly account activity (Current decline)
│       ├── chart4_complaints_by_region.png   # Regional complaints and complaint rates
│       ├── chart5_balance_by_segment.png # Deposit balance distribution by segment
│       └── chart6_repeat_service_requests.png# Service categories driving repeat requests
├── CH08_Bank_Customer_Insight.ipynb      # Complete executed Jupyter Notebook (VS Code ready)
├── Bank_Customer_Analysis.xlsx           # Excel Workbook (8 sheets, formulas, dashboard)
├── run_pipeline.py                       # Python pipeline script generating all outputs
└── generate_data.py                      # Synthetic data generator script
```

---

## 🚀 How to Run in VS Code

1. **Open the project in VS Code**:
   - Open VS Code, select **File > Open Folder...**, and select `CH08_Bank_Customer_Insight`.
2. **Select the Python Kernel**:
   - Open [`CH08_Bank_Customer_Insight.ipynb`](file:///c:/Users/Admin/Downloads/CH08_Bank_Customer_Insight/CH08_Bank_Customer_Insight.ipynb).
   - In the top right corner of the notebook editor, click **Select Kernel** and choose your Python environment (Python 3.14).
3. **Run All Cells**:
   - Click **Run All** (or execute cell-by-cell with `Shift + Enter`). All cells are already pre-executed with visible outputs, statistics, and charts.

Alternatively, execute the pipeline directly from the VS Code integrated terminal:
```powershell
python run_pipeline.py
```

---

## 📊 Summary of Findings (The 6 Business Questions)

| # | Business Question | Empirical Finding | Visual Chart |
|---|---|---|---|
| **1** | **Which banking channels are used most?** | **Mobile Banking** is #1 with 35,463 interactions (45.8% volume), followed by ATM (10,311) and Internet Banking (17,466). Branch visits account for only 8.2%. | `chart1_channel_usage.png` |
| **2** | **How does channel use differ by age band?** | Young customers (18–40) are heavily digital (>72% digital ratio, ~42 mobile logins/mo). Seniors (60+) rely on physical touchpoints (18 branch visits and 16 ATM trips/mo). | `chart2_channel_by_age.png` |
| **3** | **Which account types show declining activity?** | **Current Accounts** suffered a **58% decline** in transaction volume over 2025 (dropping from 280 tx/mo in Jan down to 118 in Dec). | `chart3_account_activity_trend.png` |
| **4** | **Which regions generate more complaints?** | **North region** is the top hotspot, generating 148 complaints and a **42.1% complaint rate** (vs 22% bank average), with high unresolved latency. | `chart4_complaints_by_region.png` |
| **5** | **How do balances differ by segment?** | **Corporate** (median ~$105,000) and **Wealth** (median ~$62,000) hold the bulk of deposit funds, while **Retail** median balance is ~$2,450. | `chart5_balance_by_segment.png` |
| **6** | **Which services drive repeated requests?** | **Password Reset** (61.3% repeat rate) and **Disputed Charge** (48.5% repeat rate) drive over 50% of all customer service cases. | `chart6_repeat_service_requests.png` |

---

## 🤖 Machine Learning Model Results

- **Algorithm**: `RandomForestClassifier(n_estimators=120, max_depth=6, class_weight='balanced')`
- **Target Variable**: `has_complaint` (Binary: 1 if customer recorded complaint, 0 otherwise)
- **Validation Scheme**: 75% Train (750 customers) / 25% Stratified Unseen Test (250 customers)

| Metric | Measured Value | Business Interpretation |
|---|---|---|
| **Accuracy** | **73.2%** | High baseline correctness on held-out test data |
| **Precision** | **50.0%** | When flag is raised, 1 in 2 customers has a verified complaint |
| **Recall** | **97.0%** | Captures 65 out of 67 actual at-risk complaint customers |
| **F1-Score** | **0.6599** | Robust harmonic mean balancing precision and recall |
| **ROC-AUC** | **0.8866** | Outstanding discrimination between complaint and non-complaint profiles |

**Top Predictive Features**:
1. `service_request_count` (frequency of support interactions)
2. `days_since_last_tx` (customer inactivity / recency)
3. `region_North` (geographic risk exposure)
4. `mobile_usage` (digital engagement level)
5. `tx_total_amount` (transaction value volume)

---

## 📑 Excel Workbook Architecture (`Bank_Customer_Analysis.xlsx`)

The workbook contains **8 dedicated sheets**:
1. `Summary_Dashboard`: KPI Cards, Total Customers, Top Channel, Declining Account, Complaint Hotspot, and 4 embedded visual charts.
2. `Cleaned_Data`: Master Customer 360 table (1,000 customers × 19 attributes) with formatted currency and numbers.
3. `Statistical_Summary`: Built with actual dynamic formulas (`=COUNT()`, `=COUNTA()`, `=SUM()`, `=AVERAGE()`, `=MEDIAN()`, `=MIN()`, `=MAX()`, `=STDEV.S()`, `=COUNTIF()`).
4. `Channel_Analysis`: Channel totals, customer averages, percentage distributions, and age band cross-tabulations.
5. `Account_Activity`: Monthly transaction activity by account type tracking the Current account decline.
6. `Complaint_Analysis`: Regional breakdown, customer counts, complaint rates (`=COUNTIF()`), and operational risk ratings.
7. `Balance_Analysis`: Segment deposit volume, mean and median balances, and deposit share (`=SUMIF()`, `=AVERAGEIF()`).
8. `Service_Requests`: Request category volume, unique customers, and calculated repeat request friction metrics.

