2020s

Databricks

## What did a data pipeline look like before data lakehouse?

Complex systems to support analytics and ML
- creating, maintaining, and processing data: time-consuming with many systems


1. incoming data
	1. real time analytics engines? (Kafka)
2. data lake 1
	1. takes time to transfer tons of data from 
3. data lake 2
4. ...
5. data warehouse 1
6. ...
7. final data warehouse

Your final data warehouse would always be a few days stale


[!What is Delta Lake]-
>Apache Spark + Parquet file format
> - data lake layers that support transactions and data quality controls
> - data all in one place
> - metadata transactions
> - Apache Spark to process the data lake

Analytics engine
- indexing, caching (spark)

## Databricks

1. Managed Apache Spark
2. Delta Lake
	1. all data in one place
		1. instead of in data lakes and data warehouses
	2. data can be used in multiple jobs
		1. at the same time
	3. parquet files with metadata transactions
3. ML Flow
    1. data scientist: how do I deploy this model
    2. model registry, deployment
    3. alternative: Kubeflow
4. Code
	1. Jupyter notebooks
5. Web UI
	1. execute jobs
	2. view run
	3. task orchestration


## Databricks vs Snowflake

????
