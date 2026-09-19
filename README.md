# ApexPlanet Data Analytics Internship -- Task 3

## Deep-Dive Analysis & Interactive Dashboarding
**Live Dashboard:** https://datastudio.google.com/reporting/fd06b1ec-f192-498f-9423-3b9bbade9e6b

### Intern

**Shaikh Maria Islam**

### Internship

**ApexPlanet Software Pvt. Ltd. -- Data Analytics Internship**

------------------------------------------------------------------------

## 1. Project Overview

Task 3 focuses on performing a deep-dive business analysis and
developing an interactive dashboard to support data-driven
decision-making.

Building on the cleaned dataset and exploratory analysis completed in
Tasks 1 and 2, this task focuses on defining core KPIs, performing
customer segmentation, analyzing revenue contribution, and creating an
interactive Power BI dashboard.

The selected deep-dive area is **Customer Segmentation using Business
Rules**.

------------------------------------------------------------------------

## 2. Objectives

1.  Define 3--5 core business KPIs.
2.  Perform a deep-dive analysis of customer purchasing behavior.
3.  Segment customers based on total spending.
4.  Identify the contribution of each customer segment to overall
    revenue.
5.  Build an interactive Power BI dashboard.
6.  Provide business insights based on the analysis.

------------------------------------------------------------------------

## 3. Dataset

The analysis uses the cleaned and feature-engineered dataset prepared
during Task 1.

-   **Rows:** 1,000
-   **Columns:** 18 in the original cleaned dataset
-   **Unique Customers:** 947

Important columns include `Order_ID`, `Order_Date`, `Customer_ID`,
`Age`, `Gender`, `City`, `Product`, `Category`, `Quantity`,
`Unit_Price`, `Total_Sales`, `Order_Year`, `Order_Month`,
`Order_Quarter`, and `Age_Group`.

A new column, **`Customer_Segment`**, was added for Task 3.

------------------------------------------------------------------------

## 4. Tools Used

-   Python
-   Pandas
-   Google Colab
-   Microsoft Power BI
-   GitHub

Python was used for customer-level aggregation and segmentation. Power
BI was used to create the interactive dashboard.

------------------------------------------------------------------------

# 5. Step 1 -- Core KPIs

## KPI 1 -- Total Revenue

**Formula:** `Total Revenue = SUM(Total_Sales)`

**Result:** **₹139,399,439.65**

**Business rationale:** Measures the overall revenue generated from the
transaction records.

## KPI 2 -- Total Transactions

**Formula:** `Total Transactions = COUNTROWS(Data)`

**Result:** **1,000**

**Business rationale:** Represents the total number of transaction
records available for analysis.

## KPI 3 -- Average Transaction Value

**Formula:**
`Average Transaction Value = Total Revenue / Total Transactions`

**Result:** **₹139,399.44**

**Business rationale:** Shows the average revenue generated per
transaction record.

## KPI 4 -- Total Units Sold

**Formula:** `Total Units Sold = SUM(Quantity)`

**Result:** **5,435 units**

**Business rationale:** Measures the total number of product units sold.

## KPI 5 -- Total Customers

**Formula:** `Total Customers = DISTINCTCOUNT(Customer_ID)`

**Result:** **947 customers**

**Business rationale:** Measures the number of unique customers
represented in the dataset.

------------------------------------------------------------------------

# 6. Step 2 -- Deep-Dive Analysis

## Selected Business Area: Customer Segmentation

Customer segmentation was selected because customer spending behavior
can be used to identify different levels of customer value.

For each customer, the following metrics were calculated:

-   Total Spend
-   Total Quantity
-   Purchase Count

The customer-level dataset contains **947 unique customers**.

------------------------------------------------------------------------

# 7. Customer-Level Analysis

Customer-level data was created by grouping transactions using
`Customer_ID`.

``` python
customer_analysis = df.groupby("Customer_ID").agg(
    Total_Spend=("Total_Sales", "sum"),
    Total_Quantity=("Quantity", "sum"),
    Purchase_Count=("Order_ID", "count")
).reset_index()
```

------------------------------------------------------------------------

# 8. Customer Spending Distribution

  Statistic               Total Spend
  --------------------- -------------
  Number of Customers             947
  Mean                    ₹147,201.10
  Minimum                     ₹437.34
  25th Percentile          ₹47,859.02
  Median                  ₹112,029.57
  75th Percentile         ₹214,435.46
  Maximum                 ₹867,333.24

These spending statistics were used to create data-driven customer
segments.

------------------------------------------------------------------------

# 9. Customer Segmentation Method

A quartile-based business rule was used to divide customers into four
spending segments based on `Total_Spend`.

  Customer Segment   Spending Rule
  ------------------ ----------------------------------
  Low Value          ≤ ₹47,859.02
  Medium Value       \> ₹47,859.02 and ≤ ₹112,029.57
  High Value         \> ₹112,029.57 and ≤ ₹214,435.46
  Top Value          \> ₹214,435.46

------------------------------------------------------------------------

