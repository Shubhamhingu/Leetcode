# 🧠 LeetCode 1484 – Group Sold Products By The Date

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Activities**

| Column Name | Type    |
|------------|---------|
| sell_date  | date    |
| product    | varchar |

There is no primary key for this table.  
The table may contain duplicate rows.

---

### 📝 Task

Write a SQL query to find for each **sell_date**:

- The **number of distinct products sold** on that date.
- A **comma-separated list of products** sold on that date, sorted lexicographically.

The result should be ordered by `sell_date`.

---

## 🧩 Approach

- Use a subquery to select **distinct (product, sell_date)** combinations.
- Group the result by `sell_date`.
- Use `COUNT(*)` to get the number of products sold per date.
- Use `LISTAGG` with `WITHIN GROUP (ORDER BY product)` to concatenate product names in sorted order.
- Format the date using `TO_CHAR`.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT TO_CHAR(SELL_DATE,'yyyy-mm-dd') AS SELL_DATE, COUNT(*) AS num_sold, 
LISTAGG(product, ',') WITHIN GROUP (ORDER BY product) AS products
FROM (SELECT DISTINCT PRODUCT,SELL_DATE FROM ACTIVITIES)
GROUP BY SELL_DATE;
