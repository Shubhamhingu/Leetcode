# 🏢 LeetCode 1179 – Reformat Department Table

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Department**

| Column Name | Type |
|------------|------|
| id         | int  |
| month      | varchar |
| revenue    | int  |

---

## 📝 Task

Reformat the table to show **one row per department** with **12 columns**, each representing the revenue for a month (`Jan` through `Dec`).

- If a department has no revenue for a month, return `NULL` in that column.

---

## 🧩 Approach

- Use **conditional aggregation** with `SUM` and `IF` statements:
  - For each month, sum `revenue` if the `month` matches
- Group by department `id` to consolidate rows

---

## 🧪 SQL Solution (MySQL)

```sql
# Write your MySQL query statement below
SELECT id,
    SUM(IF(month='Jan',revenue,NULL)) AS Jan_Revenue,
    SUM(IF(month='Feb',revenue,NULL)) AS Feb_Revenue,
    SUM(IF(month='Mar',revenue,NULL)) AS Mar_Revenue,
    SUM(IF(month='Apr',revenue,NULL)) AS Apr_Revenue,
    SUM(IF(month='May',revenue,NULL)) AS May_Revenue,
    SUM(IF(month='Jun',revenue,NULL)) AS Jun_Revenue,
    SUM(IF(month='Jul',revenue,NULL)) AS Jul_Revenue,
    SUM(IF(month='Aug',revenue,NULL)) AS Aug_Revenue,
    SUM(IF(month='Sep',revenue,NULL)) AS Sep_Revenue,
    SUM(IF(month='Oct',revenue,NULL)) AS Oct_Revenue,
    SUM(IF(month='Nov',revenue,NULL)) AS Nov_Revenue,
    SUM(IF(month='Dec',revenue,NULL)) AS Dec_Revenue
FROM DEPARTMENT
GROUP BY id;
