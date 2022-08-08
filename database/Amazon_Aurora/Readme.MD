## Amazon Aurora
Amazon Aurora is a fully managed MySQL- and PostgreSQL-compatible relational database built for the cloud that combines the performance and availability of traditional enterprise databases with the simplicity and cost-effectiveness of open source databases. ( Amazon RDS (Relational Database Service) is a managed SQL database service a relational database in cloud which makes it easy to provision, setup, patching, and backups. It supports Aurora, MySQL, PostgreSQL, MariaDB, Microsoft SQL Server, and Oracle database engines. ).

- Compatible API for PostgreSQL / MySQL 
- Data is held in 6 replicas, across 3 AZ 
- Auto healing capability 
- Multi AZ
- Auto Scaling Read Replicas 
- Read Replicas can be Global 
- Aurora database can be Global for DR or latency purposes 
- Auto scaling of storage from 10GB to 128 TB 
- Define EC2 instance type for aurora instances 
- Same security / monitoring / maintenance features as RDS 
- Aurora Serverless – for unpredictable / intermittent workloads 
- Aurora Multi-Master – for continuous writes failover 
- Use case: same as RDS, but with less maintenance / more flexibility / more performance




### Storage -
- RDS use Amazon EBS volumes for database and log storage. To achieve reliability, you need to enable the Multi-AZ feature on your RDS instance and replicate it synchronously to a standby replica in another Availability Zone.

- Aurora database storage is reliable and fault-tolerant by design. Aurora’s database storage is separate from the instances. In Aurora, data has 6 copies (as 10GB chunks distributed) to three Availability Zones. Hence, even if you have only one Aurora instance, your data will still have 6 copies.

### Performance
- RDS uses SSDs storage for better I/O throughput performance. You can choose between two SSD-backed storage options, that is, one that is optimized for high-performance OLTP applications and another one for cost-effective general-purpose use.

- Aurora gives two times throughput performance provided by PostgreSQL or five times the throughput provided by standard MySQL running on similar hardware.

- Aurora’s performance is higher and more consistent. Aurora writes logs directly to the storage without keeping log buffers. The replication to the replicas is asynchronous and for only cached data. Because the replicas also share the same storage cluster, the replica lag is small and consistent over time. Due to its unique storage design, Aurora’s performance stays consistent when the load increases.

### Database Engine Support
- RDS is compatible with MySQL, PostgreSQL, MariaDB, Microsoft SQL Server, and Oracle.

- Aurora is compatible with PostgreSQL and MySQL.


### Availability and Durability
- Aurora offers higher availability and better durability than RDS, due to its unique storage model, and ability to perform continuous backups and restore with a very low RPO (recovery point objective).

- In Aurora, data is durable by design. You always have multiple copies of your data. Every Aurora cluster has six storage nodes, spread across three AZs, even if you have just one compute node. In RDS, you have to max out your read replicas for this level of durability.


### Resiliency
- Aurora is more resilient than RDS because of its architecture design. It has fast recovery from failures. If a compute node crashes, Aurora can recover quickly. It can start new read replicas with minimal lag, and if the writer fails, another replica can be promoted to take over without waiting for the other nodes to reach consensus. All the shared state is in the data nodes, so failed nodes can be replaced almost immediately.

### Storage
- RDS storage auto scaling automatically scales storage capacity up to 64 TiB (except SQL Server’s 16 TiB) in response to growing database workloads, with zero downtime. With RDS Storage Auto Scaling, you simply set your desired maximum storage limit, and Auto Scaling takes care of the rest.

- Aurora automatically increases storage from a minimum of 10 GB to a maximum of 128 TiB. This is done in increments of 10 GB without any impact on the database performance. You are not required to provide the storage in advance.

### Scalability
- Vertical Scaling: Both, Aurora and RDS, allow you to scale the memory and compute resources up and down, to a maximum of 244 GiB of RAM and 32 vCPUs. Scaling operations can be done within a few clicks.

- Dynamic Scaling: Aurora Auto Scaling dynamically adjusts the number of Aurora Replicas provisioned for an Aurora DB cluster using single-master replication. It enables your Aurora DB cluster to handle sudden increases in connectivity or workload. When the connectivity or workload decreases, It removes unnecessary Aurora Replicas, so that you don’t pay for unused provisioned DB instances. RDS does not support such Auto Scaling.

### Replication
- RDS allows you to provision up to 5 replicas, and the process of replication is slower compared to Aurora.

- Aurora allows you to provision up to 15 replicas, and the replication is done in milliseconds.

- Aurora scales faster because it can add new read replicas quickly. Because replicas all use the shared storage volume, a new replica can serve queries almost immediately. It doesn’t have to wait to replicate data from the other nodes. Aurora does some asynchronous cache replication between nodes, but nothing synchronous. This reduces the inter-node I/O, which means Aurora can have more replicas.


