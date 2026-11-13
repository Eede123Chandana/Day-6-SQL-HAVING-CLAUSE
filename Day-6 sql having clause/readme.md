# 📊 SQL HAVING Clause | Filtering Aggregated Data

## 🎯 Overview

The SQL `HAVING` clause filters aggregated results based on specified conditions.

It is commonly used with `GROUP BY` and aggregate functions to analyze summarized business data.

**Objective:** Understand HAVING, its differences from WHERE, SQL logical execution order, and practical business applications.

---

## 1️⃣ What is the HAVING Clause?

`HAVING` filters groups or aggregate results based on specified conditions.

It helps analysts identify categories, stores, customers, or regions that meet business performance thresholds.

### Basic Syntax

```sql
SELECT column_name,
       AGG_FUNCTION(column_name)
FROM table_name
GROUP BY column_name
HAVING AGG_FUNCTION(column_name) > value;
```

---

## 2️⃣ Sample Dataset

**Table: orders**

| Category | Sales |
|---|---:|
| Electronics | 70000 |
| Electronics | 50000 |
| Clothing | 40000 |
| Clothing | 32000 |
| Grocery | 28000 |
| Grocery | 20000 |

### Grouped Sales Summary

```sql
SELECT
    category,
    SUM(sales) AS total_sales
FROM orders
GROUP BY category;
```

**Output:**

| Category | Total Sales |
|---|---:|
| Electronics | 120000 |
| Clothing | 72000 |
| Grocery | 48000 |

---

## 3️⃣ HAVING with GROUP BY

### Business Question

Which product categories generated more than ₹50,000?

```sql
SELECT
    category,
    SUM(sales) AS total_sales
FROM orders
GROUP BY category
HAVING SUM(sales) > 50000;
```

**Output:**

| Category | Total Sales |
|---|---:|
| Electronics | 120000 |
| Clothing | 72000 |

**Explanation:**

- GROUP BY creates category-wise groups.
- SUM() calculates total sales.
- HAVING filters totals above ₹50,000.
- Grocery is excluded because its total is ₹48,000.

---

## 4️⃣ WHERE vs HAVING

| WHERE | HAVING |
|---|---|
| Filters individual rows | Filters grouped/aggregated results |
| Applied before grouping | Applied after grouping |
| Cannot directly filter aggregate calculations | Supports aggregate conditions |
| Used for row-level conditions | Used for group-level conditions |

### WHERE Example

```sql
SELECT *
FROM orders
WHERE sales > 30000;
```

Returns individual transactions exceeding ₹30,000.

### HAVING Example

```sql
SELECT
    category,
    SUM(sales) AS revenue
FROM orders
GROUP BY category
HAVING SUM(sales) > 50000;
```

Returns categories exceeding ₹50,000 in total revenue.

---

## 5️⃣ HAVING with Aggregate Functions

### SUM() – Total Sales

```sql
SELECT
    category,
    SUM(sales) AS total_sales
FROM orders
GROUP BY category
HAVING SUM(sales) > 50000;
```

### COUNT() – Transaction Volume

```sql
SELECT
    category,
    COUNT(*) AS transaction_count
FROM orders
GROUP BY category
HAVING COUNT(*) >= 2;
```

### AVG() – Average Sales

```sql
SELECT
    category,
    AVG(sales) AS avg_sales
FROM orders
GROUP BY category
HAVING AVG(sales) > 30000;
```

### MIN() – Minimum Transaction

```sql
SELECT
    category,
    MIN(sales) AS min_sale
FROM orders
GROUP BY category
HAVING MIN(sales) > 25000;
```

### MAX() – Maximum Transaction

```sql
SELECT
    category,
    MAX(sales) AS max_sale
FROM orders
GROUP BY category
HAVING MAX(sales) > 50000;
```

---

## 6️⃣ SQL Logical Execution Order

SQL queries are logically evaluated in the following sequence:

**FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY**

| Stage | Purpose |
|---|---|
| FROM | Identifies the source data |
| WHERE | Filters individual records |
| GROUP BY | Organizes records into groups |
| HAVING | Filters grouped results |
| SELECT | Determines output columns |
| ORDER BY | Sorts the final output |

### Example

```sql
SELECT
    category,
    SUM(sales) AS revenue
FROM orders
WHERE sales > 20000
GROUP BY category
HAVING SUM(sales) > 50000
ORDER BY revenue DESC;
```

**Explanation:**

1. FROM retrieves the orders table.
2. WHERE selects transactions above ₹20,000.
3. GROUP BY creates category-wise groups.
4. HAVING retains groups above ₹50,000.
5. SELECT produces the requested columns.
6. ORDER BY sorts revenue in descending order.

*Note: This is the logical processing order. Database engines may optimize physical execution differently.*

---

## 7️⃣ Real-World Business Applications

### 🛒 Retail – High-Revenue Categories

```sql
SELECT
    category,
    SUM(sales) AS revenue
FROM orders
GROUP BY category
HAVING SUM(sales) > 50000;
```

**Purpose:** Identify profitable product categories by revenue.

### 🏬 Store Performance

```sql
SELECT
    store_id,
    SUM(sales) AS total_revenue
FROM orders
GROUP BY store_id
HAVING SUM(sales) > 100000;
```

**Purpose:** Identify stores exceeding revenue targets.

### 💳 Transaction Analysis

```sql
SELECT
    customer_id,
    COUNT(*) AS total_transactions
FROM orders
GROUP BY customer_id
HAVING COUNT(*) >= 5;
```

**Purpose:** Identify customers with frequent transactions.

### 📈 Business Performance

```sql
SELECT
    region,
    AVG(sales) AS avg_sales
FROM orders
GROUP BY region
HAVING AVG(sales) > 25000;
```

**Purpose:** Identify regions with strong average sales.

*These business examples assume the relevant columns exist in the orders table.*

---

## 8️⃣ Important Interview Questions

**Q1. What is HAVING?**

HAVING filters groups or aggregated results based on conditions.

**Q2. WHERE vs HAVING?**

WHERE filters rows before grouping; HAVING filters groups after aggregation.

**Q3. Can HAVING be used without GROUP BY?**

Yes. SQL can treat the entire result set as one aggregate group.

```sql
SELECT COUNT(*) AS total_orders
FROM orders
HAVING COUNT(*) > 5;
```

**Q4. Can HAVING use multiple conditions?**

Yes, using AND and OR.

```sql
SELECT category,
       SUM(sales) AS revenue,
       COUNT(*) AS total_orders
FROM orders
GROUP BY category
HAVING SUM(sales) > 50000
   AND COUNT(*) >= 2;
```

**Q5. Can WHERE use SUM() directly?**

No. Aggregate conditions belong in HAVING or an outer query.

---

## 🎯 Key Takeaways

✅ HAVING filters aggregate results.

✅ WHERE filters individual records.

✅ GROUP BY organizes data into groups.

✅ SUM(), COUNT(), AVG(), MIN(), and MAX() work with HAVING.

✅ HAVING supports multiple aggregate conditions.

✅ HAVING can be used without GROUP BY.

✅ Logical execution order helps explain query behavior.

✅ HAVING supports KPI analysis and business reporting.

---

## 💡 Final Thoughts

**The HAVING clause helps analysts move beyond individual transactions and focus on meaningful business summaries.**

Combining GROUP BY, aggregate functions, WHERE, and HAVING enables more effective SQL reporting and data-driven decision-making.

### 🏷️ Topics

`SQL` `HAVING` `WHERE` `GROUP BY` `Aggregation` `SUM` `COUNT` `AVG` `MIN` `MAX` `Data Analytics` `Business Analytics` `MySQL`
