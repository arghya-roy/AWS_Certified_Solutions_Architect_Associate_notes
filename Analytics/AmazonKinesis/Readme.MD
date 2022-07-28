
https://digitalcloud.training/amazon-kinesis/#kinesis-video-streams


## Kinesis Overview - All of them are serverless
- Makes it easy to collect, process, and analyze streaming data in real-time 
- Ingest real-time data such as: Application logs, Metrics, Website clickstreams, 
IoT telemetry data.
- **Kinesis Data Streams**: capture, process, and store data streams (Retention between 1 day to 365 days)
- **Kinesis Data Firehose**: load data streams into AWS data stores ( like s3 )
- **Kinesis Data Analytics**: analyze data streams with SQL or Apache Flink
- **Kinesis Video Streams**: capture, process, and store video streams
---
## Kinesis Data Streams - 
- Amazon Kinesis Data Streams is a serverless streaming data service that makes it easy to capture, process, and store data streams at any scale.
- Retention between 1 day to 365 days
- By default, records of a stream are accessible for up to 24 hours from the time they are added to the stream (can be raised to 7 days by enabling extended data retention).
- Ability to reprocess (replay) data
- Once data is inserted in Kinesis, it can’t be deleted (immutability)
- Data that shares the same partition goes to the same shard (ordering)
- Kinesis Data Streams replicates synchronously across three AZs.
- **Producers:** AWS SDK, Kinesis Producer Library (KPL), Kinesis Agent
- **Consumers:** Write your own: Kinesis Client Library (KCL), AWS SDK | Managed: AWS Lambda, Kinesis Data Firehose, Kinesis Data Analytics,
### Capacity Modes -
**Provisioned mode:**
- You choose the number of shards provisioned, scale manually or using API
- Each shard gets 1MB/s in (or 1000 records per second)
- Each shard gets 2MB/s out (classic or enhanced fan-out consumer)
- You pay per shard provisioned per hour
- 
**On-demand mode:**
- No need to provision or manage the capacity
- Default capacity provisioned (4 MB/s in or 4000 records per second)
- Scales automatically based on observed throughput peak during the last 30 days
- Pay per stream per hour & data in/out per GB
### Details -
- Kinesis data stream picks real time data as producer through kinesis agent from any app / website / ec2. Then pass those inside shard of kinesis. Shard keeps data records in serial no wise. Then loads those realtime data inside another server / ec2 / app / lambda as consumer.
- You can keep multiple shards as per data requests.
- data will be loaded from code. If you want to load data to lambda then it lambda have to set kinesis stream as a trigger.
- For provisioned mode scaling is required.
### **Shards of Kinesis Data Streams** -

### For ondemand -
By default, data streams with on-demand mode scale throughput automatically to accommodate traffic of up to 200 MiB per second and 200,000 records per second for the write capacity. If traffic exceeds capacity, your data stream will throttle.
- Write capacity - Maximum
  200 MiB/second and 200,000 records/second
- Read capacity - Maximum (per consumer) 400 MiB/second Up to 2 default consumers. Use Enhanced Fan-Out (EFO) for more consumers. EFO supports adding upto 20     consumers, each having a **dedicated throughput**.

### For Provisioned -
- Write capacity -Maximum 1 MiB/second and 1,000 records/second per shard
- read capacity - Maximum 2 MiB/second

## Record or data of shards -
Record is made up of 3 things 1) partition key 2) sequence number 3) data blob
### partition key -
- group of related data
- data with same partition key will go to same shard/
### sequence number -
- unique number per record.
- added automatically by the kinesis
### data blob -
- It is actual data which can be of max 1 MB
### every record is a binary data, which can be json, csv etc.

### Resharding of shard -
- There are two types of resharding operations: shard split and shard merge.
- In a shard split, you divide a single shard into two shards.
- In a shard merge, you combine two shards into a single shard.
- Splitting increases the number of shards in your stream and therefore increases the data capacity of the stream.
- Splitting increases the cost of your stream (you pay per-shard).
- Merging reduces the number of shards in your stream and therefore decreases the data capacity—and cost—of the stream.

### Use cases of kinesis data stream -
- Accelerated log and data feed intake.
- Real-time metrics and reporting.
- Real-time data analytics.
- Complex stream processing.
---






