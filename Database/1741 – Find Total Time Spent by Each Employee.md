# 🧠 LeetCode 1741 – Find Total Time Spent by Each Employee

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Employees**

| Column Name | Type |
|------------|------|
| emp_id     | int  |
| event_day  | date |
| in_time    | int  |
| out_time   | int  |

- Each row represents an employee’s working session on a given day.
- `in_time` and `out_time` are measured in minutes.

---

### 📝 Task

Write a SQL query to calculate the **total time spent by each employee per day**.

- Total time = sum of `(out_time - in_time)`
- Format the date as `YYYY-MM-DD`

---

## 🧩 Approach

- Group records by `emp_id` and `event_day`.
- Calculate session duration using `out_time - in_time`.
- Sum durations per employee per day.
- Format the date using `TO_CHAR`.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT TO_CHAR(EVENT_DAY,'YYYY-MM-DD') AS "DAY",
EMP_ID,
SUM(OUT_TIME - IN_TIME) AS TOTAL_TIME 
FROM EMPLOYEES
GROUP BY EVENT_DAY,EMP_ID;
