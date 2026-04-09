# 🚀 E-Commerce Data Engineering Pipeline (Databricks | PySpark | SQL)

## 📌 Project Overview

This project demonstrates an **end-to-end data engineering pipeline** built in **Databricks** using **PySpark and SQL**, following the **Lakehouse architecture (Bronze → Silver → Gold)**.

The pipeline processes raw e-commerce data, performs data cleaning and transformations, and generates business insights for analytics.

---

## 🧠 Architecture (Lakehouse)

```text
Raw CSV → Bronze → Silver → Gold → Analytics
```

---

## ⚙️ Technologies Used

* Databricks (Lakehouse Platform)
* PySpark
* SQL (Spark SQL)
* Delta Lake

---

## 📂 Data Source

* customers.csv
* orders.csv
* order_items.csv

Uploaded into **DBFS (Databricks File System)**

---

## 🏗️ Pipeline Implementation

---

### 🥉 Bronze Layer (Raw Ingestion)

* Loaded raw data from DBFS
* Stored as Delta tables

```python
df = spark.read.csv("/FileStore/tables/orders.csv", header=True, inferSchema=True)

df.write.format("delta").saveAsTable("orders_bronze")
```

---

### 🥈 Silver Layer (Cleaning & Transformation)

* Removed NULL values
* Removed duplicates
* Standardized data
* Created revenue column

```sql
CREATE TABLE orders_silver AS
SELECT DISTINCT *,
       price * quantity AS revenue
FROM orders_bronze
WHERE price IS NOT NULL
  AND quantity IS NOT NULL;
```

---

### 🥇 Gold Layer (Business Logic)

* Joined multiple tables
* Generated analytics-ready datasets

```sql
SELECT city,
       SUM(revenue) AS total_revenue
FROM sales_gold
GROUP BY city;
```

---

## 📊 Business Insights

* Revenue per city
* Top 3 customers
* Top product per city
* Category performance
* Repeat customers
* Customer segmentation

---

## 🔥 Key Features

* Built using **Databricks Lakehouse architecture**
* Combined **SQL + PySpark**
* Used **Delta tables**
* Implemented **window functions (RANK)**
* End-to-end **ELT pipeline**

---

## 📁 Project Structure

```text
project/
│
├── data/
├── notebooks/
│   └── databricks_pipeline.py
├── output/
└── README.md
```

---

## 🚀 How to Run in Databricks

1. Upload CSV files to DBFS
2. Create Bronze tables using PySpark
3. Run SQL queries for Silver and Gold layers
4. Query results using Spark SQL

---

## 💡 Key Learnings

* Lakehouse Architecture (Bronze, Silver, Gold)
* ELT pipeline design
* PySpark transformations
* SQL window functions
* Data cleaning techniques

---

## 🎯 Future Improvements

* Add incremental pipelines
* Optimize using Delta Lake (Z-Order, Partitioning)
* Schedule jobs using Databricks Workflows

---

## 👨‍💻 Author

Koushik Reddy
Aspiring Data Engineer 🚀

---

## ⭐ Support

If you found this useful, give a ⭐ on GitHub!
