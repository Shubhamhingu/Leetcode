# 📊 LeetCode 1084 – Sales Analysis III

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Sales**

| Column Name | Type |
|------------|------|
| sale_id | int |
| product_id | int |
| sale_date | date |
| quantity | int |
| price | int |

Table: **Product**

| Column Name | Type |
|------------|------|
| product_id | int |
| product_name | varchar |

---

## 📝 Task

Report the **product_id** and **product_name** of products that were **sold only between**
**January 1, 2019** and **March 31, 2019** (inclusive).

A product must:
- Have **at least one sale** in this period
- Have **no sales outside** this period

---

## 🧩 Approach

- Filter products with sales **inside the given date range**
- Exclude products that have **any sales before or after** the range
- Join the filtered product IDs with the `Product` table to get names

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT P.PRODUCT_ID, P.PRODUCT_NAME FROM
(
    SELECT PRODUCT_ID FROM SALES
    WHERE SALE_DATE BETWEEN TO_DATE('2019-01-01','YYYY-MM-DD')
    AND TO_DATE('2019-03-31','YYYY-MM-DD')
    AND PRODUCT_ID NOT IN (
        SELECT PRODUCT_ID FROM SALES
        WHERE SALE_DATE < TO_DATE('2019-01-01','YYYY-MM-DD')
        OR SALE_DATE > TO_DATE('2019-03-31','YYYY-MM-DD')
    )
    GROUP BY PRODUCT_ID
) T JOIN PRODUCT P
ON T.PRODUCT_ID = P.PRODUCT_ID;
