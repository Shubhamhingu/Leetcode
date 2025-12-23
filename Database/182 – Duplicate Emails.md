# 🧠 LeetCode 182 – Duplicate Emails

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Person**

| Column Name | Type |
|------------|------|
| id         | int  |
| email      | varchar |

`id` is the primary key for this table.  
Each row contains an email address. Emails will not be `NULL`.

---

### 📝 Task

Write a SQL query to report **all duplicate email addresses**.  
Return the result table in **any order**.

---

## 🧩 Approach

- Group records by the `EMAIL` column.
- Use `COUNT(*)` to determine how many times each email appears.
- Filter groups having more than one record using `HAVING`.

---

## 🧪 SQL Solution

```sql
SELECT EMAIL
FROM PERSON
GROUP BY EMAIL
HAVING COUNT(*) > 1;
