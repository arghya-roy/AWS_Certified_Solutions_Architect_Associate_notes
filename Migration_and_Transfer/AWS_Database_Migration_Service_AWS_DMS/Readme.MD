## Aws Database migration service -
- Helps to migrate your on prem db to cloud and cloud to on prem
      - same engine or different engine
      - to migrate to different engine you need to use SCT means schema conversion tool.
      - SCT is also needed for same engine also if the engine version of on prem and cloud are too different.
- Helps to migrate one type of engine of cloud to another type of engine in cloud
      - SCT is needed.
      
 
## DMS – Database Migration Service
- Quickly and securely migrate databases to AWS, resilient, self healing
- The source database remains available during the migration
- Supports:
     - Homogeneous migrations: ex Oracle to Oracle
     - Heterogeneous migrations: ex Microsoft SQL Server to Aurora
- Continuous Data Replication using CDC
- You must create an EC2 instance ( replocation instance ) to perform the replication tasks

## DMS Sources and Targets

### SOURCES:
- On-Premise and EC2 instances databases: Oracle, MS SQL Server, MySQL, MariaDB, PostgreSQL, MongoDB, SAP, DB2
- Azure: Azure SQL Database
- Amazon RDS: all including Aurora
- Amazon S3

### TARGETS -
- On-Premise and EC2 instances databases: Oracle, MS SQL Server, MySQL, MariaDB, PostgreSQL, SAP
- Amazon RDS
- Amazon Redshift
- Amazon DynamoDB
- Amazon S3
- ElasticSearch Service
- Kinesis Data Streams
- DocumentDB

## AWS Schema Conversion Tool (SCT)
- Convert your Database’s Schema from one engine to another
- Example OLTP: (SQL Server or Oracle) to MySQL, PostgreSQL, Aurora
- Example OLAP: (Teradata or Oracle) to Amazon Redshift
- Prefer compute-intensive instances to optimize data conversions
- You do not need to use SCT if you are migrating the same DB engine
    - Ex: On-Premise PostgreSQL => RDS PostgreSQL
    - The DB engine is still PostgreSQL (RDS is the platform)
    
