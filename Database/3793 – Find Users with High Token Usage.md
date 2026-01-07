# 🧠 LeetCode 3793 – Find Users with High Token Usage

**Difficulty:** Medium  
**Category:** SQL / Aggregation  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **PROMPTS**

| Column Name | Type    |
|-------------|---------|
| USER_ID     | int     |
| TOKENS      | number  |
| PROMPT_TEXT | varchar |

You are asked to find users who have **high token usage**. Specifically:

1. Users who submitted **at least 3 prompts**.
2. Users whose **maximum token usage for a prompt is greater than their average token usage**.

For these users, return:

- `USER_ID`
- Number of prompts (`PROMPT_COUNT`)
- Average tokens used per prompt (`AVG_TOKENS` rounded to 2 decimals)

Order results by `AVG_TOKENS DESC` and then `USER_ID ASC`.

---

### 🧩 Approach

1. **Aggregate prompts by user** using `GROUP BY USER_ID`.
2. Compute:
   - `COUNT(*)` → number of prompts per user
   - `AVG(TOKENS)` → average token usage
   - `MAX(TOKENS)` → maximum tokens used
3. Use a `HAVING` clause to filter users:
   - `MAX(TOKENS) > AVG(TOKENS)`  
   - `COUNT(*) >= 3`
4. Sort the final output as required.

---

### 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT USER_ID, COUNT(*) AS PROMPT_COUNT, ROUND(AVG(TOKENS),2) AS AVG_TOKENS
FROM PROMPTS
GROUP BY USER_ID
HAVING MAX(TOKENS) > AVG(TOKENS) AND COUNT(*) >= 3
ORDER BY AVG_TOKENS DESC, USER_ID;
