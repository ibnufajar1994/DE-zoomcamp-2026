## Question 1:  ##

Open log files on q1.yaml, it will give outputs:
```bash
-rw-r--r-- 1 root root 129M Feb 01 10:35 file.csv
128.3 MiB
```
**The Answer: 128.3 MiB**

## Question 2: ##
The file is named using the format {{inputs.taxi}}_tripdata_{{inputs.year}}-{{inputs.month}}.csv. For example, if the taxi input is green, the year is 2020, and the month is 04 at runtime, the resulting file name will be green_tripdata_2020-04.csv.

## Question 3: ##
```bash
SELECT
	COUNT(*)
FROM
	dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata
WHERE
	tpep_pickup_datetime >= '2020-01-01'
	AND tpep_pickup_datetime < '2021-01-01'
```
The query will result: 24648235
Closest Answer:**24,648,499**

## Question 4: ##
```bash
SELECT
	COUNT(*)
FROM
	dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.green_tripdata
WHERE
	lpep_pickup_datetime >= '2020-01-01'
	AND lpep_pickup_datetime < '2021-01-01'
```
The query will result: 1733999
Closest Answer:**1,734,051**

## Question 5: ##

```bash
SELECT
	COUNT(*)
FROM
	dtc-de-course-485117.dtc_de_course_485117_module_1_dataset.yellow_tripdata_2021_03
```
The query will result: 1925152
Closest Answer:**1,925,152**


## Question 6:##
Add a timezone property set to America/New_York in the Schedule trigger configuration
```bash
triggers:
  - id: run_schedule
    type: io.kestra.plugin.core.trigger.Schedule
    cron: "0 9 * * *"
    timezone: "America/New_York"

```


