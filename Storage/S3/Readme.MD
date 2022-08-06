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
