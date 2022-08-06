
## General Purpose SSD -
General Purpose SSD (gp2 and gp3) volumes offer cost-effective storage that is ideal for a broad range of workloads.
### General Purpose SSD (gp2) - 
- Size 1 GiB to 16384 GiB. 
- 100 IOPS to 3000 IOPS and 3 IOPS per GiB.
- Throughput (MiB/s) is Not applicable
### General Purpose SSD (gp3) - 
- Size 1 GiB to 16384 GiB. 
- 3000 IOPS to 16000 IOPS 
- Throughput (MiB/s) is 125 MiB to 1000 MiB and 125 MiB/s per TiB.
## Provisioned IOPS SSD
Provisioned IOPS SSD (io1 and io2) volumes provide low latency and are designed to meet the needs of I/O-intensive workloads. They are best for EBS-optimized instances.
### Provisioned IOPS SSD (io1) -
- Size 4 GiB to 16384 GiB. 
- 100 IOPS to 5000 IOPS and up to 50 IOPS per GiB
- Throughput (MiB/s) is Not applicable.
### Provisioned IOPS SSD (io2) -
- Size 4 GiB to 65536 GiB. 
- 100 IOPS to 100000 IOPS and up to 1000 IOPS per GiB
- Throughput (MiB/s) is Not applicable.
## Cold HDD
Cold HDD (sc1) volumes provide low-cost magnetic storage that offers lower throughput than st1. sc1 is a good fit for large, sequential cold-data workloads that require infrequent access to data.
### Cold HDD (sc1) -
- Size 125 GiB to 16384 GiB. 
- IOPS is not applicable.
- Throughput (MiB/s) is 6 MiB/s to 40 MiB/s and 12 MiB/s per TiB.
## Throughput Optimized HDD
Throughput Optimized HDD (st1) volumes provide low-cost magnetic storage that is a good fit for large, sequential workloads.
### Throughput Optimized HDD (st1) -
- Size 125 GiB to 16384 GiB. 
- IOPS is not applicable.
- Throughput (MiB/s) is 20 MiB to 123 MiB and 40 MiB/s per TiB.
## Magnetic
Magnetic (standard) volumes are best suited for workloads where data is accessed infrequently.
### Magnetic (standard) -
- Size 1 GiB to 1024 GiB. 
- IOPS is Not applicable
- Throughput (MiB/s) is Not applicable
