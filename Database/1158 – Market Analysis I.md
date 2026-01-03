# 🛒 LeetCode 1158 – Market Analysis I

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Users**

| Column Name | Type |
|------------|------|
| user_id    | int  |
| join_date  | date |

Table: **Orders**

| Column Name | Type |
|------------|------|
| order_id   | int  |
| buyer_id   | int  |
| order_date | date |

---

## 📝 Task

For each user, report:
- `buyer_id`
- `join_date`
- Number of orders the user made in **2019**

If a user did not make any orders in 2019, return `0`.

---

## 🧩 Approach

- Use a **LEFT OUTER JOIN** to keep all users
- Count orders placed in the year **2019**
- Use `NVL` to replace `NULL` values with `0`
- Format dates using `TO_CHAR`

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT U.USER_ID AS BUYER_ID, TO_CHAR(U.JOIN_DATE,'YYYY-MM-DD') AS JOIN_DATE, NVL(T.ORDERS_IN_2019, 0) AS ORDERS_IN_2019
FROM USERS U LEFT OUTER JOIN 
(SELECT U.USER_ID AS USER_ID, COUNT(O.ORDER_ID) AS ORDERS_IN_2019
FROM USERS U JOIN ORDERS O
ON U.USER_ID = O.BUYER_ID
AND TO_CHAR(O.ORDER_DATE) LIKE '%2019%'
GROUP BY U.USER_ID) T
ON T.USER_ID = U.USER_ID;