# 10. Customer Segment Results

  Segment          Customers          Revenue   Average Spend   Units
  -------------- ----------- ---------------- --------------- -------
  Low Value              237    ₹5,627,896.89      ₹23,746.40     763
  Medium Value           237   ₹19,319,065.69      ₹81,515.05   1,114
  High Value             236   ₹37,403,551.78     ₹158,489.63   1,476
  Top Value              237   ₹77,048,925.29     ₹325,100.95   2,082

The segment revenue totals equal the overall customer revenue of
**₹139,399,439.65**.

------------------------------------------------------------------------

# 11. Revenue Contribution by Segment

  Segment          Revenue Share
  -------------- ---------------
  Low Value                4.04%
  Medium Value            13.86%
  High Value              26.83%
  Top Value               55.27%

### Key Finding

**Top Value customers generate 55.27% of total customer revenue.**

Although the four segments contain approximately one-quarter of the
customers each, their contributions to revenue are substantially
different.

------------------------------------------------------------------------

# 12. Average Spending Comparison

-   **Top Value average spend:** ₹325,100.95
-   **Low Value average spend:** ₹23,746.40

The results show a substantial difference in average spending between
the customer segments.

------------------------------------------------------------------------

# 13. Purchase Frequency Observation

    Purchase Count   Number of Customers
  ---------------- ---------------------
                 1                   895
                 2                    51
                 3                     1

Most customers have one recorded purchase in the dataset. Therefore,
total spending was used as the primary segmentation dimension rather
than relying heavily on repeat-purchase behavior.

------------------------------------------------------------------------

# 14. Step 3 -- Interactive Power BI Dashboard

An interactive dashboard was created using **Microsoft Power BI**.

### Dashboard components

**KPI Cards** - Total Revenue - Total Transactions - Average Transaction
Value - Total Units Sold - Total Customers

**Visualizations** - Revenue by Customer Segment - Customer Count by
Customer Segment - Monthly Revenue Trend from January to December

**Interactive Slicers** - Customer Segment - Category - City - Product -
Gender

The slicers were tested to confirm that the dashboard visuals respond to
user selections.

------------------------------------------------------------------------

# 15. Dashboard Data Preparation

The customer segment was merged back into the cleaned transaction
dataset.

The resulting Task 3 dashboard dataset contains:

-   **1,000 rows**
-   **19 columns**
-   **0 missing Customer_Segment values**

The generated file is:

`task3_dashboard_data.csv`

------------------------------------------------------------------------

# 16. Key Business Findings

### Finding 1 -- Top Value customers contribute the largest share of revenue

Top Value customers account for **55.27% of total customer revenue**.

### Finding 2 -- Customer value varies substantially

Average spending ranges from **₹23,746.40** for Low Value customers to
**₹325,100.95** for Top Value customers.

### Finding 3 -- Revenue contribution is uneven

The segments contain approximately similar numbers of customers, but
their revenue contributions differ considerably.

### Finding 4 -- Repeat purchasing is limited in the available dataset

Out of 947 customers:

-   895 have one recorded purchase
-   51 have two recorded purchases
-   1 has three recorded purchases

------------------------------------------------------------------------

# 17. Business Interpretation

The segmentation provides a way to distinguish customers according to
their contribution to revenue.

The results can support future analysis such as:

-   Identifying high-value customer groups
-   Monitoring changes in customer segment contribution
-   Comparing product and category preferences across segments
-   Examining geographic differences between segments
-   Designing targeted customer strategies
-   Tracking segment performance over time

These interpretations are based on the observed transaction and customer
spending data.

------------------------------------------------------------------------

# 18. Project Workflow

``` text
Cleaned Dataset
       ↓
Core KPI Definition
       ↓
Customer-Level Aggregation
       ↓
Customer Spending Analysis
       ↓
Quartile-Based Segmentation
       ↓
Segment Revenue Analysis
       ↓
Dashboard Data Preparation
       ↓
Power BI Dashboard
       ↓
Interactive Filtering
       ↓
Business Insights
```

------------------------------------------------------------------------

# 19. Project Files

``` text
ApexPlanet-Data-Analytics-Task3/
│
├── README.md
├── task3_dashboard_data.csv
└── ApexPlanet_Task3_Dashboard.pbix
```

------------------------------------------------------------------------

# 20. Conclusion

Task 3 extends the work completed in Tasks 1 and 2 by moving from
exploratory analysis to a customer-focused deep-dive analysis.

A quartile-based customer segmentation approach was used to classify
customers into Low Value, Medium Value, High Value, and Top Value
groups.

The analysis found that the Top Value segment contributes **55.27% of
total customer revenue**, with an average spend of **₹325,100.95**.

An interactive Power BI dashboard was developed to present the core
KPIs, customer segmentation analysis, and monthly revenue trend.

The dashboard also provides interactive filtering by customer segment,
category, city, product, and gender.

------------------------------------------------------------------------

## 21. Technologies

**Programming:** Python\
**Library:** Pandas\
**Analysis Environment:** Google Colab\
**Dashboard:** Microsoft Power BI\
**Version Control:** GitHub

------------------------------------------------------------------------

## 22. Author

**Shaikh Maria Islam**

Computer Science Undergraduate

**ApexPlanet Data Analytics Internship -- Task 3**
