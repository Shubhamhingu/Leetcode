# 👥 LeetCode 627 – Swap Sex of Employees

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Salary**

| Column Name | Type |
|------------|------|
| id         | int  |
| name       | varchar |
| sex        | char |
| salary     | int |

`id` is the primary key.  

---

## 📝 Task

Write a SQL query to **swap the sex** of all employees:
- `'m'` should become `'f'`
- `'f'` should become `'m'`

---

## 🧩 Approach

- Use an `UPDATE` statement
- Use a `CASE` expression to switch `'m'` to `'f'` and `'f'` to `'m'`
- Apply the change to the entire table

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
update salary set sex=case
when sex='m' Then 'f' 
when sex='f' Then 'm' 
end;
