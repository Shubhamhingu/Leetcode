# 🧠 LeetCode 1587 – Bank Account Summary II

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Users**

| Column Name | Type |
|------------|------|
| account    | int  |
| name       | varchar |

`account` is the primary key for this table.

---

Table: **Transactions**

| Column Name | Type |
|------------|------|
| trans_id   | int  |
| account    | int  |
| amount     | int  |
| transacted_on | date |

`trans_id` is the primary key for this table.

---

### 📝 Task

Write a SQL query to report the **name** and **balance** of users whose account balance is **greater than 10000**.

The account balance is calculated as the **sum of all transaction amounts** for each account.

---

## 🧩 Approach

- Aggregate transactions by `account` to compute the total balance.
- Join the aggregated result with the `Users` table.
- Filter accounts where the balance is greater than `10000`.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT U.NAME,T.BALANCE
FROM USERS U JOIN 
(SELECT ACCOUNT,SUM(AMOUNT) AS BALANCE
FROM TRANSACTIONS
GROUP BY ACCOUNT) T
ON U.ACCOUNT = T.ACCOUNT
WHERE T.BALANCE > 10000;
