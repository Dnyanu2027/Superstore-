# Top 10 Products — Retail Sales Analysis

## 📌 Project Overview

This project analyzes retail sales data from **2009–10** to identify the **Top 10 products by total sales**.

The project focuses not only on ranking products, but also on **data cleaning, validation, handling non-product transactions, ranking ties, and visualization**.

---

## 🎯 Objective

* Identify the Top 10 products by sales
* Practice sorting and ranking using Pandas
* Clean and validate the sales data
* Exclude non-product transactions
* Handle ranking ties correctly
* Create a clear visualization
* Export the final results to Excel

---

## 🗂️ Dataset

**Dataset:** `Retail_2009-10.csv`

The analysis starts with:

* **525,461** raw rows
* **518,596** rows after removing exact duplicates
* **504,730** valid sale lines
* **4,251** distinct stock codes initially

After removing non-product transactions, **4,231 real products** were analyzed.

---

## 🛠️ Tools & Technologies

* **Python**
* **Pandas** — data cleaning, grouping, aggregation and ranking
* **Matplotlib** — visualization
* **OpenPyXL** — Excel export
* **Jupyter Notebook**

---

## 🔄 Analysis Process

```text
Raw Data
   ↓
Remove Duplicate Rows
   ↓
Calculate Sales = Quantity × Price
   ↓
Remove Cancellations / Invalid Sales
   ↓
Identify Non-Product Transactions
   ↓
Group Sales by Product
   ↓
Rank Products
   ↓
Top 10 Products
   ↓
Visualization
   ↓
Excel Export
```

---

## 🧹 Data Cleaning

The following steps were performed:

1. Read the CSV using the appropriate encoding.
2. Treated `Invoice`, `StockCode`, and `Customer ID` as text.
3. Removed exact duplicate rows.
4. Created a `Sales` column:

```python
df["Sales"] = df["Quantity"] * df["Price"]
```

5. Kept only valid sales where:

```text
Quantity × Price > 0
```

6. Excluded cancellation invoices beginning with `C`.

---

## ⚠️ Important Data Quality Check

A key finding was that **not every `StockCode` represented an actual product**.

Examples included:

* Manual entries
* Postage
* Carriage
* Amazon fees
* Bank charges
* Discounts
* Adjustments
* Test products
* Gift vouchers

A total of **2,300 rows** representing non-product transactions were excluded, with **467,115.42** in sales value removed from the product analysis.

This step was important because otherwise non-products such as **Manual** and **Postage** could incorrectly appear in the Top 10.

---

## 📊 Top 10 Products

| Rank | Stock Code | Product                             | Total Sales |
| ---: | ---------- | ----------------------------------- | ----------: |
|    1 | 22423      | REGENCY CAKESTAND 3 TIER            |  169,912.76 |
|    2 | 85123A     | WHITE HANGING HEART T-LIGHT HOLDER  |  158,305.72 |
|    3 | 85099B     | JUMBO BAG RED RETROSPOT             |   88,976.33 |
|    4 | 84879      | ASSORTED COLOUR BIRD ORNAMENT       |   72,890.19 |
|    5 | 22086      | PAPER CHAIN KIT 50'S CHRISTMAS      |   58,127.30 |
|    6 | 47566      | PARTY BUNTING                       |   49,664.12 |
|    7 | 84347      | ROTATING SILVER ANGELS T-LIGHT HLDR |   47,954.49 |
|    8 | 21843      | RED RETROSPOT CAKE STAND            |   44,994.25 |
|    9 | 48138      | DOOR MAT UNION FLAG                 |   42,095.60 |
|   10 | 20685      | DOOR MAT RED SPOT                   |   39,762.78 |

---

## 📈 Key Results

* **4,231** real products were analyzed.
* Total sales across these products: **9,804,647.24**
* Top 10 product sales: **772,683.54**
* Top 10 products contributed approximately **7.9%** of total product sales.
* The 10th-place sales cutoff was **39,762.78**.
* There was **no tie at the Top 10 cutoff**.

---

## 📊 Visualization

A horizontal bar chart was created because product names can be long and horizontal bars make the ranking easier to read.

![Top 10 Products](output/top10_products_chart.png)

---

## 🔢 Ranking & Tie Handling

Pandas `.rank()` was used to assign product rankings.

```python
by_product["Rank"] = (
    by_product["Total_Sales"]
    .rank(method="min", ascending=False)
    .astype(int)
)
```

The `method="min"` approach means products with the same sales receive the same rank, while the following rank is skipped.

For example:

```text
Product A → Rank 1
Product B → Rank 1
Product C → Rank 3
```

---

## 📁 Project Structure

```text
Top-10-Products/
│
├── Top10_Products.ipynb
├── Retail_2009-10.csv
│
└── output/
    ├── top10_products.xlsx
    └── top10_products_chart.png
```

---

## 📤 Output Files

### Excel

`top10_products.xlsx`

Contains:

* **Top 10 Products** sheet
* **Method Notes** sheet documenting the analysis rules and exclusions

### Chart

`top10_products_chart.png`

A horizontal bar chart showing the Top 10 products by total sales.

---

## 💡 Key Learnings

### 1. Sorting vs Ranking

**Sorting** puts data in order.

**Ranking** assigns a position to each record.

### 2. Data validation matters

Before ranking products, it is important to verify that the category being ranked actually represents products.

### 3. Business definitions matter

A technically correct calculation can still produce a misleading business result if postage, fees, manual entries or other non-product transactions are included.

### 4. Document the methodology

The final output documents:

* Data used
* Sale-line definition
* Excluded codes
* Excluded sales value
* Ranking method
* Number of products analyzed

---

## 📚 Excel Method

The same analysis can also be performed in Excel using a **PivotTable**:

1. Create a `Sales` column.
2. Filter invalid/cancellation transactions.
3. Remove non-product transactions.
4. Create a PivotTable.
5. Add `StockCode` / `Description` to Rows.
6. Add `Sales` to Values using **Sum**.
7. Sort Sales from largest to smallest.
8. Apply a **Top 10 Value Filter**.
9. Create a horizontal bar chart.

---

## 🚀 Future Improvements

Possible extensions to this project:

* Analyze Top 10 products by **quantity sold**
* Compare **sales vs quantity**
* Analyze monthly product performance
* Analyze customer segments
* Identify products with declining sales
* Build an interactive **Power BI dashboard**

---

## 👩‍💻 Author

**Data Analytics Project**

Skills demonstrated:

`Python` · `Pandas` · `Matplotlib` · `Excel` · `Data Cleaning` · `Data Analysis` · `Data Visualization`
