## Kinesis Overview -
- Makes it easy to collect, process, and analyze streaming data in real-time 
- Ingest real-time data such as: Application logs, Metrics, Website clickstreams, 
IoT telemetry data.
**Kinesis Data Streams**: capture, process, and store data streams (Retention between 1 day to 365 days)
**Kinesis Data Firehose**: load data streams into AWS data stores ( like s3 )
**Kinesis Data Analytics**: analyze data streams with SQL or Apache Flink
**Kinesis Video Streams**: capture, process, and store video streams
---
## Kinesis Data Streams - 
Retention between 1 day to 365 days
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
**On-demand mode:**
- No need to provision or manage the capacity
- Default capacity provisioned (4 MB/s in or 4000 records per second)
- Scales automatically based on observed throughput peak during the last 30 days
- Pay per stream per hour & data in/out per GB

