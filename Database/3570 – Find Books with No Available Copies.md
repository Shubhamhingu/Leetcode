# 📚 LeetCode 3570 – Find Books with No Available Copies

**Difficulty:** Medium  
**Category:** SQL / Aggregation / Join  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:

**Library_Books**

| Column Name      | Type    |
|-----------------|---------|
| book_id          | int     |
| title            | varchar |
| author           | varchar |
| genre            | varchar |
| publication_year | int     |
| total_copies     | int     |

**Borrowing_Records**

| Column Name | Type    |
|------------|---------|
| record_id   | int     |
| book_id     | int     |
| user_id     | int     |
| borrow_date | date    |
| return_date | date    |

- Each book has a `total_copies` count.  
- A book may be borrowed multiple times.  
- `return_date` is NULL if the book is currently borrowed.

---

### 📝 Task

Find all books for which **all copies are currently borrowed**:

1. Count how many copies of each book are currently borrowed.  
2. Compare with `total_copies`.  
3. Return book details along with current borrowers count.  

Return columns:

- `BOOK_ID`  
- `TITLE`  
- `AUTHOR`  
- `GENRE`  
- `PUBLICATION_YEAR`  
- `CURRENT_BORROWERS`  

Sort by `CURRENT_BORROWERS` descending and `TITLE` ascending.

---

## 🧩 Approach

1. Use a **CTE** (`TEMPTABLE`) to count currently borrowed copies per book (`RETURN_DATE IS NULL`).  
2. Join `Library_Books` with this CTE on `BOOK_ID`.  
3. Filter books where `CURRENT_BORROWERS = TOTAL_COPIES`.  
4. Order results as required.

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS(
    SELECT BOOK_ID, COUNT(BOOK_ID) AS CURRENT_BORROWERS
    FROM BORROWING_RECORDS BR
    WHERE RETURN_DATE IS NULL
    GROUP BY BOOK_ID
)
SELECT L.BOOK_ID, L.TITLE, L.AUTHOR, L.GENRE, L.PUBLICATION_YEAR, T.CURRENT_BORROWERS
FROM LIBRARY_BOOKS L JOIN TEMPTABLE T
ON L.BOOK_ID = T.BOOK_ID
WHERE L.TOTAL_COPIES = T.CURRENT_BORROWERS
ORDER BY CURRENT_BORROWERS DESC, TITLE;
