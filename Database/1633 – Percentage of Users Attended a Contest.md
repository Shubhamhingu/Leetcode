# 🧠 LeetCode 1633 – Percentage of Users Attended a Contest

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Users**

| Column Name | Type |
|------------|------|
| user_id    | int  |
| user_name  | varchar |

`user_id` is the primary key for this table.

---

Table: **Register**

| Column Name | Type |
|------------|------|
| contest_id | int  |
| user_id    | int  |

Each row indicates that a user registered for a contest.

---

### 📝 Task

Write a SQL query to find the **percentage of users** who registered for each contest.  
Round the percentage to **2 decimal places**.

Return the result ordered by:
1. `percentage` in **descending order**
2. `contest_id` in **ascending order**

---

## 🧩 Approach

- Count the number of users registered per contest.
- Divide by the total number of users.
- Multiply by 100 and round to 2 decimal places.
- Group results by `contest_id` and sort as required.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT CONTEST_ID, ROUND(COUNT(*)*100/(SELECT COUNT(*) FROM USERS),2) AS PERCENTAGE
FROM REGISTER
GROUP BY CONTEST_ID
ORDER BY PERCENTAGE DESC, CONTEST_ID;
