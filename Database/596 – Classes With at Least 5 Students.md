# 🎓 LeetCode 596 – Classes With at Least 5 Students

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Courses**

| Column Name | Type |
|-------------|------|
| student     | varchar |
| class       | varchar |

There is **no primary key** for this table.  
Each row indicates that a student is enrolled in a class.

---

## 📝 Task

Write a SQL query to find all **classes** that have **at least 5 students**.

---

## 🧩 Approach

- Group records by `class`
- Count the number of students per class
- Filter groups using the `HAVING` clause

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT CLASS FROM COURSES GROUP BY CLASS HAVING COUNT(CLASS) >= 5;
