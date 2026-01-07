# 📈 LeetCode 3580 – Find Consistently Improving Employees

**Difficulty:** Medium  
**Category:** SQL / Window Functions / Ranking  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:

**Employees**

| Column Name | Type    |
|------------|---------|
| employee_id | int     |
| name        | varchar |

**Performance_Reviews**

| Column Name | Type    |
|------------|---------|
| review_id   | int     |
| employee_id | int     |
| review_date | date    |
| rating      | int     |

- Each employee may have multiple performance reviews over time.  
- Reviews include a `RATING` and the `REVIEW_DATE`.  

---

### 📝 Task

Find employees whose **latest three reviews show consistent improvement** (i.e., each review rating is higher than the previous one).  

Return columns:

- `EMPLOYEE_ID`  
- `NAME`  
- `IMPROVEMENT_SCORE` (difference between the latest and the oldest of the last three reviews)  

Order by `IMPROVEMENT_SCORE` descending, then by `NAME`.

---

## 🧩 Approach

1. **Rank reviews** per employee by `REVIEW_DATE` descending using `RANK() OVER`.  
2. Separate the **top three reviews** into three CTEs: `FIRSTRANK`, `SECONDRANK`, `THIRDRANK`.  
3. Join these CTEs with `EMPLOYEES` to get employee names.  
4. Filter employees where `FR.RATING > SR.RATING > TR.RATING`.  
5. Calculate `IMPROVEMENT_SCORE = FR.RATING - TR.RATING`.  
6. Order results by improvement descending and name ascending.

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS (
    SELECT
        RANK() OVER (PARTITION BY EMPLOYEE_ID ORDER BY REVIEW_DATE DESC) AS RANKING,
        EMPLOYEE_ID,
        REVIEW_DATE,
        RATING
    FROM 
    PERFORMANCE_REVIEWS
), FIRSTRANK AS (
    SELECT * FROM TEMPTABLE
    WHERE RANKING = 1
), SECONDRANK AS (
    SELECT * FROM TEMPTABLE
    WHERE RANKING = 2
), THIRDRANK AS (
    SELECT * FROM TEMPTABLE
    WHERE RANKING = 3
)
SELECT E.EMPLOYEE_ID, E.NAME, FR.RATING - TR.RATING AS IMPROVEMENT_SCORE
FROM FIRSTRANK FR JOIN SECONDRANK SR ON FR.EMPLOYEE_ID = SR.EMPLOYEE_ID
JOIN THIRDRANK TR ON FR.EMPLOYEE_ID = TR.EMPLOYEE_ID
JOIN EMPLOYEES E ON E.EMPLOYEE_ID = FR.EMPLOYEE_ID
WHERE FR.RATING > SR.RATING AND SR.RATING > TR.RATING
ORDER BY IMPROVEMENT_SCORE DESC, NAME;