### Failover
- In RDS, Failover to read replica is done manually, which could lead to data loss. You can use Multi-AZ (Standby instance) feature for automatic failover, and to prevent downtime and data loss.

- In Aurora, Failover to read replica is done automatically to prevent data loss. Failover time is faster on Aurora.

### Cluster Endpoints
- In RDS, there is a cluster endpoint which you use for your write queries. It is the DNS endpoint pointing to your current master db instance. During a failover, RDS routes this endpoint to the new master by a simple DNS change. However, for read replicas, you have to balance the load in your application using the instance endpoints. RDS does not provide a load balancer for read replicas.

- In Aurora, you still use cluster endpoint for your write queries. It also provides a reader endpoint acting as a load balancer for your read replicas. So you can use this endpoint for your read queries. In the case of a failover, one of the read replicas become master and is removed from this reader set.

### Pricing
Aurora is more expensive than RDS for the same workloads. Aurora pricing is mainly based on instance size and storage is billed according to actual usage.


### Backup
- RDS creates and saves automated backups of your DB instance during the backup window of your DB instance. RDS creates a storage volume snapshot of your DB instance, backing up the entire DB instance and not just individual databases according to the backup retention period that you specify. If necessary, you can recover your database to any point in time during the backup retention period. While the snapshot is being taken, storage I/O may be interrupted while data is copied, affecting database performance.

- Aurora backs up your cluster volume automatically and retains restore data for the length of the backup retention period. Aurora backups are continuous and incremental so you can quickly restore to any point within the backup retention period. No performance impact or interruption of database service occurs as backup data is being written.

###  Security: 
- AWS responsible for OS security, we are responsible for setting up KMS, security groups, IAM policies, authorizing users in DB, using SSL

## Aurora Global Database -
- Amazon Aurora Global Database is designed for globally distributed applications, allowing a single Amazon Aurora database to span multiple AWS regions. It replicates your data with no impact on database performance, enables fast local reads with low latency in each region, and provides disaster recovery from region-wide outages.
- We can have one primary and one secondary at least.
- At least one secondary AWS Region is required, but an Aurora global database can have up to five secondary AWS Regions.
- Aurora Global Database is designed for globally distributed applications, allowing a single Amazon Aurora database to span multiple AWS regions. It replicates your data with no impact on database performance, enables fast local reads with low latency in each region, and provides disaster recovery from region-wide outages.


## Aurora Multi-Master
- In a multi-master cluster, all DB instances have read/write capability. The notions of a single read/write primary instance and multiple read-only Aurora Replicas don’t apply. There isn’t any failover when a writer DB instance becomes unavailable, because another writer DB instance is immediately available to take over the work of the failed instance.

## Aurora Serverless
- Aurora Serverless lets you run Aurora without having to guess how many compute nodes you need. It automatically starts and stops nodes to match the needs of your application. It scales up to meet a spike in demand and scales down when things are quiet. The data remains in the shared storage volume, independent of any scaling.

### Recovery Point Objective (RPO) and Recovery Time Objective (RTO) -
- Recovery Point Objective (RPO) and Recovery Time Objective (RTO) are two important parameters of a disaster recovery or data protection plan.

- RPO describes the time duration in which your company may loose data before a disaster strikes. And, RTO describes the time duration that requires to recover data after an incident happens. Both RTO and RPO are measured in time, it could be in a minutes, hours, days or weeks.

- In a simple meaning, RTO is a time between last available backup and disaster where RPO is a time between disaster and systems recovery.

- Let’s say, RPO is 10 hours and the last available good copy of data is from 8 hours ago, then we are still within the parameters of the Business Continuity Plan’s RPO.

- If RTO is 10 hours (your business can survive with systems down for this amount of time), then you have to make sure that the system can be recovered quickly or within the time frame.




---
## A financial services company has a web application with an application tier running in the U.S and Europe. The database tier consists of a MySQL database running on Amazon EC2 in us-west-1. Users are directed to the closest application tier using Route 53 latency-based routing. The users in Europe have reported poor performance when running queries. Which changes should a Solutions Architect make to the database tier to improve performance?
### ANS -
- Migrate the database to an Amazon Aurora global database in MySQL compatibility mode. Configure the application tier in Europe to use the local reader endpoint.
- Amazon Aurora Global Database is designed for globally distributed applications, allowing a single Amazon Aurora database to span multiple AWS regions. It replicates your data with no impact on database performance, enables fast local reads with low latency in each region, and provides disaster recovery from region-wide outages. A global database can be configured in the European region and then the application tier in Europe will need to be configured to use the local database for reads/queries. The diagram below depicts an Aurora Global Database deployment.
