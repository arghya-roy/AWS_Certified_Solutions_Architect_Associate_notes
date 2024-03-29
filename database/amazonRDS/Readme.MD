- It can support multi az read replica also means you can crate read replica inside multiple available zone in same region.
- RDS stands for Relational Database Service
- It’s a managed DB service for DB use SQL as a query language. 
- It allows you to create databases in the cloud that are managed by AWS like - Postgres, MySQL, MariaDB, Oracle, Microsoft SQL Server, Aurora (AWS Proprietary database)
-  Multi-Master is not supported by red ( supported by aurora )
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

### backup and aws snapshot -
- We can manually do snapshot.
- aws also has feature to backup automatically in backup window. So that is called backup. But in the background the aws backup is also creating snapshot.


### Recovery Point Objective (RPO) and Recovery Time Objective (RTO) -
- Recovery Point Objective (RPO) and Recovery Time Objective (RTO) are two important parameters of a disaster recovery or data protection plan.

- RPO describes the time duration in which your company may loose data before a disaster strikes. And, RTO describes the time duration that requires to recover data after an incident happens. Both RTO and RPO are measured in time, it could be in a minutes, hours, days or weeks.

- In a simple meaning, RTO is a time between last available backup and disaster where RPO is a time between disaster and systems recovery.

- Let’s say, RPO is 10 hours and the last available good copy of data is from 8 hours ago, then we are still within the parameters of the Business Continuity Plan’s RPO.

- If RTO is 10 hours (your business can survive with systems down for this amount of time), then you have to make sure that the system can be recovered quickly or within the time frame.

### RDS Read Replicas -
- Up to 5 Read Replicas ( 1 write and 5 read )
- In the backgroud RDS takes snapshot then create read only db from the snapshot.
- Within AZ, Cross AZ or Cross Region
- Replication is ASYNC, so reads are eventually consistent ( Eventtually consistent means it will give outpyt before sync of every replicas )
- Replicas can be promoted to their own DB
- Applications must update the connection string to leverage read replicas.
- Assume we have one read and write ( main1) and three read replicas ( r1, r2, r3 ). Then data will be replicated from main1 to r1 then r1 to r2 then r2 to r3.
- Read replicas can solve latency problem.
- But read replica does not give sub milisecond result. for that cases you can use elasticache.

### RDS Read Replicas use cases -
- You have a production database that is taking on normal load
- You want to run a reporting application to run some analytics
- You create a Read Replica to run the new workload there
- The production application is unaffected
- Read replicas are used for SELECT (=read) only kind of statements (not INSERT, UPDATE, DELETE)
- You cannot create an encrypted read replica of an unencrypted RDS DB.

### RDS Read Replicas – Network Cost 
- In AWS there’s a network cost when data goes from one AZ to another 
- For RDS Read Replicas within the same region, you don’t pay that fee
- When read replicas are in same region then no replication fees, but when in different region then have to pay.
- Also no replivcation cost when replicas are present inside different az of same region.
- You can create read replicas in different region

### RDS Multi AZ (Disaster Recovery)
- SYNC replication
- Multi az means there is always a primary database which will work for write and read operation but there is also a standby ( not working for read and write ) database inside another az in same regions. data from primary db will be replicated sync to standby db. when primary db fails then standby will take place of primary and that will works as a primary db for read and write operation. After that another standby db will be created automatically.
- One DNS name – automatic app failover to standby
- Increase availability
- Failover in case of loss of AZ, loss of network, instance or storage failure
- No manual intervention in apps
- Not used for scaling
- Multi-AZ replication is free
- You also cannot have an encrypted Multi-AZ standby instance of an unencrypted RDS DB.
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
- Possibility to encrypt the master & read replicas with AWS KMS - AES-256 encryption
- Encryption has to be defined at launch time
- If the master is not encrypted, the read replicas cannot be encrypted
- Transparent Data Encryption (TDE) available for Oracle and SQL Server
### In-flight encryption
- SSL certificates to encrypt data to RDS in flight
- Provide SSL options with trust certificate when connecting to database
- To enforce SSL: </br>
    PostgreSQL: rds.force_ssl=1 in the AWS RDS Console (Parameter Groups) </br>
    MySQL: Within the DB: GRANT USAGE ON *.* TO 'mysqluser'@'%' REQUIRE SSL; </br>
## RDS Encryption Operations
### Encrypting RDS backups
- Snapshots of un-encrypted RDS databases are un-encrypted
- Snapshots of encrypted RDS databases are encrypted
- Can copy a unencrypted snapshot into an encrypted one
### To encrypt an un-encrypted RDS database:
- Create a snapshot of the un-encrypted database
- Copy the snapshot and enable encryption for the snapshot
- Restore the database from the encrypted snapshot
- Migrate applications to the new database, and delete the old databas

