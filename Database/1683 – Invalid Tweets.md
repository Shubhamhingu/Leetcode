# 🧠 LeetCode 1683 – Invalid Tweets

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Tweets**

| Column Name | Type    |
|------------|---------|
| tweet_id   | int     |
| content    | varchar |

- `tweet_id` is the primary key.
- Each row represents a tweet.

---

### 📝 Task

Write a SQL query to find the **IDs of invalid tweets**.

A tweet is considered **invalid** if:
- The length of `content` is **greater than 15 characters**

---

## 🧩 Approach

- Use the `LENGTH()` function to calculate the number of characters in the tweet.
- Filter rows where the length exceeds 15.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT TWEET_ID
FROM TWEETS
WHERE LENGTH(CONTENT) > 15;
