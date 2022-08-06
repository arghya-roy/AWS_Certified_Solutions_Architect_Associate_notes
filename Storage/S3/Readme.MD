### What is S3 Select?
Amazon S3 Select is new feature that allows you to perform simple SQL operations against your raw data stored in S3. One of the requirements is that your data needs to be in a structured format, i.e. JSON, CSV, Parquet. Do note that it will also work on compressed version of files so you don’t need to decompress them before reading.
S3 Select is a completely serverless solution. You don’t provision any servers or databases to make this run. </br>
One of the big limits though is that S3 Select only supports the SELECT clause in SQL. That means no joins, no groupings, and no other sophisticated SQL operations. In your SELECT statement, only the following other clauses are supported: </br>
- FROM
- WHERE
- LIMIT
Also note that nested json fields can also be accessed, so if you have deeply nested objects you should still be good to go. </br>
The other, most important constraint of S3 SELECT is that you can only perform a query on one object at at time. This makes S3 select not a suitable option for many use cases requiring parsing of entire bucket paths or collections of objects. </br>

### S3 select vs athena 
S3 Select is a lightweight solution designed to let you use SQL to perform simple SELECT clauses on a maximum of one file. Amazon Athena is an analytics workhorse that allows you to perform SQL on extremely large datasets spanning many files with great performance.

--
## A company has over 2000 users and is planning to migrate data into the AWS Cloud. Some of the data is user’s home folders on an existing file share and the plan is to move this data to Amazon S3. Each user will have a folder in a shared bucket under the folder structure: bucket/home/%username%. What steps should a Solutions Architect take to ensure that each user can access their own home folder and no one else’s? (choose 2)
### ANS -
Create an IAM policy that applies folder-level permissions and Create an IAM group and attach the IAM policy, add IAM users to the group.
## An application stores encrypted data in Amazon S3 buckets. A Solutions Architect needs to be able to query the encrypted data using SQL queries and write the encrypted results back the S3 bucket. As the data is sensitive fine-grained control ( Fine-grained access control is a method of controlling who can access certain data ) must be implemented over access to the S3 bucket. What combination of services represent the BEST options support these requirements? (choose 2)
### ANS -
- Use IAM policies to restrict access to the bucket.
- Use Athena for querying the data and writing the results back to the bucket

## An application will gather data from a website hosted on an EC2 instance and write the data to an S3 bucket. The application will use API calls to interact with the EC2 instance and S3 bucket. Which Amazon S3 access control method will be the MOST operationally efficient? (choose 2)
### ANS -
- Grant programmatic access.
- Create an IAM policy.

## A Solutions Architect would like to store a backup of an Amazon EBS volume on Amazon S3. What is the easiest way of achieving this?
### ANS -
- Create a snapshot of the volume. ( Snapshots capture a point-in-time state of an instance. Snapshots of Amazon EBS volumes are stored on S3 by design so you only need to take a snapshot and it will automatically be stored on Amazon S3. )
## A company has over 200 TB of log files in an Amazon S3 bucket. The company must process the files using a Linux-based software application that will extract and summarize data from the log files and store the output in a separate Amazon S3 bucket. The company needs to minimize data transfer charges associated with the processing of this data. How can a Solutions Architect meet these requirements?
### ANS -
- Launch an Amazon EC2 instance in the same Region as the S3 bucket. Process the log files and upload the output to another S3 bucket in the same Region.
- "Connect an AWS Lambda function to the S3 bucket via a VPC endpoint. Process the log files and store the output to another S3 bucket in the same Region" is incorrect. You cannot install a Linux-based software application on AWS Lambda. For lambda we can select runtime, we can not select operating system
