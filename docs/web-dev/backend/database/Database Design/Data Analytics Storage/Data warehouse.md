First data warehouse in 1980s

>[!Why can't we use our app database to generate reports/analyze data? (3)]-
>1. we don't want our app to slow down when we analyze our data
>2. It may not work: Analysis tool may expect a specific format
>	- Power BI: might expect a star schema, machine learning expects a different format
>3. Even if it works, joining large tables together is slow

>[!What is OLAP?]-
>- multi dimensional data analysis
>- analyze data for business queries
>- aggregations (sums, avg) precomputed on multiple dimensions
>- informed decision making

>[!Example implementation of a small data warehouse]-
>use a regular SQL database

>[!Example implementation of large data warehouse]-
>Google BigQuery
>Amazon Redshift
>Snowflake

>[!Downsides to data warehouses (2)]-
> - expensive hardware, which means you can't have all your data there
> 	- SSDs
> 	- for petabytes and exabytes of data
>- AI: SQL interface isn't great for machine learning tools
>	- don't deal with pictures well

## Data warehouse schema


Fact table
- holds primary keys of dimension tables
- quantitative metrics that can be calculated
	- amount, quantity


Dimension table
- contain data common across events
- sale at retailer
	- tables for customer information
	- 

![[image-20230429114535190.png]]

Example star schema query


- we can't use it because we drop the full_result table
	- star schema auxiliary table foreign keys

- snowflake schema
	- stuff is 

- Ralph Kimble
- Inmon


Schema on write