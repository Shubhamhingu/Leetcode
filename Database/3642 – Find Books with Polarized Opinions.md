# 🧪 LeetCode 3642 – Find Books with Polarized Opinions

**Difficulty:** Hard  
**Category:** SQL / Aggregation / CTE  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:

**Books**

| Column Name | Type    |
|-------------|---------|
| book_id     | int     |
| title       | varchar |
| author      | varchar |

**Reading_Sessions**

| Column Name     | Type    |
|-----------------|---------|
| session_id      | int     |
| book_id         | int     |
| session_rating  | int     |

- Each book can have multiple reading sessions with ratings.  
- A book is considered **polarized** if:
  1. It has ratings both **≥ 4** and **≤ 2**.  
  2. It has **at least 5 sessions**.  
  3. The **polarization score** ≥ 0.6, where:  
     \[
     \text{polarization\_score} = \frac{\#\text{high ratings (≥4)} + \#\text{low ratings (≤2)}}{\text{total sessions}}
     \]  
- Also calculate **rating spread** = `MAX(session_rating) - MIN(session_rating)`.

---

### 📝 Task

For each book:

1. Compute `polarization_score` and `rating_spread`.  
2. Filter books with `polarization_score >= 0.6`.  
3. Return book details along with `polarization_score` and `rating_spread`.  
4. Order by `polarization_score DESC` and `title DESC`.

---

## 🧩 Approach

1. Use a **CTE** to calculate for each book:
   - Count of high ratings (≥4)
   - Count of low ratings (≤2)
   - Total number of sessions  
   - `polarization_score` and `rating_spread`.
2. Filter books with the required number of sessions and rating conditions in the `HAVING` clause.  
3. Join CTE with `BOOKS` to retrieve book details.  
4. Filter books with `polarization_score >= 0.6`.  
5. Sort results as per requirements.

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS (
    SELECT BOOK_ID, 
           (SUM(CASE WHEN SESSION_RATING >= 4 THEN 1 ELSE 0 END) +
            SUM(CASE WHEN SESSION_RATING <= 2 THEN 1 ELSE 0 END)
           )/COUNT(*) AS polarization_SCORE,
           MAX(SESSION_RATING) - MIN(SESSION_RATING) AS RATING_SPREAD
    FROM READING_SESSIONS
    GROUP BY BOOK_ID
    HAVING MAX(SESSION_RATING) >= 4 AND MIN(SESSION_RATING) <= 2 AND COUNT(*) >= 5
)
SELECT B.*, 
       T.RATING_SPREAD, 
       ROUND(T.polarization_SCORE,2) AS polarization_SCORE
FROM BOOKS B 
JOIN TEMPTABLE T ON B.BOOK_ID = T.BOOK_ID
WHERE T.polarization_SCORE >= 0.6
ORDER BY T.polarization_SCORE DESC, B.TITLE DESC;
