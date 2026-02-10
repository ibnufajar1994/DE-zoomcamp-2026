## Big Query Setup

```bash
CREATE OR REPLACE EXTERNAL TABLE `dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.external_yellow_tripdata_2024`
OPTIONS (
  format = 'PARQUET',
  uris = ['gs://dtc-de-course-485117-module-1-bucket/yellow_tripdata_2024-*.parquet']
);

```


To create a (regular/materialized) table:
```bash
CREATE OR REPLACE TABLE dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata_2024_non_partitioned AS
SELECT * FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.external_yellow_tripdata_2024;

```

### Question 1

```bash
SELECT COUNT(*) FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata_2024_non_partitioned;
```
Answer: **20,332,093**

### Question 2

For External Table:
```bash
SELECT COUNT(DISTINCT PULocationID) FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.external_yellow_tripdata_2024;
```
For regular/materialized table:

```bash
SELECT COUNT(DISTINCT PULocationID)  FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata_2024_non_partitioned;
```
Answer: **0 MB for the External Table and 155.12 MB for the Materialized Table**

### Question 3
for getting PULocationIDs: 
```bash
SELECT PULocationID
FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata_2024_non_partitioned;

```

for getting PULocationIDs and DOLocationIDs:
```bash
SELECT PULocationID, DOLocationID
FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata_2024_non_partitioned;
```
Answer: **BigQuery is a columnar database, and it only scans the specific columns requested in the query. Querying two columns (PULocationID, DOLocationID) requires reading more data than querying one column (PULocationID), leading to a higher estimated number of bytes processed.**
### Question 4

```bash
SELECT COUNT(*)
FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata_2024_non_partitioned
WHERE fare_amount = 0;

```
Answer: **8,333**
### Question 5
To create table:
```bash
CREATE OR REPLACE TABLE dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata_2024_partitioned_clustered
PARTITION BY DATE(tpep_dropoff_datetime)
CLUSTER BY VendorID AS
SELECT * FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.external_yellow_tripdata_2024;
```
Answer: **Partition by tpep_dropoff_datetime and Cluster on VendorID**

### Question 6
for regular/materialized table:
```bash
SELECT DISTINCT VendorID
FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata_2024_non_partitioned
WHERE tpep_dropoff_datetime >= '2024-03-01' AND tpep_dropoff_datetime < '2024-03-16';
```
for partitioned and clustered table:

```bash
SELECT DISTINCT VendorID
FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata_2024_partitioned_clustered
WHERE tpep_dropoff_datetime >= '2024-03-01' AND tpep_dropoff_datetime < '2024-03-16';
```
Answer: **310.24 MB for non-partitioned table and 26.84 MB for the partitioned table**

### Question 7
Answer: **GCP Bucket**

### Question 8
On small datasets, clustering often creates extra overhead without performance gains. It becomes valuable for large datasets—typically multi-gigabyte or terabyte scale—where filtering or aggregation on clustering columns is common.

Answer: **False**

### Question 9

for external table
```bash
SELECT COUNT(*)
FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.external_yellow_tripdata_2024;

```
- Estimated Bytes processed: 0B
- Actual Bytes processed: 0B (Because parquet files have metadata)

for materialized table:
```bash
SELECT COUNT(*)
FROM dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata_2024_non_partitioned;
```

- Estimated Bytes processed: 0B (Because it can just read from metadata)
- Actual Bytes processed: 0B (Because it can just read from metadata)
