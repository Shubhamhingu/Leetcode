# 👨‍💼 LeetCode 1075 – Project Employees I

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Project**

| Column Name | Type |
|------------|------|
| project_id | int  |
| employee_id | int |

Table: **Employee**

| Column Name | Type |
|------------|------|
| employee_id | int |
| name | varchar |
| experience_years | int |

Each row of `Project` indicates that an employee is working on a project.

---

## 📝 Task

Write a SQL query to report the **average experience years** of employees for **each project**, rounded to **2 decimal places**.

---

## 🧩 Approach

- Join the `Project` and `Employee` tables using `employee_id`
- Group results by `project_id`
- Compute the average experience using `AVG`
- Round the result to 2 decimal places

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT P.PROJECT_ID, ROUND(AVG(E.EXPERIENCE_YEARS),2) AS AVERAGE_YEARS 
FROM PROJECT P, EMPLOYEE E 
WHERE P.EMPLOYEE_ID = E.EMPLOYEE_ID 
GROUP BY P.PROJECT_ID;
