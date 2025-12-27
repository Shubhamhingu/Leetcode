# 🧠 LeetCode 585 – Investments in 2016

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Insurance**

| Column Name | Type |
|------------|------|
| pid        | int  |
| tiv_2015   | float |
| tiv_2016   | float |
| lat        | float |
| lon        | float |

`pid` is the primary key for this table.

---

### 📝 Task

Write a SQL query to report the **sum of all `tiv_2016` values**, rounded to **2 decimal places**, for policies that satisfy:

1. The policy’s `tiv_2015` value appears **more than once**
2. The policy’s `(lat, lon)` location is **unique**

---

## 🧩 Approach

- Identify policies with **unique locations** using `(lat, lon)` grouping.
- Identify `tiv_2015` values that are **repeated across multiple policies**.
- Join these two result sets to filter only valid policies.
- Sum the corresponding `tiv_2016` values.
- Use `ROUND()` to format the final result.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
WITH UNIQUELOCATIONS AS (
    SELECT pid, tiv_2015, tiv_2016
    FROM Insurance
    WHERE (lat, lon) IN (
        SELECT lat, lon
        FROM Insurance
        GROUP BY lat, lon
        HAVING COUNT(*) = 1
    )
), TIVSREPEATED AS (
    SELECT TIV_2015
    FROM INSURANCE
    GROUP BY TIV_2015
    HAVING COUNT(*) > 1
)
SELECT ROUND(SUM(TIV_2016), 2) AS TIV_2016
FROM TIVSREPEATED T JOIN UNIQUELOCATIONS U
ON U.TIV_2015 = T.TIV_2015;
