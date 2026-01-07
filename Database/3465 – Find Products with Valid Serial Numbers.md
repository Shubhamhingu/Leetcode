# 🧾 LeetCode 3465 – Find Products with Valid Serial Numbers

**Difficulty:** Easy  
**Category:** SQL / String Matching  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Products**

| Column Name | Type    |
|------------|---------|
| product_id | int     |
| description | varchar |

Each product has a textual description that may include a serial number.

---

### 📝 Task

Find all products whose **description contains a valid serial number**.

A **valid serial number**:
- Starts with `SN`
- Follows the format: `SNxxxx-xxxx`
- Each `x` is an **alphanumeric character**
- The serial number may appear:
  - At the beginning
  - In the middle
  - At the end of the description
- Must be separated by spaces (if not at the beginning or end)

---

## 🧩 Approach

- Use `LIKE` with wildcards to detect valid serial number patterns
- Handle different positions of the serial number in the description:
  - Middle
  - Beginning
  - End
- `_` is used to match exactly one character

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT * FROM
PRODUCTS
WHERE DESCRIPTION LIKE '% SN____-____ %'
OR DESCRIPTION LIKE '%SN____-____ %'
OR DESCRIPTION LIKE '% SN____-____';
