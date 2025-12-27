# 🔺 LeetCode 610 – Triangle Judgement

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Triangle**

| Column Name | Type |
|------------|------|
| x          | int |
| y          | int |
| z          | int |

Each row represents the lengths of three line segments.

---

## 📝 Task

Write a SQL query to determine whether the three given sides can form a **valid triangle**.

Return `'Yes'` if they can form a triangle, otherwise return `'No'`.

---

## 🧩 Approach

- Use the **triangle inequality theorem**
- The sum of any two sides must be greater than the third side
- Use a `CASE` expression to evaluate the condition

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT X,Y,Z,
CASE WHEN (X + Y) > Z AND (Y + Z) > X AND (X + Z) > Y THEN 'Yes'
ELSE 'No' 
END AS triangle 
FROM TRIANGLE;
