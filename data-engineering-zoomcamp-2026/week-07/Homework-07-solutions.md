## Question 1
Answer: **v25.3.9**

## Question 2
Answer: **10 Seconds **

## Question 3
Answer: **8506**
## Question 4
SQL for creating table pickup_location:

```bash
CREATE TABLE pickup_location (
    window_start TIMESTAMP(3),
    PULocationID INT,
    num_trips BIGINT,
    PRIMARY KEY (window_start, PULocationID)
)
```

SQL for reading answer:
```bash
SELECT PULocationID, num_trips
FROM pickup_location
ORDER BY num_trips DESC
LIMIT 3;
```
Answer: **74**
## Question 5
SQL for creating table pickup_location:

```bash
CREATE TABLE longest_streak (
    PULocationID INT,
    window_start TIMESTAMP(3),
    window_end TIMESTAMP(3),
    num_trips BIGINT,
    PRIMARY KEY (PULocationID, window_start, window_end)
)

```

SQL for reading answer:
```bash
SELECT *
FROM longest_streak
ORDER BY num_trips DESC
LIMIT 3;

```
Answer: **81**

## Question 6
SQL for creating table pickup_location:

```bash
SELECT *
FROM largest_tip
ORDER BY total_amount DESC
LIMIT 3;
```

SQL for reading answer:
```bash
CREATE TABLE largest_tip (
    window_start TIMESTAMP(3),
    total_amount DOUBLE PRECISION,
    PRIMARY KEY (window_start)
)
```
Answer: **2025-10-16 18:00:00**
