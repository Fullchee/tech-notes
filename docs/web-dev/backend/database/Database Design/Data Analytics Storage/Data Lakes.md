2010s

>[!Benefits of data lake (2)]-
>- Cheap/unlimited data storage (HDFS)
>	- cheap hardware 
>- Unstructured data (images, audio, video, JSON) (just files)

>[!What breakthrough did HDFS introduce?]-
>- Hadoop distributed file system
>- removed file limit (everything is a file)

>[!HDFS vs AWS S3]-
>- you can have HDFS on AWS S3 now
>- S3 is cheaper

Parquet (data format)
- pseudo tables
- you still access it like a file??

>[!Downsides to data lake (3)]-
>- no transactions
>- slow
>	- No indexes
>	- schema on read: more flexible but slower
>	- like JS dynamic object
>- No built-in quality controls


## Structure layers

- raw data
- cleaned data
- enriched data
	- what was the weather that day? Do people buy more stuff on rainy days?

Tool used: Apache Spark



What’s the context for this databricks stuff?

1. Commissions runs are moving to databricks
2. So it makes sense to run restores all in databricks
3. And then move the app database to databricks too
4. And then the data

Delta stuff 

Tracking things over time

