- In real time - AWS Kinesis data stream
- In near real time - Aws kinesis firehose
- data to analyse in future - Aws kinesis firehose
- Stream data- aws kinesis any one 
- Ingest data - kinesis data stream / firehose
- processing data - ec2, lambda, ecs etc
- SQS queues have a maximum retention time of 14 days.
- SQS is not the most efficient service for streaming, real time data.
- you cannot save data to EBS from Kinesis.
---
### A retail company with many stores and warehouses is implementing IoT sensors to gather monitoring data from devices in each location. The data will be sent to AWS in real time. A solutions architect must provide a solution for ensuring events are received in order for each device and ensure that data is saved for future processing. Which solution would be MOST efficient?
- (ans) Use Amazon Kinesis Data Streams for real-time events with a partition key for each device. Use Amazon Kinesis Data Firehose to save data to Amazon S3.
- (explanation) Amazon Kinesis Data Streams collect and process data in real time. A Kinesis data stream is a set of shards. Each shard has a sequence of data records. Each data record has a sequence number that is assigned by Kinesis Data Streams. A shard is a uniquely identified sequence of data records in a stream. </br>
A partition key is used to group data by shard within a stream. Kinesis Data Streams segregates the data records belonging to a stream into multiple shards. It uses the partition key that is associated with each data record to determine which shard a given data record belongs to. </br>
For this scenario, the solutions architect can use a partition key for each device. This will ensure the records for that device are grouped by shard and the shard will ensure ordering. Amazon S3 is a valid destination for saving the data records. 
