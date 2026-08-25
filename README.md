# Customer Segmentation & RFM Analysis

An end-to-end customer segmentation project using Python, pandas, and RFM analysis to turn more than one million raw retail transaction rows into actionable customer groups for retention and marketing decisions.

## Business Objective

The goal of this project is to move beyond aggregate sales reporting and answer practical customer questions: Who are the most valuable customers? Which valuable customers have become inactive? Which segments contribute disproportionately to spending? Where should retention resources be prioritized?

## Key Results

- Cleaned **1,067,371 raw transaction rows** into **805,549 usable positive-purchase rows** for customer-level RFM analysis.
- Built RFM profiles for **5,878 unique customers** across **36,969 completed orders**.
- Identified **Champions** as only **12.2% of customers** while accounting for **54.6% of historical completed-purchase spending**.
- Found **589 high-value At-Risk customers** with approximately **$1.99 million in historical completed-purchase spending**.
- Found that **Hibernating customers** represent **21.9% of customers** but only **3.6% of historical completed-purchase spending**, supporting lower-cost reactivation strategies for that group.

## Visual Findings

### Customer share vs. spending contribution

![Customer share vs. spending contribution](images/segment_spending_share.png)

### Inactivity by customer segment

![Average days since last purchase by segment](images/segment_recency.png)

### Highest-value At-Risk customers

![Top high-value at-risk customers](images/top_at_risk_customers.png)

## Methodology

1. Loaded the two Online Retail II worksheets and inspected structure, data types, and missing values.
2. Converted Customer ID to an identifier-friendly string type and quantified missing-ID records.
3. Created line-level transaction value as `Quantity × Price`.
4. Investigated cancellations, negative quantities, zero/non-positive prices, and unidentified transaction rows.
5. Built a clean RFM transaction base containing identifiable, non-cancelled purchases with positive quantity and price.
6. Calculated customer-level **Recency**, **Frequency**, and **Monetary** metrics.
7. Scored Recency and Monetary using quartiles. Frequency used behavior-based cut points because 27.6% of customers had exactly one order, making a naive quartile split inappropriate.
8. Assigned customers to business-friendly lifecycle segments and analyzed segment size, activity, and spending contribution.
9. Developed segment-specific retention and marketing recommendations.

## RFM Segment Logic

- **Champions:** very recent, highly frequent customers.
- **Loyal Customers:** recent customers with consistent repeat purchasing.
- **Potential Loyalists:** very recent customers beginning to repeat.
- **New Customers:** very recent customers with one completed order.
- **Promising:** relatively recent customers with limited purchase frequency.
- **At Risk:** historically frequent customers who have not purchased recently.
- **Needs Attention:** lower-frequency customers showing declining engagement.
- **Hibernating:** infrequent customers with long periods of inactivity.

## Business Recommendations

Prioritize protection of Champions, continued development of Loyal Customers, and targeted win-back efforts for historically valuable At-Risk customers. Use lower-cost automated reactivation for Hibernating customers rather than applying the same retention investment across every segment.

## Limitations

- Records without Customer IDs cannot support customer-level RFM analysis and were excluded.
- Cancelled invoices, negative quantities, and non-positive prices were excluded. Monetary therefore represents **gross completed-purchase value**, not net customer value after returns.
- RFM describes historical behavior; it does not predict future churn, purchases, or revenue.
- Segment definitions are rule-based and dataset-specific.
- No demographic, acquisition-channel, or campaign-response data is available in the source dataset.

## Data Source

**Online Retail II**, UCI Machine Learning Repository. The dataset contains transactions from a UK-based non-store retailer from December 2009 through December 2011.

- Source: https://archive.ics.uci.edu/dataset/502/online%2Bretail%2Bii
- Citation: Chen, D. (2012). *Online Retail II* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5CG6D
- License: CC BY 4.0

The 43.5 MB workbook is not included in this repository. Download `online_retail_II.xlsx` from UCI and place it in the repository root before running the notebook.

## Repository Structure

```text
customer-rfm-analysis/
├── Customer_RFM_Analysis.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── images/
    ├── segment_spending_share.png
    ├── segment_recency.png
    └── top_at_risk_customers.png
```

## Run Locally

```bash
pip install -r requirements.txt
jupyter notebook
```

Then open `Customer_RFM_Analysis.ipynb` after placing `online_retail_II.xlsx` in the repository root.

## Tools

Python · pandas · Matplotlib · Jupyter Notebook
