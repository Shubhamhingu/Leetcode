# 📊 LeetCode 1211 – Queries Quality and Percentage

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Queries**

| Column Name | Type |
|------------|------|
| query_name | varchar |
| rating     | int    |
| position   | int    |

---

## 📝 Task

For each query, calculate:

1. **QUALITY** – average of `rating / position` (rounded to 2 decimals)  
2. **POOR_QUERY_PERCENTAGE** – percentage of ratings **less than 3** (rounded to 2 decimals)

Return the result grouped by `query_name`.

---

## 🧩 Approach

- Use **aggregate functions** with `GROUP BY`  
- Compute QUALITY with `AVG(RATING / POSITION)`  
- Compute POOR_QUERY_PERCENTAGE with:
