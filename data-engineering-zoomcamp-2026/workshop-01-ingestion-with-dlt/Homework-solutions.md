# DLT Trips Dataset – Homework Answers

## Question 1: What are the start and end dates of the dataset?

- 2009-01-01 to 2009-01-31  
- 2009-06-01 to 2009-07-01  
- 2024-01-01 to 2024-02-01  
- 2024-06-01 to 2024-07-01  

---

### ✅ Answer to Question 1

**2009-06-01 to 2009-07-01**

### Explanation

To identify the dataset’s time coverage, we check the earliest and latest values in the pickup and dropoff timestamp columns.

#### Using the DLT Dashboard

Execute a query to retrieve the minimum and maximum dates:

```sql
-- Q1 Validation Query
SELECT
    MIN(trip_pickup_date_time)::DATE AS first_pickup_date,
    MAX(trip_pickup_date_time)::DATE AS last_pickup_date,
    MIN(trip_dropoff_date_time)::DATE AS first_dropoff_date,
    MAX(trip_dropoff_date_time)::DATE AS last_dropoff_date
FROM "trips";
```

<img width="1165" height="368" alt="image" src="https://github.com/user-attachments/assets/611b7559-fec8-4273-a7ab-10eadd596e95" />

The result confirms that the dataset ranges from **June 1, 2009** to **July 1, 2009**.

#### Using the DLT MCP Server

You can also ask:

> "What is the start date and end date of the trips dataset?"

<img width="577" height="210" alt="image" src="https://github.com/user-attachments/assets/e1ea752f-6c39-4a56-bbb8-5ab95aa6f680" />

Both methods confirm the same date interval.

---

## Question 2: What percentage of trips were paid using a credit card?

- 16.66%  
- 26.66%  
- 36.66%  
- 46.66%  

---

### ✅ Answer to Question 2

**26.66%**

### Explanation

To determine the share of trips paid by credit card, we calculate the percentage of each `payment_type` relative to the total number of trips.

#### Using the DLT Dashboard

```sql
-- Q2 Validation Query
SELECT
    payment_type,
    COUNT(*) AS trip_count,
    ROUND(COUNT(*) * 100.0 / SUM(COUNT(*)) OVER (), 2) AS percentage
FROM "trips"
GROUP BY payment_type
ORDER BY trip_count DESC;
```

<img width="1143" height="580" alt="image" src="https://github.com/user-attachments/assets/3e45bd7e-d58b-422a-9b4b-19f848278c44" />

The calculation shows that **26.66%** of all trips were paid using a credit card.

#### Using the DLT MCP Server

You may also ask:

> "What proportion of trips are paid with credit card in trips dataset?"

<img width="742" height="237" alt="image" src="https://github.com/user-attachments/assets/0761b67f-605c-4769-9d9e-63381c849c16" />

The result matches the dashboard calculation.

---

## Question 3: What is the total amount of money generated from tips?

- $4,063.41  
- $6,063.41  
- $8,063.41  
- $10,063.41  

---

### ✅ Answer to Question 3

**$6,063.41**

### Explanation

To compute the total tips collected, we sum the `tip_amt` column across all trips.

#### Using the DLT Dashboard

```sql
-- Q3 Validation Query
SELECT
    payment_type,
    ROUND(SUM(tip_amt), 2) AS total_tips
FROM "trips"
GROUP BY payment_type
ORDER BY total_tips DESC;
```

<img width="1053" height="640" alt="image" src="https://github.com/user-attachments/assets/e0e28cdc-417f-423c-a602-42dd6b6be6b3" />

Since tips are typically associated with credit card payments, that category shows the highest value.

The final total tip revenue is **$6,063.41**.

#### Using the DLT MCP Server

You can also ask:

> "What is the total amount of money generated in tips for this trips dataset?"

<img width="745" height="101" alt="image" src="https://github.com/user-attachments/assets/b1df2526-b5c7-4f65-9c4f-73e40f514b3a" />

The result confirms the same total amount.

---
