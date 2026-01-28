# SQL Queries Documentation

This document contains a set of SQL queries used to answer analytical questions based on the `green_trip` and `zones` tables.

---

## Question 3  
**Count the number of trips with a distance less than or equal to 1 mile within a specific date range**

```sql
SELECT COUNT(*)
FROM green_trip
WHERE lpep_pickup_datetime BETWEEN '2025-11-01' AND '2025-12-01'
  AND trip_distance <= 1;
```

## Question 4

```sql
SELECT 
    lpep_pickup_datetime AS pickup_day,
    MAX(trip_distance) AS max_distance
FROM green_trip
WHERE trip_distance < 100
GROUP BY pickup_day
ORDER BY max_distance DESC
LIMIT 1;
```

## Question 5

```sql
SELECT 
    z."Zone" AS pickup_zone,
    SUM(t.total_amount) AS total_sum
FROM green_trip t
JOIN zones z 
    ON t."PULocationID" = z."LocationID"
WHERE CAST(t.lpep_pickup_datetime AS DATE) = '2025-11-18'
GROUP BY z."Zone"
ORDER BY total_sum DESC
LIMIT 1;
```

## Question 6

```sql
SELECT
    z_do.Zone AS dropoff_zone,
    MAX(t.tip_amount) AS max_tip
FROM green_trip t
JOIN zones z_pu
    ON t.PULocationID = z_pu.LocationID
JOIN zones z_do
    ON t.DOLocationID = z_do.LocationID
WHERE z_pu.Zone = 'East Harlem North'
  AND t.lpep_pickup_datetime >= '2025-11-01'
  AND t.lpep_pickup_datetime <  '2025-12-01'
GROUP BY z_do.Zone
ORDER BY max_tip DESC
LIMIT 1
```




