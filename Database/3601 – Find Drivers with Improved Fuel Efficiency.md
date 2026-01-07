# 🧪 LeetCode 3601 – Find Drivers with Improved Fuel Efficiency

**Difficulty:** Medium  
**Category:** SQL / CTEs / Aggregation  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:

**Drivers**

| Column Name | Type    |
|------------|---------|
| driver_id   | int     |
| driver_name | varchar |

**Trips**

| Column Name    | Type    |
|---------------|---------|
| trip_id       | int     |
| driver_id     | int     |
| trip_date     | date    |
| distance_km   | number  |
| fuel_consumed | number  |

- Each driver may have multiple trips over a year.  
- Fuel efficiency per trip = `distance_km / fuel_consumed`.  

---

### 📝 Task

For each driver:

1. Calculate the **average fuel efficiency** for the **first half** of the year (Jan–Jun).  
2. Calculate the **average fuel efficiency** for the **second half** of the year (Jul–Dec).  
3. Return only drivers whose **second half average > first half average**.  
4. Return columns:

- `DRIVER_ID`  
- `DRIVER_NAME`  
- `FIRST_HALF_AVG`  
- `SECOND_HALF_AVG`  
- `EFFICIENCY_IMPROVEMENT = SECOND_HALF_AVG - FIRST_HALF_AVG`  

Order by `EFFICIENCY_IMPROVEMENT` descending, then `DRIVER_NAME`.

---

## 🧩 Approach

1. Use a CTE `MAINTABLE` to compute per-trip fuel efficiency.  
2. Use two CTEs `FIRSTHALF` and `SECONDHALF` to compute average efficiency per driver for each half of the year.  
3. Join with the `DRIVERS` table.  
4. Filter to include only drivers with improved efficiency.  
5. Round results to 2 decimal places for readability.

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH MAINTABLE AS (
    SELECT TRIP_ID, DRIVER_ID, TRIP_DATE, DISTANCE_KM/FUEL_CONSUMED AS AVERAGE
    FROM TRIPS
), FIRSTHALF AS (
    SELECT DRIVER_ID, AVG(AVERAGE) AS FIRST_HALF_AVG
    FROM MAINTABLE
    WHERE EXTRACT(MONTH FROM TRIP_DATE) <= 6
    GROUP BY DRIVER_ID
), SECONDHALF AS (
    SELECT DRIVER_ID, AVG(AVERAGE) AS SECOND_HALF_AVG
    FROM MAINTABLE
    WHERE EXTRACT(MONTH FROM TRIP_DATE) >= 7
    GROUP BY DRIVER_ID
)
SELECT D.DRIVER_ID, D.DRIVER_NAME, ROUND(F.FIRST_HALF_AVG,2) AS FIRST_HALF_AVG, 
       ROUND(S.SECOND_HALF_AVG,2) AS SECOND_HALF_AVG,
       ROUND(S.SECOND_HALF_AVG - F.FIRST_HALF_AVG,2) AS EFFICIENCY_IMPROVEMENT
FROM DRIVERS D 
JOIN FIRSTHALF F ON F.DRIVER_ID = D.DRIVER_ID 
JOIN SECONDHALF S ON S.DRIVER_ID = D.DRIVER_ID
WHERE S.SECOND_HALF_AVG - F.FIRST_HALF_AVG > 0
ORDER BY EFFICIENCY_IMPROVEMENT DESC, DRIVER_NAME;
