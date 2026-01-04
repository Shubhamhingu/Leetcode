# 🧠 LeetCode 1581 – Customer Who Visited but Did Not Make Any Transactions

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Visits**

| Column Name | Type |
|------------|------|
| visit_id   | int  |
| customer_id| int  |

`visit_id` is the primary key of this table.

---

Table: **Transactions**

| Column Name | Type |
|------------|------|
| transaction_id | int |
| visit_id       | int |
| amount         | int |

`transaction_id` is the primary key of this table.

---

### 📝 Task

Write a SQL query to find the **customer IDs** and the **number of visits** where the customer **did not make any transactions**.

Only include visits that have **no corresponding record** in the `Transactions` table.

---

## 🧩 Approach

- Identify visits whose `visit_id` does **not exist** in the `Transactions` table.
- Group the remaining visits by `customer_id`.
- Count the number of such visits per customer.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT CUSTOMER_ID, COUNT(*) AS COUNT_NO_TRANS FROM VISITS WHERE VISIT_ID NOT IN
(SELECT V.VISIT_ID
FROM VISITS V JOIN TRANSACTIONS T
ON V.VISIT_ID = T.VISIT_ID)
GROUP BY CUSTOMER_ID;
