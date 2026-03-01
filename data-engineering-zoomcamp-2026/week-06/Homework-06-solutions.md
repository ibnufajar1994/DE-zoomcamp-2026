# DE Zoomcamp - Module 6 Homework

This repository includes my completed solutions for **Module 6 Homework** from the Data Engineering Zoomcamp.

The assignment centers on batch data processing and analysis using **Apache Spark (PySpark)**.

---

## Environment Setup (Linux / WSL)

Tested on the following setup:

- Ubuntu 24.04  
- WSL2  

---

## Installing Java (Required for Spark 4.x)

Spark 4.x requires **Java 17 or Java 21**.

Install Java with:

```bash
sudo apt update
sudo apt install default-jdk
```

Confirm the installation:

```bash
java --version
```

Configure `JAVA_HOME` (add this to your `.bashrc` or `.zshrc` file):

```bash
export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which java))))
export PATH="${JAVA_HOME}/bin:${PATH}"
```

---

## Project Initialization

Initialize the project and install dependencies:

```bash
uv init
uv add pyspark notebook ipykernel
```

To launch Jupyter Notebook:

```bash
uv run jupyter notebook
```

---

# Dataset Information

The following datasets were used:

- Yellow Taxi Trip Data – November 2025  
- Taxi Zone Lookup Table  

Data source:  
https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

---

## Question 1

**Install Spark and PySpark. Create a local Spark session and display the Spark version.**

**Answer:**  
4.1.1  

---

## Question 2

**Load the November 2025 Yellow Taxi dataset.  
Repartition it into 4 partitions and save it in Parquet format.  
What is the average size of the generated Parquet files?**

**Answer:**  
25 MB  

---

## Question 3

**How many taxi trips occurred on November 15th, 2025 (based on pickup date)?**

Trips with pickup date `2025-11-15`:

**Answer:**  
162,604  

---

## Question 4

**What was the maximum trip duration in hours?**

Longest trip duration:

**Answer:**  
90.6 hours  

---

## Question 5

**Which port does the Spark UI use when running locally?**

**Answer:**  
4040  

---

## Question 6

**Which pickup location zone appears least frequently?**

After joining with the taxi zone lookup table:

**Answer:**  
Governor's Island/Ellis Island/Liberty Island  
