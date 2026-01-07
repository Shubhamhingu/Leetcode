# 🧠 LeetCode 3673 – Find Zombie Sessions

**Difficulty:** Medium  
**Category:** SQL / Analytics / CTE  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **APP_EVENTS**

| Column Name      | Type    |
|-----------------|---------|
| session_id       | int     |
| user_id          | int     |
| event_type       | varchar |
| event_timestamp  | datetime |

- `event_type` can be `'click'`, `'scroll'`, `'purchase'`, etc.  
- A **zombie session** is defined as a session that:
  1. **Does not contain any `purchase` events**.
  2. Has **more than 30 minutes duration**.
  3. Has at least **5 scroll events**.
  4. Has a **click-to-scroll ratio < 0.20**.

---

### 📝 Task

Return the `session_id`, `user_id`, `session_duration_minutes`, and `scroll_count` for all zombie sessions, ordered by `scroll_count` descending, then `session_id`.

---

### 🧩 Approach

1. Use a **CTE (`DURATION`)** to compute the total session duration in minutes for sessions with no `purchase` events:
   - `MAX(event_timestamp) - MIN(event_timestamp)` × 24 × 60 → convert to minutes.
2. Use another **CTE (`SESS`)** to compute for each session:
   - Number of scroll events (`scroll_count`).  
   - Click-to-scroll ratio (`click_ratio`) = clicks ÷ scrolls.
3. Join both CTEs on `session_id` and filter by zombie session criteria:
   - `session_duration_minutes > 30`  
   - `scroll_count >= 5`  
   - `click_ratio < 0.20`

---

### 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH DURATION AS (
    SELECT SESSION_ID, USER_ID, (MAX(EVENT_TIMESTAMP) - MIN(EVENT_TIMESTAMP)) * 24 * 60 AS SESSION_DURATION_MINUTES
    FROM APP_EVENTS
    WHERE SESSION_ID NOT IN (
        SELECT SESSION_ID FROM APP_EVENTS
        WHERE EVENT_TYPE = 'purchase'
    )
    GROUP BY SESSION_ID, USER_ID
), SESS AS (
    SELECT SESSION_ID,
           SUM(CASE WHEN EVENT_TYPE = 'scroll' THEN 1 ELSE 0 END) AS SCROLL_COUNT,
           SUM(CASE WHEN EVENT_TYPE = 'click' THEN 1 ELSE 0 END)/
           SUM(CASE WHEN EVENT_TYPE = 'scroll' THEN 1 ELSE 0 END) AS CLICK_RATIO
    FROM APP_EVENTS
    GROUP BY SESSION_ID
)
SELECT D.SESSION_ID, D.USER_ID, D.SESSION_DURATION_MINUTES, S.SCROLL_COUNT
FROM DURATION D JOIN SESS S ON D.SESSION_ID = S.SESSION_ID
WHERE S.CLICK_RATIO < 0.20 AND D.SESSION_DURATION_MINUTES > 30 AND S.SCROLL_COUNT >= 5
ORDER BY SCROLL_COUNT DESC, SESSION_ID;
