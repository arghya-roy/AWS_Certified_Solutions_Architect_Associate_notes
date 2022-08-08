- With a gateway vpc endpoint you configure your route table to point to the endpoint. Amazon S3 and DynamoDB use gateway endpoints.
- Dynamodb does not take any downtime for scaling vertically. ( where rds and aurora take downtime, It will take less time when multiaz enables but will take downtime)
- dynamodb Store objects larger than 400KB in S3 and use pointers in DynamoDB

### DynamoDB Overview
- AWS proprietary technology, managed NoSQL database
- Serverless, provisioned capacity, auto scaling, on demand capacity (Nov 2018)
- Can replace ElastiCache as a key/value store (storing session data for example)
- Highly Available, Multi AZ by default, Read and Writes are decoupled, DAX for read cache
- Reads can be eventually consistent or strongly consistent or transactional
- Security, authentication and authorization is done through IAM
- DynamoDB Streams to integrate with AWS Lambda
- Backup / Restore feature, Global Table feature
- Monitoring through CloudWatch
- Can only query on primary key, sort key, or indexes

### Use Case: 
Serverless applications development (small documents 100s KB), distributed serverless cache, doesn’t have SQL query language available, has transactions capability from Nov 2018

### DynamoDB for Solutions Architect
- Operations: no operations needed, auto scaling capability, serverless
- Security: full security through IAM policies, KMS encryption, SSL in flight
- Reliability: Multi AZ, Backups
- Performance: single digit millisecond performance, DAX for caching 
reads, performance doesn’t degrade if your application scales
- Cost: Pay per provisioned capacity and storage usage (no need to guess 
in advance any capacity – can use auto scaling)

### Eventual vs Strong Consistency -
- Means as a example you are replicating your data into 3 replica. 
- just put a data ( assume that data exist only 1 replica still now )
- when you do a eventually then you will get the data but when you do strong then you will not get that.
- Because strong only give you which completed all steps.

### Read capacity unit (RCU) -
- 1RCU = 4KB
- **For Strong Consistency** one RCU can perform one strongly consistent read request per second.  1 RCU = 4 KB
- **For Eventual Consistency** one RCU can perform two eventually consistent read requests per second.  1 RCU = 8 KB
- **For transactional Consistency** two RCU can perform one transactional consistent read request per second.  1 RCU = 2 KB
- For example, a strongly consistent read of an 8 KB item would require two RCUs, an eventually consistent read of an 8 KB item would require one RCU, and a transactional read of an 8 KB item would require four RCUs. 

### Write capacity unit (WCU):
- No eventually write
- **For Strong write** One wcu can perform one write request per sec. 1 WCU = 1 KB
- **For transactional write** two wcu can perform one write request per sec. 1 WCU = 1/2 KB
- or example, a standard write request of a 1 KB item would require one WCU, a standard write request of a 3 KB item would require three WCUs, and a transactional write request of a 3 KB item would require six WCUs.

### Dynamodb Table class -

- **Standard** DynamoDB offers two table classes designed to help you optimize for cost. The DynamoDB Standard table class is the default, and is recommended for the vast majority of workloads. 
 
- **Standard-IA** The DynamoDB Standard-Infrequent Access (DynamoDB Standard-IA) table class is optimized for tables where storage is the dominant cost. For example, tables that store infrequently accessed data, such as application logs, old social media posts, e-commerce order history, and past gaming achievements, are good candidates for the Standard-IA table class.


## DynamoDB Streams -
- Amazon DynamoDB Streams captures a time-ordered sequence of item-level modifications in any DynamoDB table and stores this information in a log for up to 24 hours. Applications can access this log and view the data items as they appeared before and after they were modified, in near-real time.
- Every time an item in an Amazon DynamoDB table is modified, ceated, deleted, then the log is stored in dynamodb stream for 24 hrs.
- The deleted item data will not be recorded in CloudWatch Logs. But it recored in dynamodb stream
- CloudTrail records API actions so it will not record the data from the item that was modified.
- can not store dynamodb stream to s3 directly.
### To store dynamodb stream log permanantly -
DynamoDB stream is being consumed by a Lambda function which processes the item data and records a record in CloudWatch Logs - dynamodb strem to lambda to cloudwatch.

## Dynamodb global table -
- You can replicate your table in multiple region.
- need to enable dynamodb stream.
- may need to create replication group ( not sure ).
- It is multi master configure means you can edit table in any of region.
- user can be redireted based on their region.

## DynamoDB Accelerator (DAX) -
- It is cache of dynamodb.
- It is a cluster.
--
