- It is used to store large data and analyze on it using sql.
- Redshift is based on PostgreSQL, but it’s not used for OLTP
- It’s OLAP – online analytical processing (analytics and data warehousing)
- 10x better performance than other data warehouses, scale to PBs of data
- Columnar storage of data (instead of row based)
- Massively Parallel Query Execution (MPP)
- Pay as you go based on the instances provisioned
- Has a SQL interface for performing the queries ( EMR uses handloop, spark etc )
- BI tools such as AWS Quicksight or Tableau integrate with it.
- Data is loaded from S3, DynamoDB, DMS, other DBs…
- From 1 node to 128 nodes, up to 128 TB of space per node
- Leader node: for query planning, results aggregation
- Compute node: for performing the queries, send results to leader
- Redshift Spectrum: perform queries directly against S3 (no need to load)
- Backup & Restore, Security VPC / IAM / KMS, Monitoring
- Redshift Enhanced VPC Routing: COPY / UNLOAD goes through VPC

### Redshift – Snapshots & DR
- Redshift has no “Multi-AZ” mode
- Snapshots are point-in-time backups of a cluster, stored internally in S3
- Snapshots are incremental (only what has changed is saved)
- You can restore a snapshot into a new cluster
- Automated: every 8 hours, every 5 GB, or on a schedule. Set retention
- Manual: snapshot is retained until you delete it
- You can configure Amazon Redshift to automatically copy snapshots (automated or manual) of a cluster to another AWS Region
### Loading data into Redshift - You can load data to redshift from 
- Amazon Kinesis Data Firehose to redshift
- From S3 using COPY command to redshift
- From EC2 Instance JDBC driver to redshift.
### Redshift Spectrum
- Query data that is already in S3 without loading it
- Must have a Redshift cluster available to start the query
- The query is then submitted to thousands of Redshift Spectrum nodes
### Redshift for Solutions Architect
- Operations: like RDS
- Security: IAM, VPC, KMS, SSL (like RDS)
- Reliability: auto healing features, cross-region snapshot copy
- Performance: 10x performance vs other data warehousing, compression
- Cost: pay per node provisioned, 1/10th of the cost vs other warehouses
- vs Athena: faster queries / joins / aggregations thanks to indexes
- Remember: Redshift = Analytics / BI / Data Warehouse
- vs EMR: EMR uses handoop, spark etc to query on large data but redshift uses SQL.
### Benefits of Replicating Data from Amazon RDS to Redshift
Many organizations will have a separate database (Eg: Amazon RDS) for all the online transaction needs and another warehouse (Eg: Amazon Redshift) application for all the offline analysis and large aggregation requirements. There is an obvious need to move data across these two databases (Eg: Amazon RDS to Redshift) for the following reasons:

- The online database is usually optimized for quick responses and fast writes. Running large analysis or aggregation jobs over this database will slow down the database and can affect your customer experience.
- The warehouse application can have data from multiple sources and not only transactional data. There may be third-party sources or data sources from other parts of the pipeline that needs to be used for analysis or aggregation.
