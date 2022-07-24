- RDS stands for Relational Database Service
- It’s a managed DB service for DB use SQL as a query language. 
- It allows you to create databases in the cloud that are managed by AWS like - Postgres, MySQL, MariaDB, Oracle, Microsoft SQL Server, Aurora (AWS Proprietary database)

### Advantage over using RDS versus deploying DB on EC2
- RDS is a managed service:
- Automated provisioning, OS patching
- Continuous backups and restore to specific timestamp (Point in Time Restore)!
- Monitoring dashboards
- Read replicas for improved read performance
- Multi AZ setup for DR (Disaster Recovery)
- Maintenance windows for upgrades
- Scaling capability (vertical and horizontal)
- Storage backed by EBS (gp2 or io1)
- BUT you can’t SSH into your instance

### RDS Backups
- Backups are automatically enabled in RDS
- Automated backups:
- Daily full backup of the database (during the maintenance window)
- Transaction logs are backed-up by RDS every 5 minutes
-  ability to restore to any point in time (from oldest backup to 5 minutes ago)
- 7 days retention (can be increased to 35 days)
### DB Snapshots:
- backup and snapshoot both are different things.
- Manually triggered by the user
- Retention of backup for as long as you want
### RDS Storage Auto Scaling -
- Helps you increase storage on your RDS DB instance dynamically
- When RDS detects you are running out of free database storage, it scales automatically
- Avoid manually scaling your database storage 
- You have to set Maximum Storage Threshold (maximum limit for DB storage)
- Automatically modify storage if:  Free storage is less than 10% of allocated storage, Low-storage lasts at least 5 minutes, 6 hours have passed since last modification 
- Useful for applications with unpredictable workloads 
- Supports all RDS database engines (MariaDB, MySQL, PostgreSQL, SQL Server, Oracle)

### RDS Read Replicas -
- Up to 5 Read Replicas ( 1 write and 5 read )
- Within AZ, Cross AZ or Cross Region
- Replication is ASYNC, so reads are eventually consistent ( Eventtually consistent means it will give outpyt before sync of every replicas )
- Replicas can be promoted to their own DB
- Applications must update the connection string to leverage read replicas.
- Assume we have one read and write ( main1) and three read replicas ( r1, r2, r3 ). Then data will be replicated from main1 to r1 then r1 to r2 then r2 to r3.
### RDS Read Replicas use cases -
- You have a production database that is taking on normal load
- You want to run a reporting application to run some analytics
- You create a Read Replica to run the new workload there
- The production application is unaffected
- Read replicas are used for SELECT (=read) only kind of statements (not INSERT, UPDATE, DELETE)

### RDS Read Replicas – Network Cost 
- In AWS there’s a network cost when data goes from one AZ to another 
- For RDS Read Replicas within the same region, you don’t pay that fee
- When read replicas are in same region then no replication fees, but when in different region then have to pay.
- Also no replivcation cost when replicas are present inside different az of same region.

### RDS Multi AZ (Disaster Recovery)
- SYNC replication
- Multi az means there is always a primary database which will work for write and read operation but there is also a standby ( not working for read and write ) database inside another az in same regions. data from primary db will be replicated sync to standby db. when primary db fails then standby will take place of primary and that will works as a primary db for read and write operation. After that another standby db will be created automatically.
- One DNS name – automatic app failover to standby
- Increase availability
- Failover in case of loss of AZ, loss of network, instance or storage failure
- No manual intervention in apps
- Not used for scaling
- Multi-AZ replication is free
- **Note:The Read Replicas be setup as Multi AZ for Disaster Recovery (DR)**
### RDS – move From Single-AZ to Multi-AZ -
- Zero downtime operation (no need to stop the DB)
- Just click on “modify” for the database
- The following happens internally:
- A snapshot is taken
- A new DB is restored from the snapshot in a new AZ
- Synchronization is established between the two databases

## RDS Security - Encryption
### At rest encryption
• Possibility to encrypt the master & read replicas with AWS KMS - AES-256 encryption
• Encryption has to be defined at launch time
• If the master is not encrypted, the read replicas cannot be encrypted
• Transparent Data Encryption (TDE) available for Oracle and SQL Server
### In-flight encryption
• SSL certificates to encrypt data to RDS in flight
• Provide SSL options with trust certificate when connecting to database
• To enforce SSL:
• PostgreSQL: rds.force_ssl=1 in the AWS RDS Console (Parameter Groups)
• MySQL: Within the DB: GRANT USAGE ON *.* TO 'mysqluser'@'%' REQUIRE SSL;
