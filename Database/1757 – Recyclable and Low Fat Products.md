# 🧠 LeetCode 1757 – Recyclable and Low Fat Products

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Products**

| Column Name | Type    |
|------------|---------|
| product_id | int     |
| low_fats   | char(1) |
| recyclable | char(1) |

- `product_id` is the primary key.
- `low_fats` and `recyclable` indicate whether the product is low in fats and recyclable (`'Y'` or `'N'`).

---

### 📝 Task

Write a SQL query to find all **products** that are:

- **Low fat** (`LOW_FATS = 'Y'`)  
- **Recyclable** (`RECYCLABLE = 'Y'`)

---

## 🧩 Approach

- Use a `WHERE` clause with `AND` to filter products meeting both conditions.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT PRODUCT_ID FROM PRODUCTS WHERE LOW_FATS = 'Y' AND RECYCLABLE = 'Y';
