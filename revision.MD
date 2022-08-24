## Placement group -
### Cluster - 
- All Ec2 instances will be placed inside a single rack / hardware.
- Use cases
     - Big Data job that needs to complete fast
     - Application that needs extremely low latency and high network throughput

### Spread - 
- each Ec2 instance will be spread in different rack / hardware.
- Span over multi az but 7 instance per az.
- Use case: 
    -  Application that needs to maximize high availability
    -  Critical Applications where each instance must be isolated from failure from each other

### Partition -
- upto 7 partition per az.
- per partition has separe power source and hardware.
- If we place 5 ec2 in a single partition then those 5 ec2 shares power source and hardware.
- The instances in a partition do not share racks with the instances in the other partitions
- Scales to 100s of EC2 instances per group.
- Use cases: HDFS, HBase, Cassandra, Kafka


## Protocol of amazon MQ -

- MQTT, AMQT, STOMP, WSS, openwire
- full form = managed Apache ActiveMQ

## Order of SQS FIFO after visibility timeout -
- The order remains the same: [A, B, C, D] . In fact, it is not possible to fetch another message from the queue with the same Message Group ID until message A has been processed. This ensures that the order is preserved. Where certain messages are allowed to be processed in parallel, you can specify a different Message Group ID.
- Dead letter queue is not recommended for SQS FIFO
