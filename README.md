# Lab 4: Distributed ETL Pipeline using Apache Spark, Airflow, and Cassandra

## Project Overview
This repository contains a data engineering pipeline that orchestrates a Spark ETL process using Apache Airflow. The objective is to automate the ingestion and transformation of large datasets into a distributed Cassandra database.

For this implementation, I utilized **DataStax Astra DB** (Cloud Cassandra) to ensure high availability and managed scalability, bypassing local environment constraints.

## Pipeline Architecture
The ETL workflow is split into two primary Spark jobs:

1.  **Ingestion Layer (Load Job):** Processes 100k records from a raw CSV source and writes them into a primary Cassandra table.
2.  **Processing Layer (Transform Job):** Extracts data from the primary table, performs logic-based transformations, and loads the results into a secondary analytics table.

## Prerequisites & Environment
- **Environment:** Linux-based Cloud IDE (Gitpod/Ubuntu)
- **Engine:** Apache Spark 3.0.1
- **Orchestration:** Apache Airflow
- **Storage:** DataStax Astra (Serverless Cassandra)

---

## Setup & Implementation Steps

### 1. Database Configuration (Astra DB)
- Created a database instance named `lab4_db` with the keyspace `corp_data`.
- Generated a **Database Administrator** token (Client ID and Client Secret) for secure API authentication.
- Downloaded the **Secure Connect Bundle (SCB)** to enable the Spark-to-Cassandra driver connection.

### 2. Schema Initialization
Using the Astra CLI, I initialized the target tables defined in `setup.cql`:
```bash
astra db cqlsh lab4_db -f setup.cql