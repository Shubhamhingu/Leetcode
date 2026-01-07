# 🌐 LeetCode 3451 – Find Invalid IP Addresses

**Difficulty:** Hard  
**Category:** SQL / String Processing / Regex  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Logs**

| Column Name | Type    |
|------------|---------|
| ip         | varchar |

Each row contains an IP address logged by the system.

---

### 📝 Task

Identify **invalid IP addresses** and report how many times each invalid IP appears.

An IP address is considered **valid** if:
- It consists of **exactly 4 numeric segments** separated by dots (`.`)
- Each segment:
  - Is between **0 and 255**
  - Does **not start with `0`**
- The IP contains **exactly 3 dots**

Return:
- `ip`
- `invalid_count` (number of occurrences)

Order the result by:
1. `invalid_count` in descending order
2. `ip` in descending order

---

## 🧩 Approach

- Use `REGEXP_SUBSTR` to split the IP address into 4 segments
- Use `REGEXP_COUNT` to ensure exactly 3 dots
- Validate each segment:
  - Numeric range between `0` and `255`
  - No leading zero
- Exclude all **valid IPs** and keep only **invalid ones**
- Count occurrences of each IP

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH SPLITTABLE AS (
    SELECT
    IP,
    REGEXP_SUBSTR(IP, '[^.]+', 1, 1) AS col1,
    REGEXP_SUBSTR(IP, '[^.]+', 1, 2) AS col2,
    REGEXP_SUBSTR(IP, '[^.]+', 1, 3) AS col3,
    REGEXP_SUBSTR(IP, '[^.]+', 1, 4) AS col4,
    COUNT(*) AS CNT
    FROM LOGS
    GROUP BY IP
)
SELECT IP, CNT AS INVALID_COUNT
FROM SPLITTABLE
WHERE IP NOT IN(
    SELECT IP
    FROM SPLITTABLE
    WHERE SUBSTR(COL1,0,1) != '0'
    AND TO_NUMBER(COL1) BETWEEN 0 AND 255
    AND SUBSTR(COL2,0,1) != '0'
    AND TO_NUMBER(COL2) BETWEEN 0 AND 255
    AND SUBSTR(COL3,0,1) != '0'
    AND TO_NUMBER(COL3) BETWEEN 0 AND 255
    AND SUBSTR(COL4,0,1) != '0'
    AND TO_NUMBER(COL4) BETWEEN 0 AND 255
    AND REGEXP_COUNT(IP, '[.]') = 3
)
ORDER BY CNT DESC, IP DESC;
