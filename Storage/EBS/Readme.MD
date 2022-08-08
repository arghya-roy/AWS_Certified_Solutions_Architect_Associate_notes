must read for snapshot and encryption sectrion- https://digitalcloud.training/amazon-ebs/#ebs-volume-types
For more aboyt ebs type read the slide of udemy from page 95 to 113

### IOPS - 
Input/output operations per second is an input/output performance measurement used to characterize computer storage devices like hard disk drives, solid state drives, and storage area networks.
### Throughput -
Throughput is the measure of the amount of data transferred from/to a storage device in a second. Typically stated in KB/MB/GB/s 


### EBS Volumes come in 6 types
- gp2 / gp3 (SSD): General purpose SSD volume that balances price and performance for 
a wide variety of workloads
- io1 / io2 (SSD): Highest-performance SSD volume for mission-critical low-latency or 
high-throughput workloads
- st1 (HDD): Low cost HDD volume designed for frequently accessed, throughput- intensive workloads
- sc1 (HDD): Lowest cost HDD volume designed for less frequently accessed workloads

###  For more read the slide of udemy from page 95 to 113


## Provisioned IOPS SSD
Provisioned IOPS SSD (io1 and io2) volumes provide low latency and are designed to meet the needs of I/O-intensive workloads. They are best for EBS-optimized instances.

- Critical business applications with sustained IOPS performance
- Or applications that need more than 16,000 IOPS
- Great for databases workloads (sensitive to storage perf and consistency)

### Provisioned IOPS SSD (io1) -
- Size 4 GiB to 16384 GiB. 
- 100 IOPS to 5000 IOPS and up to 50 IOPS per GiB
- Throughput (MiB/s) is Not applicable.
- EBS Multi-attach Supported
- Can be boot volume?	Yes
### Provisioned IOPS SSD (io2) -
- Size 4 GiB to 65536 GiB. 
- 100 IOPS to 100000 IOPS and up to 1000 IOPS per GiB
- Throughput (MiB/s) is Not applicable.
- EBS Multi-attach Supported
- Can be boot volume?	Yes


## General Purpose SSD -
General Purpose SSD (gp2 and gp3) volumes offer cost-effective storage that is ideal for a broad range of workloads.
### General Purpose SSD (gp2) - 
- Size 1 GiB to 16384 GiB. 
- 100 IOPS to 3000 IOPS and 3 IOPS per GiB.
- Throughput (MiB/s) is Not applicable
- EBS Multi-attach not Supported
- Can be boot volume?	Yes
### General Purpose SSD (gp3) - 
- Size 1 GiB to 16384 GiB. 
- 3000 IOPS to 16000 IOPS 
- Throughput (MiB/s) is 125 MiB to 1000 MiB and 125 MiB/s per TiB.
- EBS Multi-attach not Supported
- Can be boot volume?	Yes


## Throughput Optimized HDD
- Throughput Optimized HDD (st1) volumes provide low-cost magnetic storage that is a good fit for large, sequential workloads.
- Low-cost HDD volume, designed for frequently accessed. Throughput intensive workloads.
- Big Data, Data Warehouses, Log Processing
### Throughput Optimized HDD (st1) -
- Size 125 GiB to 16384 GiB. 
- IOPS is not applicable.
- Throughput (MiB/s) is 20 MiB to 123 MiB and 40 MiB/s per TiB.
- EBS Multi-attach not Supported
- Can be boot volume?	no

## Cold HDD
- Cold HDD (sc1) volumes provide low-cost magnetic storage that offers lower throughput than st1. sc1 is a good fit for large, sequential cold-data workloads that require infrequent access to data.
- Lowest cost HDD volume designed for less frequently accessed workloads
### Cold HDD (sc1) -
- Size 125 GiB to 16384 GiB. 
- IOPS is not applicable.
- Throughput (MiB/s) is 6 MiB/s to 40 MiB/s and 12 MiB/s per TiB.
- EBS Multi-attach not Supported
- Can be boot volume?	no

## Magnetic
Magnetic (standard) volumes are best suited for workloads where data is accessed infrequently.
### Magnetic (standard) -
- Size 1 GiB to 1024 GiB. 
- IOPS is Not applicable
- Throughput (MiB/s) is Not applicable
- EBS Multi-attach not Supported
- Can be boot volume?	no
--
- Data in transit between an instance and an encrypted volume is also encrypted.
- All EBS types and all instance families support encryption but not all instance types support encryption.

## A company has multiple AWS accounts for several environments (Prod, Dev, Test etc.). A Solutions Architect would like to copy an Amazon EBS snapshot from DEV to PROD. The snapshot is from an EBS volume that was encrypted with a custom key. What steps must be performed to share the encrypted EBS snapshot with the Prod account? (choose 2)
### ANS -
- Share the custom key used to encrypt the volume and Modify the permissions on the encrypted snapshot to share it with the Prod account.

## A Solutions Architect is attempting to clean up unused EBS volumes and snapshots to save some space and cost. How many of the most recent snapshots of an EBS volume need to be maintained to guarantee that you can recreate the full EBS volume from the snapshot?
### ANS -
- Only the most recent snapshot. Snapshots are incremental, but the deletion process will ensure that no data is lost.
## A Solutions Architect would like to implement a method of automating the creation, retention, and deletion of backups for the Amazon EBS volumes in an Amazon VPC. What is the easiest way to automate these tasks using AWS tools?
### ANS -
- Use the EBS Data Lifecycle Manager (DLM) to manage snapshots of the volumes
- "Create a scheduled job and run the AWS CLI command “create-snapshot” to take backups of the EBS volumes" is incorrect. This is not the easiest method, DLM would be a much better solution.
