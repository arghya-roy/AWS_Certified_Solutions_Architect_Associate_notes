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
- Ability to reprocess (replay) data
- Once data is inserted in Kinesis, it can’t be deleted (immutability)
- Data that shares the same partition goes to the same shard (ordering)
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
### Use cases:
- Time-series analytics
- Real-time dashboards
- Real-time metrics

---

## Kinesis video stream -
- Can process or transfer realtime video.
- No need to use shards here
- you do not have to build, operate, or scale any WebRTC related cloud infrastructure 
- **Producer** - Drones, cctv etc
- **Consumer** - amazon rekognization video, amazon segamaker, HLS based media playback etc.
- No infrastructure to be managed.
- Example - Live Youtube, Video call, Zoom etc.
---

- **Kinesis Data Streams**: For provisioned mode scaling is required but for on demand scaling will be done by amazon. Serverless. shards are required.
- **Kinesis Data Firehose**: scaling will be done by amazon. Serverless. shards are  not required.
- **Kinesis Data Analytics**: scaling will be done by amazon. Serverless. shards are  not required.
- **Kinesis Video Streams**: scaling will be done by amazon. Serverless. shards are  not required.

---

### **Shards of Kinesis Data Streams** -
