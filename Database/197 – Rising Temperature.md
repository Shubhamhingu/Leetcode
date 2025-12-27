# 🧠 LeetCode 197 – Rising Temperature

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Weather**

| Column Name | Type |
|------------|------|
| id         | int  |
| recordDate | date |
| temperature | int |

`id` is the primary key for this table.  
There are no duplicate `recordDate` values.

---

### 📝 Task

Write a SQL query to find the **IDs of dates** where the temperature was **higher than the previous day**.

Return the result table in **any order**.

---

## 🧩 Approach

- Use a **self-join** on the `Weather` table.
- Join records where:
  - `W2.recordDate` is exactly **one day after** `W1.recordDate`.
- Compare temperatures:
  - Select rows where today’s temperature is **greater than yesterday’s**.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT W2.ID
FROM WEATHER W1 JOIN WEATHER W2
ON W1.RECORDDATE = W2.RECORDDATE - 1
WHERE W2.TEMPERATURE > W1.TEMPERATURE;
