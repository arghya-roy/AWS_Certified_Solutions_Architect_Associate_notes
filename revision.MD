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
- Like kinesis we can order message by partition key, in the same way we can order messase in sqs using group id ( If we dont use group id in sqs fifo then whivh message comes first that will out first. )


##  EBS Volumes come in 6 types
- gp2 / gp3 (SSD): General purpose SSD volume that balances price and performance for 
a wide variety of workloads
- io1 / io2 (SSD): Highest-performance SSD volume for mission-critical low-latency or 
high-throughput workloads
- Throughput Optimized HDD ( st1 ) (HDD): Low cost HDD volume designed for frequently accessed, throughput- intensive workloads
- Cold HDD (sc1) (HDD): Lowest cost HDD volume designed for less frequently accessed workloads

### Provisioned IOPS SSD (io1) -
- Provisioned IOPS SSD (io1 and io2) volumes provide low latency and are designed to meet the needs of I/O-intensive workloads. They are best for EBS-optimized instances.
- Critical business applications with sustained IOPS performance
- Or applications that need more than 16,000 IOPS
     - Great for databases workloads (sensitive to storage perf and consistency)
     - Size 4 GiB to 16384 GiB. 
     - 100 IOPS to 5000 IOPS and up to 50 IOPS per GiB
     - Throughput (MiB/s) is Not applicable.
     - EBS Multi-attach Supported
     - Can be boot volume?	Yes
### Provisioned IOPS SSD (io2) -
- Provisioned IOPS SSD (io1 and io2) volumes provide low latency and are designed to meet the needs of I/O-intensive workloads. They are best for EBS-optimized instances.
- Critical business applications with sustained IOPS performance
- Or applications that need more than 16,000 IOPS
     - Great for databases workloads (sensitive to storage perf and consistency)
     - Size 4 GiB to 65536 GiB. 
     - 100 IOPS to 100000 IOPS and up to 1000 IOPS per GiB
     - Throughput (MiB/s) is Not applicable.
     - EBS Multi-attach Supported
     - Can be boot volume?	Yes
- 
### General Purpose SSD (gp2) - 
- General Purpose SSD (gp2 and gp3) volumes offer cost-effective storage that is ideal for a broad range of workloads.
- Size 1 GiB to 16384 GiB. 
     - 100 IOPS to 3000 IOPS and 3 IOPS per GiB.
     - Throughput (MiB/s) is Not applicable
     - EBS Multi-attach not Supported
     - Can be boot volume?	Yes
### General Purpose SSD (gp3) - 
- General Purpose SSD (gp2 and gp3) volumes offer cost-effective storage that is ideal for a broad range of workloads.
- Size 1 GiB to 16384 GiB. 
     - 3000 IOPS to 16000 IOPS 
     - Throughput (MiB/s) is 125 MiB to 1000 MiB and 125 MiB/s per TiB.
     - EBS Multi-attach not Supported
     - Can be boot volume?	Yes

### Throughput Optimized HDD (st1) - ( t for throughput )
- Throughput Optimized HDD (st1) volumes provide low-cost magnetic storage that is a good fit for large, sequential workloads.
- Low-cost HDD volume, designed for frequently accessed. Throughput intensive workloads.
- Big Data, Data Warehouses, Log Processing
- Size 125 GiB to 16384 GiB. 
- IOPS is not applicable.
- Throughput (MiB/s) is 20 MiB to 123 MiB and 40 MiB/s per TiB.
- EBS Multi-attach not Supported
- Can be boot volume?	no
### Cold HDD (sc1) -  ( c for cold )
- Cold HDD (sc1) volumes provide low-cost magnetic storage that offers lower throughput than st1. sc1 is a good fit for large, sequential cold-data workloads that require infrequent access to data.
- Lowest cost HDD volume designed for less frequently accessed workloads
- Size 125 GiB to 16384 GiB. 
- IOPS is not applicable.
- Throughput (MiB/s) is 6 MiB/s to 40 MiB/s and 12 MiB/s per TiB.
- EBS Multi-attach not Supported
- Can be boot volume?	no

### Magnetic (standard) -
- Magnetic (standard) volumes are best suited for workloads where data is accessed infrequently.
- Size 1 GiB to 1024 GiB. 
- IOPS is Not applicable
- Throughput (MiB/s) is Not applicable
- EBS Multi-attach not Supported
- Can be boot volume?	no
