# OTT Customer Churn Analysis (SQL + Python)

A end-to-end churn analysis for an OTT streaming service: pulling multi-table data from SQLite, cleaning and engineering features in pandas, visualizing patterns, and turning the findings into business recommendations.

> **Note:** The dataset is a small sample (21 customers) used to demonstrate the workflow. Findings are patterns worth testing on larger data, not statistically proven drivers.

---

## 1. Business Challenge

In the competitive OTT market (Netflix, Hotstar, Prime), retention is critical. As a Data Analyst, the goal is to identify high-risk subscribers using customer demographics, subscription tiers, and support escalations, and to recommend actions that reduce churn.

## 2. Tech Stack

- **SQL and Python:** sqlite3, pandas, numpy
- **Visualization:** matplotlib, seaborn
- **Skills:** data cleaning, feature engineering, analytics, writing actionable insights

## 3. Project Milestones

- [x] **Relational data extraction:** connect Python to SQLite and load 3 tables (customer, subscription, support)
- [x] **Data cleaning:** fix data types, missing values, and inconsistent categories (e.g. gender labels, country)
- [x] **Feature engineering:** churn flag, tenure, churn risk bands (low / medium / high), complaint counts
- [x] **Analysis:** churn rate, retention, ARPU, revenue at risk, escalation rate, churn by segment
- [x] **Visualization:** churn trend, churn by plan and state, correlation heatmap
- [x] **Executive reporting:** summary and recommendations (below)
- [ ] Customer aging (age from date of birth) and churn by age group

## 4. Project Structure

```
customer-churn-analysis/
├── README.md
├── requirements.txt
├── churn_analysis.ipynb        # full analysis
└── data/
    ├── customer_churn.db       # source SQLite database
    └── Exported_churn_data.csv # cleaned, merged dataset
```

## 5. Executive Summary

**Headline:** 6 of 21 customers churned (**28.6% churn, 71.4% retention**), removing about **18.7% of monthly recurring revenue**. Average revenue per user is roughly 18.85.

### Key insights

1. **Complaints are the strongest churn signal.** 6 of 7 customers who contacted support churned (86%); none of the 14 who never complained did. All cancellations came after the complaint date, so a complaint looks like an early warning.
2. **Escalated complaints always ended in churn.** All 4 escalated customers churned. Churned customers averaged a CSAT of about 34 versus 90 for retained customers.
3. **Referral customers are the leakiest channel.** 5 of 6 referral customers churned (83%), versus 0 of 9 organic and 1 of 6 paid.
4. **Monthly contracts churn far more than annual.** 56% (5 of 9) versus 8% (1 of 12). By plan: Basic 60%, Standard 22%, Premium 14%.
5. **Churn is concentrated in low-value customers.** Churned customers pay about 12.32 per month versus 21.46 for retained ones, with much lower CLTV.
6. **Reasons for leaving are spread out:** switched to competitor (2), and price, content, streaming quality, forgotten trial (1 each).
7. **Churn scores line up with outcomes.** Churned customers averaged a score of 86 versus 26 for retained customers.

### Recommendations

- **Trigger a save workflow on every complaint**, with priority handling and follow-up on escalations.
- **Review referral quality** and check whether the referral offer attracts price-sensitive customers.
- **Push monthly customers toward annual plans** with a discount.
- **Improve the Basic plan**, where content and streaming quality complaints concentrate.

### Data caveats

- Small sample (21 rows), so segment percentages are directional only.
- One customer's monthly charge (92.99) looks like an outlier or typo and inflates revenue and ARPU.
- Plan type, contract type, and acquisition channel overlap, so their effects cannot be separated with this sample.
- Only the latest complaint per customer is kept after de-duplication.

## 6. How to Run

```bash
pip install -r requirements.txt
jupyter notebook churn_analysis.ipynb
```

The notebook reads `data/customer_churn.db` and writes the cleaned dataset to `data/Exported_churn_data.csv`.

## 7. Applicability

The same workflow (extract, clean, engineer features, segment, recommend) applies to churn problems in SaaS, e-commerce, fintech, and adtech.