## RDS Security – Network & IAM
### Network Security
- RDS databases are usually deployed within a private subnet, not in a public one
- RDS security works by leveraging security groups (the same concept as for EC2 
instances) – it controls which IP / security group can communicate with RDS
### Access Management
- IAM policies help control who can manage AWS RDS (through the RDS API)
- Traditional Username and Password can be used to login into the database
- IAM-based authentication can be used to login into RDS MySQL & PostgreSQL ( details in below )
#### RDS - IAM bases Authentication
- IAM database authentication works with MySQL and PostgreSQL
- You don’t need a password, just an authentication token obtained through IAM & RDS API calls
- Auth token has a lifetime of 15 minutes
- With MySQL, authentication is handled by AWSAuthenticationPlugin—an AWS-provided plugin that works seamlessly with IAM to authenticate your IAM users. Connect to the DB instance and issue the CREATE USER statement, as shown in the following example. </br>
`CREATE USER jane_doe IDENTIFIED WITH AWSAuthenticationPlugin AS 'RDS';`  </br>
The IDENTIFIED WITH clause allows MySQL to use the AWSAuthenticationPlugin to authenticate the database account (jane_doe). The AS 'RDS' clause refers to the authentication method, and the specified database account should have the same name as the IAM user or role. In this example, both the database account and the IAM user or role are named jane_doe.
- **Benefits:** </br>
    Network in/out must be encrypted using SSL </br>
    IAM to centrally manage users instead of DB </br>
    Can leverage IAM Roles and EC2 Instance profiles for easy integration </br>

## RDS Security – Summary 
### Encryption at rest:
- Is done only when you first create the DB instance
- or: unencrypted DB => snapshot => copy snapshot as encrypted => create DB from snapshot
### Your responsibility:
- Check the ports / IP / security group inbound rules in DB’s SG
- In-database user creation and permissions or manage through IAM
- Creating a database with or without public access
- Ensure parameter groups or DB is configured to only allow SSL connections
### AWS responsibility:
- No SSH access
- No manual DB patching
- No manual OS patching
- No way to audit the underlying instance

### About security group of restored db from snapshot -
- You can restore a DB instance to a specific point in time, creating a new DB instance. When you restore a DB instance to a point in time, the default DB security group is applied to the new DB instance. If you need custom DB security groups applied to your DB instance, you must apply them explicitly using the AWS Management Console, the AWS CLI modify-db-instance command, or the Amazon RDS API ModifyDBInstance operation after the DB instance is available.

---
## An Amazon RDS Read Replica is being deployed in a separate region. The master database is not encrypted but all data in the new region must be encrypted. How can this be achieved?
### ANS - 
- Encrypt a snapshot from the master DB instance, create a new encrypted master DB instance, and then create an encrypted cross-region Read Replica.
- You cannot create an encrypted Read Replica from an unencrypted master DB instance. You also cannot enable encryption after launch time for the master DB instance. Therefore, you must create a new master DB by taking a snapshot of the existing DB, encrypting it, and then creating the new DB from the snapshot. You can then create the encrypted cross-region Read Replica of the master DB.

## A company uses an Amazon RDS MySQL database instance to store customer order data. The security team have requested that SSL/TLS encryption in transit must be used for encrypting connections to the database from application servers. The data in the database is currently encrypted at rest using an AWS KMS key. How can a Solutions Architect enable encryption in transit?
### ANS -
- Download the AWS-provided root certificates. Use the certificates when connecting to the RDS DB instance.
- Amazon RDS creates an SSL certificate and installs the certificate on the DB instance when Amazon RDS provisions the instance. These certificates are signed by a certificate authority. The SSL certificate includes the DB instance endpoint as the Common Name (CN) for the SSL certificate to guard against spoofing attacks. You can download a root certificate from AWS that works for all Regions or you can download Region-specific intermediate certificates.
- You cannot use self-signed certificates with RDS.
## A company runs an application that uses an Amazon RDS PostgreSQL database. The database is currently not encrypted. A Solutions Architect has been instructed that due to new compliance requirements al.l existing and new data in the database must be encrypted. The database experiences high volumes of changes and no data can be lost. How can the Solutions Architect enable encryption for the database without incurring any data loss?
### ANS -
- Create a snapshot of the existing RDS DB instance. Create an encrypted copy of the snapshot. Create a new RDS DB instance from the encrypted snapshot and update the application. Use AWS DMS to synchronize data between the source and destination RDS DBs
- You cannot change the encryption status of an existing RDS DB instance. Encryption must be specified when creating the RDS DB instance. The best way to encrypt an existing database is to take a snapshot, encrypt a copy of the snapshot and restore the snapshot to a new RDS DB instance. This results in an encrypted database that is a new instance. Applications must be updated to use the new RDS DB endpoint. </br>
In this scenario as there is a high rate of change, the databases will be out of sync by the time the new copy is created and is functional. The best way to capture the changes between the source (unencrypted) and destination (encrypted) DB is to use AWS Database Migration Service (DMS) to synchronize the data.

## A Solutions Architect manages multiple Amazon RDS MySQL databases. To improve security, the Solutions Architect wants to enable secure user access with short-lived credentials. How can these requirements be met?
### ANS - 
- Create the MySQL user accounts to use the AWSAuthenticationPlugin with IAM.
