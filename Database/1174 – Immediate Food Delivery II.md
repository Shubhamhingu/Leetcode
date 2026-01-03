# 🍔 LeetCode 1174 – Immediate Food Delivery II

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Delivery**

| Column Name                   | Type |
|------------------------------|------|
| delivery_id                  | int  |
| customer_id                  | int  |
| order_date                   | date |
| customer_pref_delivery_date  | date |

Each row represents a food delivery order placed by a customer.

---

## 📝 Task

Calculate the **percentage of customers** whose **first order** was delivered **immediately**.

👉 An order is considered **immediate** if:
- `order_date = customer_pref_delivery_date`

Return the percentage rounded to **2 decimal places**.

---

## 🧩 Approach

1. Identify the **first order for each customer** using `ROW_NUMBER()`
2. Check whether that first order was **immediate**
3. Convert immediate deliveries into `1`, others into `0`
4. Compute the percentage using:
