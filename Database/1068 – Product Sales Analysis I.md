# 📦 LeetCode 1068 – Product Sales Analysis I

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables: **Product**, **Sales**

### Product
| Column Name   | Type |
|--------------|------|
| product_id   | int  |
| product_name | varchar |

### Sales
| Column Name | Type |
|------------|------|
| sale_id    | int  |
| product_id | int  |
| year       | int  |
| quantity   | int  |
| price      | int  |

---

## 📝 Task

Write a SQL query to report the **product_name**, **year**, and **price** for each sale.

---

## 🧩 Approach

- Join `Product` and `Sales` tables using `product_id`
- Select required columns from both tables

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT P.PRODUCT_NAME,S.YEAR,S.PRICE FROM PRODUCT P, SALES S WHERE P.PRODUCT_ID = S.PRODUCT_ID;
