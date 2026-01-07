# 🧪 LeetCode 3626 – Find Stores with Inventory Imbalance

**Difficulty:** Hard  
**Category:** SQL / CTEs / Aggregation  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:

**Stores**

| Column Name | Type    |
|-------------|---------|
| store_id    | int     |
| store_name  | varchar |

**Inventory**

| Column Name  | Type    |
|--------------|---------|
| inventory_id | int     |
| store_id     | int     |
| product_name | varchar |
| quantity     | number  |
| price        | number  |

- Each store has multiple products with varying `price` and `quantity`.  
- Only consider stores with **at least 3 products** for max and min price calculations.  
- Define `imbalance_ratio` as:  
  \[
  \text{imbalance_ratio} = \frac{\text{quantity of cheapest product}}{\text{quantity of most expensive product}}
  \]  
- Identify stores where `imbalance_ratio > 1`.

---

### 📝 Task

For each store meeting the criteria:

1. Find the **most expensive product** and **cheapest product**.  
2. Calculate `imbalance_ratio`.  
3. Return store info with `most_exp_product`, `cheapest_product`, and `imbalance_ratio`.  
4. Order by `imbalance_ratio` descending, then `store_name`.

---

## 🧩 Approach

1. Use CTE `MAXTABLE` to select **most expensive products** per store (only stores with ≥3 products).  
2. Use CTE `MINTABLE` to select **cheapest products** per store (only stores with ≥3 products).  
3. Join `MAXTABLE` and `MINTABLE` with `STORES` to compute `imbalance_ratio`.  
4. Filter stores where `imbalance_ratio > 1`.  
5. Order results by `imbalance_ratio` descending, then `store_name`.

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH MAXTABLE AS (
    SELECT I.INVENTORY_ID, I.STORE_ID, I.PRODUCT_NAME, I.QUANTITY, I.PRICE
    FROM INVENTORY I JOIN (
        SELECT STORE_ID, MAX(PRICE) AS PRICE, COUNT(*) AS CNT
        FROM INVENTORY
        GROUP BY STORE_ID
    ) MAT
    ON I.STORE_ID = MAT.STORE_ID AND I.PRICE = MAT.PRICE
    WHERE MAT.CNT >= 3
),
MINTABLE AS (
    SELECT I.INVENTORY_ID, I.STORE_ID, I.PRODUCT_NAME, I.QUANTITY, I.PRICE
    FROM INVENTORY I JOIN (
        SELECT STORE_ID, MIN(PRICE) AS PRICE, COUNT(*) AS CNT
        FROM INVENTORY
        GROUP BY STORE_ID
    ) MIT
    ON I.STORE_ID = MIT.STORE_ID AND I.PRICE = MIT.PRICE
    WHERE MIT.CNT >= 3
),
FINTAB AS (
    SELECT S.*, XT.PRODUCT_NAME AS most_exp_product, IT.PRODUCT_NAME AS cheapest_product, 
           ROUND(IT.QUANTITY/XT.QUANTITY, 2) AS imbalance_ratio
    FROM MAXTABLE XT 
    JOIN MINTABLE IT ON XT.STORE_ID = IT.STORE_ID 
    JOIN STORES S ON S.STORE_ID = XT.STORE_ID AND IT.STORE_ID = S.STORE_ID
    ORDER BY IMBALANCE_RATIO DESC, STORE_NAME
)
SELECT * FROM FINTAB WHERE IMBALANCE_RATIO > 1;
