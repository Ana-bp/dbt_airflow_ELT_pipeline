# ELT Data Pipeline with dbt, Airflow & Snowflake

This repository contains a ELT (Extract, Load, Transform) pipeline project that utilizes Snowflake as a cloud data warehouse, dbt for transformations, and Airflow for orchestration.

The goal of this project is to showcase modular transformations, data modeling best practices, orchestration, containerization, and data quality validation in a production-like environment.

---

## 🏗 Architecture Overview

The pipeline follows a layered data architecture:

**1. Raw Layer (Snowflake)**
- Source data stored in Snowflake (snowflake_sample_data - TPCH_SF1)

**2. Staging Layer (dbt)**
- Data cleaning and standardization.
- Column renaming.

**3. Intermediate Layer**
- Business logic transformations.
- Joins and derived metrics.

**4. Mart Layer**
- Fact and dimension-ready tables.

**5. Orchestration (Airflow)**
- A scheduled DAG runs dbt transformations daily.
- dbt is executed inside a dedicated virtual environment within the Airflow container.

---

## 🗂 Project Structure
dbt_airflow_ELT_pipeline/  
│  
├── dags/  
│ ├── dbt/  
│ │ └── data_pipeline/ # dbt project  
│ └── dbt_dag.py # Airflow DAG  
├── Dockerfile    
├── requirements.txt  
├── packages.txt  
└── README.md  

---

## ⚙️ Tech Stack

- Python 3.12 # works better with dbt
- dbt-core
- dbt-snowflake
- Snowflake
- Apache Airflow (Astro CLI)
- Docker

---

## 🚀 How to Run Locally

### 1️⃣ Prerequisites

- Docker installed
- Astro CLI installed
- Snowflake account configured

### 2️⃣ Clone repository

- git clone https://github.com/Ana-bp/dbt_airflow_ELT_pipeline.git
- cd dbt_airflow_ELT_pipeline

### 3️⃣ Start Airflow

- astro dev start
  
Access Airflow UI at: http://localhost:8080

---

## 📊 Data Modeling

The project includes:

- **Staging models**
  - `stg_tpch_orders`
  - `stg_tpch_line_items`

- **Intermediate models**
  - `int_order_items`
  - `int_order_items_summary`

- **Mart models**
  - `fct_orders`

The modeling approach follows dimensional modeling principles, separating transformation layers and keeping business logic modular.

---

## ✅ Data Quality

Data quality checks are implemented using:

- dbt generic tests:
    - Data type
    - Null values
    - Uniqueness testing
    - Referential integrity
- Singular tests:
    - Discount validation
    - Date validation

All tests must pass before successful pipeline completion.

---

## 🔄 Orchestration

Airflow orchestrates the execution of dbt models using a `DbtDag` configuration.

The DAG:
- Runs on a daily schedule
- Installs dbt dependencies automatically
- Executes transformations within a controlled environment



You can find the hands-on tutorial for this project on https://youtu.be/OLXkGB7krGo?si=ULW_YgLg9dgqYOg-
