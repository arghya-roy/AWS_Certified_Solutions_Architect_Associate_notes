- Storage Gateway provides a standard set of storage protocols such as iSCSI, SMB, and NFS, which allow you to use AWS storage without rewriting your existing applications.
- Must read - https://digitalcloud.training/amazon-fsx/
- The iSCSI protocol is used by AWS Storage Gateway Volume Gateways.
- iSCSI-virtual tape library (VTL) protocol is used by AWS Storage tape Gateway.

### Overview 
- The AWS Storage Gateway service enables hybrid storage between on-premises environments and the AWS Cloud.

- It provides low-latency performance by caching frequently accessed data on premises, while storing data securely and durably in Amazon cloud storage services.

- Implemented using a virtual machine that you run on-premises (VMware or Hyper-V virtual appliance).

- Provides local storage resources backed by Amazon S3 and Glacier.

- Often used in disaster recovery preparedness to sync data to AWS.

- AWS Storage Gateway supports four storage interfaces: 
    - Amazon S3 File Gateway
    - Volume Gateway
    - Tape Gateway
    - Amazon FSx File Gateway

### File Gateway - ( also known as Amazon S3 File Gateway )
- Configured S3 buckets are accessible using the NFS and SMB protocol
- Supports S3 standard, S3 IA, S3 One Zone IA
- Bucket access using IAM roles for each File Gateway
- Most recently used data is cached in the file gateway
- Can be mounted on many servers
- Integrated with Active Directory (AD) for user authentication
- Store and access objects in Amazon S3 from NFS or SMB file data with local caching.
- Here File Gateway can "trick" your OS to "think" that S3 is a file system, but actually s3 is for object.


### Volume Gateway
- Block storage using iSCSI protocol backed by S3
- Backed by EBS snapshots which can help restore on-premises volumes!
- **Cached volumes:** low latency access to most recent data. Here a cache of the most frequently accessed data is cached on-site ( on -prem ). 
- **Stored volumes:** entire dataset is on premise, scheduled backups to S3
- Store and access iSCSI block storage volumes in Amazon S3.
- Here volume snapshot at first goes to s3, then using aws backup it creates ebs from the snapshot.
- See diagram of volume gateway -https://aws.amazon.com/storagegateway/volume/#:~:text=Volume%20Gateway%20offers%20cloud%2Dbacked,Hardware%20Appliance%20at%20your%20premises.



### Tape Gateway
- Some companies have backup processes using physical tapes (!)
- With Tape Gateway, companies use the same processes but, in the cloud
- Virtual Tape Library (VTL) backed by Amazon S3 and Glacier
- Back up data using existing tape-based processes (and iSCSI interface)
- Works with leading backup software vendors
- Store virtual tapes in Amazon S3 using iSCSI-VTL, and store archived tapes in Amazon S3 Glacier Flexible Retrieval or Amazon S3 Glacier Deep Archive.
- See diagram of tape gateway - https://aws.amazon.com/storagegateway/vtl/#:~:text=based%20backup%20workflows.-,Tape%20Gateway%20supports%20all%20leading%20backup%20applications%20and%20caches%20virtual,Storage%20Service%20(Amazon%20S3).


### Amazon FSx File Gateway
- Native access to Amazon FSx for Windows File Server
- Local cache for frequently accessed data
- Windows native compatibility (SMB, NTFS, Active Directory...) 
- Useful for group file shares and home directorie.
- We know that storage file gateway uses s3 to store files but here FSX file gateway uses fsx to store files.
- See diagram 
- ![alt text](http://url/to/img.png)



### Storage Gateway – Hardware appliance
- Using Storage Gateway means you need on-premises virtualization
- Otherwise, you can use a Storage Gateway Hardware Appliance
- You can buy it on amazon.com
- Works with File Gateway, Volume Gateway, Tape Gateway
- Has the required CPU, memory, network, SSD cache resources
- Helpful for daily NFS backups in small data centers




### Storage Gateway Exam Tips 

- Exam tip: Read the question well, it will hint at which gateway to use
- On-premises data to the cloud => Storage Gateway
- File access / NFS – user auth with Active Directory => File Gateway 
(backed by S3)
- Volumes / Block Storage / iSCSI => Volume gateway 
(backed by S3 with EBS snapshots)
- VTL Tape solution / Backup with iSCSI = > Tape Gateway
(backed by S3 and Glacier)
- No on-premises virtualization => Hardware Appliance