## Kinesis Data Firehose -
- It is mainly used to store real time data to s3 or rds.
- It puts data to destination in near realtime means within 60 sec Or minimum 32 MB of data at a time.
- Supports many data formats, conversions, transformations, compression
- Supports custom data transformations using AWS Lambda. **for transformation** - lambda
-  If you want to do any transformation of your data before load to destination then you can use lambda before load (consumer ).
-  Can send failed or all data to a backup S3 bucket.
-  no need to use shards here. serverless
-  Kinesis Firehose will take care of all of the monitoring, scaling, and data management for you.
-  With Kinesis Data Firehose you don’t need to write an application or manage resources.
- Firehose can batch, compress, and encrypt data before loading it.
- Firehose synchronously replicates data across three AZs as it is transported to destinations.
- Each delivery stream stores data records for up to 24 hours.
- A record is the data of interest your data producer sends to a delivery stream.
- The maximum size of a record (before Base64-encoding) is 1000 KB.
- A destination is the data store where your data will be delivered.
- **producer** - Application, clients, SDK, Kinesis Producer Library (KPL), Kinesis Agent, Kinesis data stream, clouthwatch log or event, AWS IoT etc.
- **Consumer** - s3, redshift, elasticsearch, HTTP endpoint, 3rd party partner: Splunk / MongoDB / DataDog / NewRelic
### use case -
- IoT Analytics
- Clickstream analytics
- log analytics
- security monitoring
---





## Kinesis Data Analytics -
- Perform real-time analytics on Kinesis Streams using SQL
- Fully managed, no servers to provision.
- No use to shards here
- Automatic scaling
- Amazon Kinesis Data Analytics takes care of everything required to run your real-time applications continuously and scales automatically to match the volume and throughput of your incoming data.
- Real-time analytics
- Pay for actual consumption rate
- Can create streams out of the real-time queries
- Can ingest data from Kinesis Streams and Kinesis Firehose.
- Output to S3, RedShift, Elasticsearch and Kinesis Data Streams.
- Sits over Kinesis Data Streams and Kinesis Data Firehose.
### Use cases:
- Time-series analytics
- Real-time dashboards
- Real-time metrics
- Generate time-series analytics.
- Feed real-time dashboards.
- Create real-time alerts and notifications.
### A Kinesis Data Analytics application consists of three components:
- **Input** – the streaming source for your application.
- **Application code** – a series of SQL statements that process input and produce output.
- **Output** – one or more in-application streams to hold intermediate results.
### Kinesis Data Analytics supports two types of inputs: streaming data sources and reference data sources:

- A streaming data source is continuously generated data that is read into your application for processing.
- A reference data source is static data that your application uses to enrich data coming in from streaming sources.

---




## Kinesis video stream -
- Can process or transfer realtime video.
- you do not have to build, operate, or scale any WebRTC related cloud infrastructure 
- **Producer** - Drones, cctv etc
- **Consumer** - amazon rekognization video, amazon segamaker, HLS based media playback etc.
- No infrastructure to be managed.
- Example - Live Youtube, Video call, Zoom etc.
- Kinesis Video Streams makes it easy to securely stream video from connected devices to AWS for analytics, machine learning (ML), and other processing.
- Durably stores, encrypts, and indexes video data streams, and allows access to data through easy-to-use APIs.
- Producers provide data streams.
- Stores data for 24 hours by default, up to 7 days.
- Stores data in shards – 5 transaction per second for reads, up to a max read rate of 2MB per second and 1000 records per second for writes up to a max of 1MB per second.
- Consumers receive and process data.
- Can have multiple shards in a stream.
- Not sure about shards

Supports encryption at rest with server-side encryption (KMS) with a customer master key.
---

- **Kinesis Data Streams**: For provisioned mode scaling is required but for on demand scaling will be done by amazon. Serverless. shards are required.
- **Kinesis Data Firehose**: scaling will be done by amazon. Serverless. shards are  not required.
- **Kinesis Data Analytics**: scaling will be done by amazon. Serverless. shards are  not required.
- **Kinesis Video Streams**: scaling will be done by amazon. Serverless. shards are  not required(not sure about shards).

---

