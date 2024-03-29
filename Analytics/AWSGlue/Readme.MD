- AWS glue is mainly used to extract data from a source ( Amazon S3, Amazon DynamoDB, Delta Lake, JDBC - Amazon Redshift, RDS, etc) Then transform those data souce after that load the data to another target ( Amazon S3, Amazon DynamoDB, Delta Lake, JDBC - Amazon Redshift, RDS, etc ).
- AWS Glue is a fully managed ETL (extract, transform, and load) service that makes it simple and cost-effective to categorize your data, clean it, enrich it, and move it reliably between various data stores and data streams.
- AWS Glue is serverless, so there’s no infrastructure to set up or manage unlike EMR.
- AWS Glue is designed to work with semi-structured data.
- It is based on dynamic frame, Which is similer to apache spark.
- You can convert between dynamic frames and Spark dataframes, so that you can take advantage of both AWS Glue and Spark transformations to do the kinds of analysis that you want.
## AWS Glue Terminology -
### AWS Glue Data Catalog
The persistent metadata store in AWS Glue. It contains table definitions, job definitions, and other control information to manage your AWS Glue environment. Each AWS account has one AWS Glue Data Catalog per region. It contains databases and tables.

### Classifier - creates schema as per file format
Determines the schema of your data. AWS Glue provides classifiers for common file types, such as CSV, JSON, AVRO, XML, and others. It also provides classifiers for common relational database management systems using a JDBC connection. You can write your own classifier by using a grok pattern or by specifying a row tag in an XML document.

### Connection
A Data Catalog object that contains the properties that are required to connect to a particular data store. You can use source or targer as connection then inside glue job you can use those connections as source or target.

### Crawler
A program that connects to a data store (source or target), progresses through a prioritized list of classifiers to determine the schema for your data, and then creates metadata tables in the AWS Glue Data Catalog. It reads the data from data sources then create a metadata table ).

### Database
A set of associated Data Catalog table definitions organized into a logical group.

### Data store, data source, data target
A data store is a repository for persistently storing your data. Examples include Amazon S3 buckets and relational databases. A data source is a data store that is used as input to a process or transform. A data target is a data store that a process or transform writes to.

### Development endpoint
An environment that you can use to develop and test your AWS Glue ETL scripts.

### Dynamic Frame
A distributed table that supports nested data such as structures and arrays. Each record is self-describing, designed for schema flexibility with semi-structured data. Each record contains both data and the schema that describes that data. You can use both dynamic frames and Apache Spark DataFrames in your ETL scripts, and convert between them. Dynamic frames provide a set of advanced transformations for data cleaning and ETL.

### Job
The business logic that is required to perform ETL work. It is composed of a transformation script, data sources, and data targets. Job runs are initiated by triggers that can be scheduled or triggered by events.

### Notebook server
A web-based environment that you can use to run your PySpark statements. PySpark is a Python dialect for ETL programming. For more information, see Apache Zeppelin. You can set up a notebook server on a development endpoint to run PySpark statements with AWS Glue extensions.

### Script
Code that extracts data from sources, transforms it, and loads it into targets. AWS Glue generates PySpark or Scala scripts.

### Table
The metadata definition that represents your data. Whether your data is in an Amazon Simple Storage Service (Amazon S3) file, an Amazon Relational Database Service (Amazon RDS) table, or another set of data, a table defines the schema of your data. A table in the AWS Glue Data Catalog consists of the names of columns, data type definitions, partition information, and other metadata about a base dataset. The schema of your data is represented in your AWS Glue table definition. The actual data remains in its original data store, whether it be in a file or a relational database table. AWS Glue catalogs your files and relational database tables in the AWS Glue Data Catalog. They are used as sources and targets when you create an ETL job.

### Transform
The code logic that is used to manipulate your data into a different format.

### Trigger
Initiates an ETL job. Triggers can be defined based on a scheduled time or an event.

### Worker
With AWS Glue, you only pay for the time your ETL job takes to run. There are no resources to manage, no upfront costs, and you are not charged for startup or shutdown time. You are charged an hourly rate based on the number of Data Processing Units (or DPUs) used to run your ETL job. A single Data Processing Unit (DPU) is also referred to as a worker. AWS Glue comes with three worker types to help you select the configuration that meets your job latency and cost requirements. Workers come in Standard, G.1X, G.2X, and G.025X configurations.

---
## Example 1 -
You can pick multiple data from multiple data source then make a schema of all of them and create a logical table using crawler. After that use a table as extract data
source of glue job then transform it using script. After that loads the transformed data to another target ( example redshit ).
## Example 2 - Convert semi structured data schema( json ) of s3 to relational data schema of rds -
AWS Glue uses crawlers to infer schemas for semi-structured data. It then transforms the data to a relational schema using an ETL (extract, transform, and load) job. For example, you might want to parse JSON data from Amazon Simple Storage Service (Amazon S3) source files to Amazon Relational Database Service (Amazon RDS) tables. Understanding how AWS Glue handles the differences between schemas can help you understand the transformation process.
https://docs.aws.amazon.com/glue/latest/dg/schema-relationalize.html
