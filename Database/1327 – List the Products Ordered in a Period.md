# 🛒 LeetCode 1327 – List the Products Ordered in a Period

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:  

**Orders**

| Column Name | Type |
|------------|------|
| order_id   | int   |
| product_id | int   |
| unit       | int   |
| order_date | date  |

**Products**

| Column Name | Type |
|------------|------|
| product_id  | int  |
| product_name| varchar |

---

## 📝 Task

List all products **ordered between `2020-02-01` and `2020-02-29`** with:

- `product_name`  
- Total `unit` sold  

Only include products with **total units ≥ 100**. Order by product name implicitly via grouping.

---

## 🧩 Approach

1. **Join** `Orders` and `Products` on `product_id`  
2. Filter by **order date** for February 2020  
3. **Group by** `product_name`  
4. **Aggregate** total units with `SUM(O.UNIT)`  
5. Use `HAVING` to filter products with **≥100 units**

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT P.PRODUCT_NAME, SUM(O.UNIT) AS UNIT 
FROM ORDERS O 
JOIN PRODUCTS P
ON P.PRODUCT_ID = O.PRODUCT_ID
WHERE O.ORDER_DATE >= '2020-02-01' 
  AND O.ORDER_DATE <= '2020-02-29'
GROUP BY P.PRODUCT_NAME
HAVING SUM(O.UNIT) >= 100;
