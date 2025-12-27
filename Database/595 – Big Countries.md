# 🌍 LeetCode 595 – Big Countries

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **World**

| Column Name | Type |
|-------------|------|
| name        | varchar |
| continent   | varchar |
| area        | int |
| population  | int |
| gdp         | bigint |

`name` is the primary key of this table.

---

## 📝 Task

A country is considered **big** if:
- It has an **area ≥ 3,000,000 km²**, **OR**
- It has a **population ≥ 25,000,000**

Write a SQL query to output the **name, population, and area** of all **big countries**.

---

## 🧩 Approach

- Filter rows using a simple `OR` condition
- Check both **area** and **population** thresholds
- Return only the required columns

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT NAME,POPULATION,AREA FROM WORLD WHERE AREA>=3000000 OR POPULATION>=25000000;
