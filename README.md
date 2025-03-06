# Fraud-Detection
Developed an SQL query using a recursive CTE to track money flow across multiple accounts, enabling the identification of indirect fund transfers.
# Detecting Recursive Fraudulent Transactions  

## Overview  
This project contains an **SQL query using a recursive CTE** to track money laundering patterns. It identifies **suspicious money transfers** across multiple accounts over successive steps and flags potential **fraudulent transactions**.  

## Features  
- **Recursive CTE for Transaction Tracing** – Tracks money movement through multiple accounts.  
- **Fraud Detection Algorithm** – Identifies transaction chains linked to fraudulent activity.  
- **Pattern Recognition** – Follows transaction flows to highlight money laundering risks.  
- **Efficient Querying** – Optimized SQL approach for detecting recursive fraud patterns.  

## Technologies Used  
- SQL  
- Recursive Common Table Expressions (CTE)  
- Fraud Detection Techniques  

## How It Works  
1. **Recursive CTE** – Traces money transfers across multiple accounts.  
2. **Pattern Matching** – Identifies suspicious transaction chains.  
3. **Fraudulent Flagging** – Filters chains where all transactions are marked as fraudulent.  

## SQL Query Example  
```sql
WITH RecursiveCTE AS (
    SELECT sender_account, receiver_account, transaction_id, amount, 1 AS level
    FROM transactions
    WHERE is_fraudulent = 1 

    UNION ALL

    SELECT t.sender_account, t.receiver_account, t.transaction_id, t.amount, c.level + 1
    FROM transactions t
    INNER JOIN RecursiveCTE c 
    ON t.sender_account = c.receiver_account
    WHERE t.is_fraudulent = 1 
)
SELECT * FROM RecursiveCTE;
