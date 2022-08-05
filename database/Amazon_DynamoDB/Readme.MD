- With a gateway vpc endpoint you configure your route table to point to the endpoint. Amazon S3 and DynamoDB use gateway endpoints.
- Dynamodb does not take any downtime for scaling vertically. ( where rds and aurora take downtime, It will take less time when multiaz enables but will take downtime)
- dynamodb Store objects larger than 400KB in S3 and use pointers in DynamoDB
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

--
