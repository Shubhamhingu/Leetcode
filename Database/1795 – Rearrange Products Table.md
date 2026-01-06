# 🧠 LeetCode 1795 – Rearrange Products Table

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Products**

| Column Name | Type |
|------------|------|
| product_id | int  |
| store1     | int  |
| store2     | int  |
| store3     | int  |

- Each row represents a product and its price at different stores.

---

### 📝 Task

Write a SQL query to **reformat the table** so that each row represents:

- `product_id`
- `store` name (`store1`, `store2`, `store3`)
- `price` at that store

This is essentially converting **columns into rows**.

---

## 🧩 Approach

- Use the **UNPIVOT** operator to turn multiple store columns into rows.
- Map each store column to a single `store` field and its corresponding `price`.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT PRODUCT_ID, STORE, PRICE
FROM PRODUCTS
UNPIVOT (
    PRICE FOR STORE IN (STORE1 AS 'store1',
    STORE2 AS 'store2',
    STORE3 AS 'store3')
);
