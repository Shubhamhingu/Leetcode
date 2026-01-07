# 🧠 LeetCode 657 – Find Loyal Customers

**Difficulty:** Medium  
**Category:** SQL / Aggregation / CTE  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Customer_Transactions**

| Column Name       | Type    |
|------------------|---------|
| customer_id       | int     |
| transaction_date  | date    |
| transaction_type  | varchar |

- `transaction_type` can be `'purchase'` or `'refund'`.  
- A **loyal customer** is defined as a customer who:
  1. Has at least **3 purchases**.
  2. Has a **refund rate** ≤ 20% (refunds ÷ purchases).
  3. Has been active for at least **30 days** between their first and last transaction.

---

### 📝 Task

Return the `customer_id` of loyal customers, sorted in ascending order.

---

### 🧩 Approach

1. Use a **CTE** to aggregate transactions per customer:
   - Count of `purchase` transactions.  
   - Count of `refund` transactions.  
   - Compute `refund_rate` = refunds ÷ purchases.  
   - Ensure customer has activity spanning **≥ 30 days** using `MAX(transaction_date) - MIN(transaction_date)`.  
2. Filter customers in the main query by:
   - `refund_rate <= 0.2`  
   - `purchase >= 3`  
3. Order results by `customer_id`.

---

### 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS(
    SELECT CUSTOMER_ID, 
           SUM(CASE WHEN TRANSACTION_TYPE = 'refund' THEN 1 ELSE 0 END) AS REFUND,
           SUM(CASE WHEN TRANSACTION_TYPE = 'purchase' THEN 1 ELSE 0 END) AS PURCHASE,
           SUM(CASE WHEN TRANSACTION_TYPE = 'refund' THEN 1 ELSE 0 END)/
           SUM(CASE WHEN TRANSACTION_TYPE = 'purchase' THEN 1 ELSE 0 END) AS REFUND_RATE
    FROM CUSTOMER_TRANSACTIONS
    HAVING MAX(TRANSACTION_DATE) - MIN(TRANSACTION_DATE) >= 30
    GROUP BY CUSTOMER_ID
)
SELECT CUSTOMER_ID 
FROM TEMPTABLE 
WHERE REFUND_RATE <= 0.2 AND PURCHASE >= 3
ORDER BY CUSTOMER_ID;
