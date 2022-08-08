- EFS uses NFS (Network File System) protocol and FsX uses SMB (Server Message Block) protocol.
- EFS and FsX both are file system not block.
- Mainly EFS for linux, Fsx for windows.
- Windows file server farm uses Distributed File System Replication (DFSR) = FSX 
- Must read - https://digitalcloud.training/amazon-fsx/

### Amazon FSx for Lustre used for Machine Learning, High Performance Computing (HPC), Video Processing, Financial Modeling, Electronic Design Automation, S3 integration.

## Amazon FsX
- Amazon FSx provides fully managed third-party file systems.

- Amazon FSx provides you with the native compatibility of third-party file systems with feature sets for workloads such as Windows-based storage, high-performancecomputing (HPC), machine learning, and electronic design automation (EDA).

- You don’t have to worry about managing file servers and storage, as Amazon FSx automates the time-consuming administration tasks such as hardware provisioning, software configuration, patching, and backups.

- Amazon FSx integrates the file systems with cloud-native AWS services, making them even more useful for a broader set of workloads.

- Amazon FSx provides you with four file systems to choose from:

      - Amazon FSx for Windows File Server for Windows-based applications
      - Amazon FSx for Lustre for compute-intensive workloads.
      - Amazon FSx for NetApp ONTAP.
      - Amazon FSX for OpenZFS.
This article concentrates on FSx for Windows File Server and FSx for Lustre as these are the only file systems currently featuring on exams.

### Amazon FSx for Windows (File Server) 
- EFS is a shared POSIX system for Linux systems.
- FSx for Windows is a fully managed Windows file system share drive 
- Supports SMB protocol & Windows NTFS 
- Microsoft Active Directory integration, ACLs, user quotas 
- Can be mounted on Linux EC2 instances 
- Scale up to 10s of GB/s, millions of IOPS, 100s PB of data • Storage Options: 
- SSD – latency sensitive workloads (databases, media processing, data analytics, …) 
- HDD – broad spectrum of workloads (home directory, CMS, …) 
- Can be accessed from your on-premises infrastructure (VPN or Direct Connect) 
- Can be configured to be Multi-AZ (high availability) 
- Data is backed-up daily to S3

### Amazon FSx for Lustre 

- Lustre is a type of parallel distributed file system, for large-scale computing
- The name Lustre is derived from “Linux” and “cluster
- Machine Learning, High Performance Computing (HPC)
- Video Processing, Financial Modeling, Electronic Design Automation
- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies
- Storage Options:
     - SSD – low-latency, IOPS intensive workloads, small & random file operations
     - HDD – throughput-intensive workloads, large & sequential file operations
- Seamless integration with S3
     - Can “read S3” as a file system (through FSx)
     - Can write the output of the computations back to S3 (through FSx)
- Can be used from on-premises servers (VPN or Direct Connect


### FSx File System Deployment Options
- Scratch File System
     - Temporary storage
     - Data is not replicated (doesn’t persist if file server fails)
     - High burst (6x faster, 200MBps per TiB)
     - Usage: short-term processing, optimize costs
- Persistent File System
     - Long-term storage
     - Data is replicated within same AZ 
     - Replace failed files within minutes
     - Usage: long-term processing, sensitive data

