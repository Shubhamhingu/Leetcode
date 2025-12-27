# 🧠 LeetCode 586 – Customer Placing the Largest Number of Orders

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Orders**

| Column Name      | Type |
|------------------|------|
| order_number     | int  |
| customer_number  | int  |

`order_number` is the primary key for this table.

---

## 📝 Task

Write a SQL query to find the **customer_number** who has placed the **largest number of orders**.

> If multiple customers have the same highest number of orders, return **any one** of them.

---

## 🧩 Approach

- Group records by `customer_number`
- Count the total orders per customer
- Sort customers by order count in **descending order**
- Use `ROWNUM = 1` to fetch the top customer (Oracle / PL-SQL)

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMP AS (
    SELECT CUSTOMER_NUMBER, COUNT(ORDER_NUMBER) AS CNT
    FROM ORDERS
    GROUP BY CUSTOMER_NUMBER
    ORDER BY CNT DESC
)
SELECT CUSTOMER_NUMBER
FROM TEMP
WHERE ROWNUM = 1;
