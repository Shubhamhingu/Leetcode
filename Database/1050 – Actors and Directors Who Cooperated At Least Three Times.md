# 🎭 LeetCode 1050 – Actors and Directors Who Cooperated At Least Three Times

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **ActorDirector**

| Column Name  | Type |
|-------------|------|
| actor_id    | int  |
| director_id | int  |
| timestamp   | int  |

Each row indicates an actor–director collaboration.

---

## 📝 Task

Write a SQL query to find all **actor_id** and **director_id** pairs that have cooperated **at least three times**.

---

## 🧩 Approach

- Group records by `actor_id` and `director_id`
- Count the number of collaborations per pair
- Filter pairs with a count of **3 or more**

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT ACTOR_ID,DIRECTOR_ID FROM 
(SELECT ACTOR_ID,DIRECTOR_ID,COUNT(*) AS CNT FROM ACTORDIRECTOR GROUP BY ACTOR_ID,DIRECTOR_ID)
WHERE CNT>=3;
