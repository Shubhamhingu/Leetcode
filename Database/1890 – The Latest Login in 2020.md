# 🧠 LeetCode 1890 – The Latest Login in 2020

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Logins**

| Column Name | Type    |
|------------|---------|
| user_id    | int     |
| time_stamp | date    |

- Each row represents a login event for a user.

---

### 📝 Task

Write a SQL query to report the **latest login timestamp** for each user in the year **2020**.

---

## 🧩 Approach

- Filter logins using `TO_CHAR(time_stamp, 'yyyy') = '2020'`.
- Group by `user_id` and use `MAX(time_stamp)` to find the latest login per user.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT USER_ID, MAX(TIME_STAMP) AS LAST_STAMP
FROM LOGINS
WHERE TO_CHAR(TIME_STAMP,'yyyy') = '2020'
GROUP BY USER_ID;
