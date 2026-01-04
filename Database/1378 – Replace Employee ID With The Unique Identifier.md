# 🆔 LeetCode 1378 – Replace Employee ID With The Unique Identifier

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:  

**Employees**

| Column Name | Type |
|------------|------|
| id         | int   |
| name       | varchar |

**EmployeeUni**

| Column Name | Type |
|------------|------|
| id         | int   |
| unique_id  | varchar |

---

## 📝 Task

For each employee, return:

- `unique_id` from `EmployeeUni` if it exists, otherwise `NULL`  
- `name` of the employee  

Order the results by `name`.

---

## 🧩 Approach

1. Use a **LEFT JOIN** to include all employees  
2. Match `Employees.ID` with `EmployeeUni.ID`  
3. Use `NVL(EU.UNIQUE_ID, NULL)` to handle missing unique IDs  
4. Order the output by employee `NAME`

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT NVL(EU.UNIQUE_ID,NULL) AS UNIQUE_ID, E.NAME
FROM EMPLOYEES E 
LEFT JOIN EMPLOYEEUNI EU
ON E.ID = EU.ID
ORDER BY E.NAME;
