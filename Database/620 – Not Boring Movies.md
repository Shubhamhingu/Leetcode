# 🎬 LeetCode 620 – Not Boring Movies

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Cinema**

| Column Name  | Type |
|-------------|------|
| id          | int  |
| title       | varchar |
| description | varchar |
| rating      | int |

`id` is the primary key.

---

## 📝 Task

Write a SQL query to return all movies that are **not boring** and have an **odd ID**.  
Order the results by **rating in descending order**.

---

## 🧩 Approach

- Filter movies with **odd IDs** using `MOD(ID, 2) != 0`
- Exclude movies with description `'boring'`
- Sort the resulting movies by `rating` descending

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT * FROM CINEMA
WHERE MOD(ID, 2) != 0
AND DESCRIPTION != 'boring'
ORDER BY RATING DESC;
