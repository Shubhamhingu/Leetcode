# 🧠 LeetCode 1729 – Find Followers Count

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Followers**

| Column Name | Type |
|------------|------|
| user_id    | int  |
| follower_id| int  |

- Each row indicates that `follower_id` follows `user_id`.

---

### 📝 Task

Write a SQL query to report the **number of followers for each user**.

- Return results ordered by `user_id`.

---

## 🧩 Approach

- Group records by `user_id`.
- Use `COUNT(*)` to count how many followers each user has.
- Sort the output by `user_id`.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT USER_ID, COUNT(*) AS FOLLOWERS_COUNT
FROM FOLLOWERS
GROUP BY USER_ID
ORDER BY USER_ID;
