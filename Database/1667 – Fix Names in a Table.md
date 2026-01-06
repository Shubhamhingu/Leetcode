# 🧠 LeetCode 1667 – Fix Names in a Table

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Users**

| Column Name | Type    |
|------------|---------|
| user_id    | int     |
| name       | varchar |

- `user_id` is the primary key.
- The `name` column may contain names in **inconsistent casing**.

---

### 📝 Task

Write a SQL query to **fix the capitalization** of names such that:

- The **first character** of the name is **uppercase**
- The **remaining characters** are **lowercase**
- Return results ordered by `user_id`

---

## 🧩 Approach

- Use `SUBSTR` to separate the first character from the rest of the name.
- Apply `UPPER()` to the first character.
- Apply `LOWER()` to the remaining substring.
- Concatenate both parts to form the corrected name.
- Sort the output by `user_id`.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
Select user_id, UPPER(SUBSTR(NAME,1,1))||LOWER(SUBSTR(NAME,2,LENGTH(NAME))) AS NAME
FROM USERS ORDER BY USER_ID;
