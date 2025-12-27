# 🧠 LeetCode 584 – Find Customer Referee

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Customer**

| Column Name | Type |
|------------|------|
| id         | int  |
| name       | varchar |
| referee_id | int |

`id` is the primary key for this table.

---

### 📝 Task

Write a SQL query to report the **names of customers** who are **not referred by customer with id = 2**.

Return the result table in **any order**.

---

## 🧩 Approach

- Filter out customers where `referee_id = 2`.
- Include customers where `referee_id` is **NULL**.
- Explicitly handling `NULL` values ensures correct results.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT NAME FROM CUSTOMER
WHERE REFEREE_ID != 2 OR REFEREE_ID IS NULL;
