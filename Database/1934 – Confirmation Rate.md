# 🧠 LeetCode 1934 – Confirmation Rate

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Signups**

| Column Name | Type |
|------------|------|
| user_id    | int  |
| time_stamp | date |

---

Table: **Confirmations**

| Column Name | Type |
|------------|------|
| user_id    | int  |
| time_stamp | date |
| action     | varchar |

- Each user may have multiple confirmation records.
- `action` can be `'confirmed'` or `'timeout'`.

---

### 📝 Task

Write a SQL query to calculate the **confirmation rate** for each user:

- Confirmation rate =  
  `confirmed actions / total confirmation requests`
- Round the result to **2 decimal places**
- Include users with **no confirmation records** (rate = 0)

---

## 🧩 Approach

- Convert confirmation actions into numeric values using a `CASE` statement:
  - `'confirmed'` → 1
  - others → 0
- Calculate the average confirmation value per user.
- Left join with the `Signups` table to include all users.
- Use `NVL` to handle users without confirmations.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT S.USER_ID, ROUND(NVL(T.ACT,0),2) AS confirmation_rate FROM SIGNUPS S LEFT OUTER JOIN
(SELECT USER_ID, AVG(ACTION) ACT FROM
(SELECT USER_ID, CASE
WHEN ACTION = 'confirmed' THEN 1
ELSE 0
END AS ACTION
FROM CONFIRMATIONS)
GROUP BY USER_ID) T
ON S.USER_ID = T.USER_ID;
