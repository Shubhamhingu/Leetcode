# 🧪 LeetCode 3611 – Find Overbooked Employees

**Difficulty:** Medium  
**Category:** SQL / CTEs / Aggregation  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:

**Employees**

| Column Name    | Type    |
|----------------|---------|
| employee_id    | int     |
| employee_name  | varchar |
| department     | varchar |

**Meetings**

| Column Name     | Type    |
|-----------------|---------|
| meeting_id      | int     |
| employee_id     | int     |
| meeting_date    | date    |
| duration_hours  | number  |

- Each employee may attend multiple meetings per week.  
- A week is defined using ISO week (starting Monday).  
- An employee is considered **overbooked** if they have **more than 20 hours of meetings in a week**.  
- Only include employees who have **2 or more overbooked weeks**.

---

### 📝 Task

For each employee:

1. Count the number of weeks with total meeting hours > 20 (`MEETING_HEAVY_WEEKS`).  
2. Return employees with at least 2 such weeks.  
3. Return columns:

- `EMPLOYEE_ID`  
- `EMPLOYEE_NAME`  
- `DEPARTMENT`  
- `MEETING_HEAVY_WEEKS`  

Order by `MEETING_HEAVY_WEEKS` descending, then `EMPLOYEE_NAME`.

---

## 🧩 Approach

1. Use a CTE `TEMPTABLE` to calculate total meeting hours per employee per week.  
2. Filter weeks with more than 20 hours using `HAVING SUM(DURATION_HOURS) > 20`.  
3. Use another CTE `FINTEMP` to count the number of overbooked weeks per employee.  
4. Join with `EMPLOYEES` table and filter to include only employees with ≥2 heavy weeks.  
5. Order results as required.

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS (
    SELECT 
        EMPLOYEE_ID, 
        TRUNC(MEETING_DATE, 'IW') AS WEEK_START,
        SUM(DURATION_HOURS) AS TOTAL_HOURS
    FROM MEETINGS
    GROUP BY EMPLOYEE_ID, TRUNC(MEETING_DATE, 'IW')
    HAVING SUM(DURATION_HOURS) > 20
), FINTEMP AS (
    SELECT EMPLOYEE_ID,
        COUNT(EMPLOYEE_ID) AS CNT
    FROM TEMPTABLE
    GROUP BY EMPLOYEE_ID
)
SELECT 
    E.EMPLOYEE_ID,
    E.EMPLOYEE_NAME,
    E.DEPARTMENT,
    T.CNT AS MEETING_HEAVY_WEEKS
FROM FINTEMP T JOIN EMPLOYEES E
ON E.EMPLOYEE_ID = T.EMPLOYEE_ID
WHERE T.CNT >= 2
ORDER BY MEETING_HEAVY_WEEKS DESC, EMPLOYEE_NAME;
