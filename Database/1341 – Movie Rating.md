# 🎬 LeetCode 1341 – Movie Rating

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:  

**MovieRating**

| Column Name | Type |
|------------|------|
| movie_id   | int   |
| user_id    | int   |
| rating     | number |
| created_at | date  |

**Users**

| Column Name | Type |
|------------|------|
| user_id    | int   |
| name       | varchar |

**Movies**

| Column Name | Type |
|------------|------|
| movie_id   | int   |
| title      | varchar |

---

## 📝 Task

Return:

1. **User who rated the most movies** (alphabetically if tie)  
2. **Movie with highest average rating** in **February 2020** (alphabetically if tie)  

---

## 🧩 Approach

1. Count movies rated per user using `COUNT(*)` and group by `USER_ID`  
2. Sort by `CNT DESC, NAME` and pick the first row (`ROWNUM = 1`)  
3. Compute average rating per movie within **Feb 2020**  
4. Select movie(s) with the **highest average rating**  
5. Use `UNION ALL` to combine both results  

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT MIN(U.NAME) AS RESULTS
FROM (
    SELECT U.USER_ID, U.NAME, COUNT(*) AS CNT
    FROM MOVIERATING MR 
    JOIN USERS U
    ON U.USER_ID = MR.USER_ID
    GROUP BY U.USER_ID,U.NAME
    ORDER BY CNT DESC, U.NAME
) T 
JOIN USERS U
ON T.USER_ID = U.USER_ID
WHERE ROWNUM = 1
UNION ALL
SELECT MIN(M.TITLE) 
FROM MOVIES M 
JOIN (
    SELECT MOVIE_ID, AVG(RATING) AS RATE 
    FROM MOVIERATING
    WHERE CREATED_AT BETWEEN TO_DATE('01/02/2020','DD-MM-YYYY') 
                          AND TO_DATE('29/02/2020','DD-MM-YYYY')
    GROUP BY MOVIE_ID
    HAVING AVG(RATING) = (
        SELECT MAX(RATE) 
        FROM (
            SELECT MOVIE_ID, AVG(RATING) AS RATE 
            FROM MOVIERATING
            WHERE CREATED_AT BETWEEN TO_DATE('01/02/2020','DD-MM-YYYY') 
                                  AND TO_DATE('29/02/2020','DD-MM-YYYY')
            GROUP BY MOVIE_ID
        )
    )
) T3
ON M.MOVIE_ID = T3.MOVIE_ID;
