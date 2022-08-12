## AWS Snow Family -
- Highly-secure, portable devices to collect and process data at the edge, and migrate data into and out of AWS
- We can use AWS snow familt in two ways -
     - Data Migration
     - Edge computing
- AWS Snow Family: offline devices to perform data migrations
- If it takes more than a week to transfer over the network, use Snowball devices!
- amazon puts all data to s3 from snowball

### Data Migration
- Snowcone 
- Snowball Edge
- Snowmobile ( truck )

### Edge computing 
- Snowcone 
- Snowball Edge


### Data Migrations challenges without AWS Snow Family
- Limited connectivity
- Limited bandwidth
- High network cost
- Shared bandwidth (can’t maximize the line)
- Connection stability



### AWS Snowcone 
- Small, portable computing, anywhere, rugged & secure, withstands harsh environments
- Light (4.5 pounds, 2.1 kg) 
- mgration upto TB. ( less than PB, 1 PB = 1000 TB ) 
- Device used for edge computing, storage, and data transfer
- 8 TBs of usable storage 
- Use Snowcone where Snowball does not fit (space constrained environment)
- Must provide your own battery / cables 
- Can be sent back to AWS offline, or connect it to internet and use AWS DataSync to send data


### Snowball Edge (for data transfers) 
- Physical data transport solution: move TBs or PBs of data in or out
of AWS
- mgration upto  10 PB.
- Alternative to moving data over the network (and paying network
fees)
- Pay per data transfer job 
- Provide block storage and Amazon S3 compatible object storage
- Snowball can be classified in two types 
    - **Snowball Edge Storage Optimized**
       - 80 TB of HDD capacity for block volume and S3 compatible object storage
    - **Snowball Edge Compute Optimized**
       - 42 TB of HDD capacity for block volume and S3 compatible object storage
- Use cases: large data cloud migrations, DC decommission, disaster recovery


### AWS Snowmobile

- Transfer exabytes of data (1 EB = 1,000 PB = 1,000,000 TBs)
- Each Snowmobile has 100 PB of capacity (use multiple in parallel)
- High security: temperature controlled, GPS, 24/7 video surveillance
- Better than Snowball if you transfer more than 10 PB


## What is Edge Computing? 
- Process data while it’s being created on an edge location
- edge location can be a truck on the road, a ship on the sea, a mining station underground
- We setup a Snowball Edge / Snowcone device to do edge computing
- Use cases of Edge Computing:
     - Preprocess data
     - Machine learning at the edge
     - Transcoding media streams
• Eventually (if need be) we can ship back the device to AWS (for transferring data for example)


## Snow Family – Edge Computing
### Snowcone (smaller)
- 2 CPUs, 4 GB of memory, wired or wireless access
- USB-C power using a cord or the optional battery
- Can run EC2 Instances & AWS Lambda functions (using AWS IoT Greengrass)
- Long-term deployment options: 1 and 3 years discounted pricing

### Snowball Edge – Compute Optimized
- 52 vCPUs, 208 GiB of RAM
- Optional GPU (useful for video processing or machine learning)
- 42 TB usable storage
- Can run EC2 Instances & AWS Lambda functions (using AWS IoT Greengrass)
- Long-term deployment options: 1 and 3 years discounted pricing

### Snowball Edge – Storage Optimized
- Up to 40 vCPUs, 80 GiB of RAM
- Object storage clustering available
- Can run EC2 Instances & AWS Lambda functions (using AWS IoT Greengrass)
- Long-term deployment options: 1 and 3 years discounted pricing























### AWS Snowball Edge -
AWS Snowball Edge is a type of Snowball device with on-board storage and compute power for select AWS capabilities. Snowball Edge can do local processing and edge-computing workloads in addition to transferring data between your local environment and the AWS Cloud. 
--
## A company has 200 TB of video files stored in an on-premises data center that must be moved to the AWS Cloud within the next four weeks. The company has around 50 Mbps of available bandwidth on an Internet connection for performing the transfer. What is the MOST cost-effective solution for moving the data within the required timeframe?
### ANS -
- Order multiple AWS Snowball devices to migrate the data to AWS.
- To move 200 TB of data over a 50 Mbps link would take over 300 days. Therefore, the solution must avoid the Internet link. The most cost-effective solution is to use multiple AWS Snowball devices to migrate the data to AWS. Snowball devices are shipped to your data center where you can load the data and then ship it back to AWS. This avoids the Internet connection and utilizes local high-bandwidth network connections to load the data.
- "Use Amazon S3 Transfer Acceleration to securely upload the data" is incorrect. This would use the Internet link and would not meet the required timeframe.
- "Create a virtual private gateway and connect a VPN to upload the data" is incorrect. This would also use the Internet link and would not meet the required timeframe.
- "Use AWS Snowmobile to migrate the data to AWS" is incorrect. This is a very large device on the back of a truck that is used for moving huge quantities of data. It would be very expensive for moving just 200 TB of data.

## A team of scientists are collecting environmental data to assess the impact of pollution in a small regional town. The scientists collect data from various sensors and cameras. The data must be immediately processed to validate its accuracy, but the scientists have limited local storage space on their laptops and intermittent and unreliable connectivity to their Amazon EC2 instances and S3 buckets. What should a Solutions Architect recommend?
### ANS -
- Use AWS Snowball Edge devices to process the data locally.
- "Use AWS DataSync on the scientists’ laptops to synchronize the data to Amazon S3. Process the data with Amazon EC2 instances" is incorrect. Due to the unreliable connectivity this does not solve the problem.
- AWS Snowball Edge is a type of Snowball device with on-board storage and compute power for select AWS capabilities. Snowball Edge can do local processing and edge-computing workloads in addition to transferring data between your local environment and the AWS Cloud. You can run Amazon EC2 compute instances on a Snowball Edge device using the Amazon EC2 compatible endpoint, which supports a subset of the Amazon EC2 API operations. Data can subsequently be transferred to Amazon S3 for storage and additional processing.
