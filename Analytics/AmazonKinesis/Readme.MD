## Kinesis Overview -
- Makes it easy to collect, process, and analyze streaming data in real-time 
- Ingest real-time data such as: Application logs, Metrics, Website clickstreams, 
IoT telemetry data.
**Kinesis Data Streams**: capture, process, and store data streams (Retention between 1 day to 365 days)
**Kinesis Data Firehose**: load data streams into AWS data stores ( like s3 )
**Kinesis Data Analytics**: analyze data streams with SQL or Apache Flink
**Kinesis Video Streams**: capture, process, and store video streams

### Kinesis Data Streams - 
Retention between 1 day to 365 days
- Ability to reprocess (replay) data
- Once data is inserted in Kinesis, it can’t be deleted (immutability)
- Data that shares the same partition goes to the same shard (ordering)
- **Producers:** AWS SDK, Kinesis Producer Library (KPL), Kinesis Agent
- **Consumers:** Write your own: Kinesis Client Library (KCL), AWS SDK | Managed: AWS Lambda, Kinesis Data Firehose, Kinesis Data Analytics,
