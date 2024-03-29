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
- **ALL HAVE 99.8 TO 99.9% DURABILITY AND 0.1 TO 0.2 % FAILUARE IN YEAR. ONLY  IO2 BLOCK EXPRESS  HAS 99.999% DURABILITY AND 0.001% YEARLY FAILURE.

### Provisioned IOPS SSD (io1) -
- Provisioned IOPS SSD (io1 and io2) volumes provide low latency and are designed to meet the needs of I/O-intensive workloads. They are best for EBS-optimized instances.
- Critical business applications with sustained IOPS performance
- Or applications that need more than 16,000 IOPS
- Max PIOPS: 64,000 for Nitro EC2 instances & 32,000 for other
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
- Max PIOPS: 64,000 for Nitro EC2 instances & 32,000 for other
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

## vvi ![image](https://user-images.githubusercontent.com/95282173/186339993-389fe5a1-58e7-41b5-b6a3-b87fed8773fb.png)


## EBS Encryption leverages keys from KMS (AES-256), SAME AS S3

## S3 storage availability and durability -
![image](https://user-images.githubusercontent.com/95282173/186341664-92123b54-d58e-48ce-8b14-2273f6866752.png)

## Important -
- Using s3 lifecycle we can go down only
- From standard and intellegent tier to standaed IA and one zone IA = We must have to wait at least 30 days using lifecycle rule.
- From standard and intellegent tier to any other = No need to wait
- from standard ia and onezone ia to any = 30 days have to wait
- from glacier instant and flexible retrival to below = 90 days to wait
- from glacier deep archive to other = 180 days to wait


## OSI model and AWS Service
- **Layer 1—Physical Layer** =
- **Layer 2—Data Link Layer** =
- **Layer 3—Network Layer ( ip, GENEVE )** =  Gateway load balancer, aws shield standard
- **Layer 4—Transport Layer ( TCP/UDP )** = Network load balancer, aws shield standard
- **Layer 5—Session Layer** =
- **Layer 6—Presentation Layer** =
- **Layer 7—Application Layer ( HTTP/ HTTPS )** =  Application load balancer, WAF, aws shield advanced


### Application Load Balancer (v2) Target Groups
- EC2 instances (can be managed by an Auto Scaling Group) – HTTP 
- ECS tasks (managed by ECS itself) – HTTP 
- Lambda functions – HTTP request is translated into a JSON event
- IP Addresses – must be private IPs
- ALB can route to multiple target groups
- Health checks are at the target group level


### Network Load Balancer (v2)
- Network load balancers (Layer 4) allow to:
   - Forward TCP & UDP traffic to your instances
   - Handle millions of request per seconds
   - Less latency ~100 ms (vs 400 ms for ALB)
- NLB has one static IP per AZ, and supports assigning Elastic IP
(helpful for whitelisting specific IP)
- NLB are used for extreme performance, TCP or UDP traffic
- Network Load Balancer –Target Groups
   - EC2 instances
   - IP Addresses – must be private IPs
   - Application Load Balancer

### Gateway Load Balancer
- Deploy, scale, and manage a fleet of 3rd party network virtual appliances in AWS
- Example: Firewalls, Intrusion Detection and Prevention Systems, Deep Packet Inspection Systems, payload manipulation
- Operates at Layer 3 (Network Layer) – IP ackets
- Before sending traffic to application NLB scan it using 3rd party network virtual appliances in AWS
- Combines the following functions:
    - Transparent Network Gateway – single entry/exit for all traffic
    - Load Balancer – distributes traffic to your virtual appliances
- Uses the GENEVE protocol on port 6081
- Gateway Load Balancer –Target Groups
    - EC2 instances
    - IP Addresses – must be private IPs

![WhatsApp Image 2022-08-24 at 12 50 49 PM](https://user-images.githubusercontent.com/95282173/186356130-0cd410f4-018a-4c32-8bee-83131e294f0b.jpeg)

### what is pass through mode ssl?
- SSL passthrough is the action of passing data through a load balancer to a server without decrypting it. Usually, the decryption or SSL termination happens at the load balancer and data is passed along to a web server as plain HTTP. But SSL passthrough keeps the data encrypted as it travels through the load balancer.
- You cannot use passthrough mode with an ALB and terminate SSL on the EC2 instances.

### You cannot use a HTTPS listener with an NLB.
### You cannot use a TCP listener with an ALB.
### AWS WAF – Web Application Firewall 
- deploy on 
    - Application Load Balancer
    - API Gateway
    - CloudFront
- Protects from common attack
   - SQL injection
   - Cross-Site Scripting (XSS)
   - OS command injection attacks
   - DDoS attacks ( layer 7 )

### Amazon GuardDuty
- It does not protect to from attacking, It notifies you after attack happended ( it come to know about attack by reading logs )
- Amazon GuardDuty is a threat detection service that continuously monitors your AWS accounts and workloads for malicious activity and delivers detailed security findings for visibility and remediation.
- Input data includes:
    - CloudTrail Events Logs – unusual API calls, unauthorized deployments
         - CloudTrail Management Events – create VPC subnet, create trail, …
         - CloudTrail S3 Data Events – get object, list objects, delete object, …
    - VPC Flow Logs – unusual internal traffic, unusual IP address
    - DNS Logs – compromised EC2 instances sending encoded data within DNS queries
    - Kubernetes Audit Logs – suspicious activities and potential EKS cluster compromises

## AWS Shield
- Protect against ddos attack.
### AWS Shield Standard:
- Free service that is activated for every AWS customer
- Provides protection from ddos attacks (such as SYN/UDP Floods - layer 4 transport, Reflection attacks - layrt 3 network ) on layer 3 ( network ) and layer 4 (transport) attacks.
- Dont have 24/7 access to AWS DDoS response team (DRP)
- It monitors network flow.
### AWS Shield Advanced:
- Optional DDoS mitigation service ($3,000 per month per organization)
- - It monitors network flow.
- Protect against more sophisticated and large attack on Amazon EC2, Elastic Load Balancing (ELB), Amazon CloudFront, AWS Global Accelerator, and Route 53
- 24/7 access to AWS DDoS response team (DRP)
- Protect against higher fees during usage spikes due to DDoS
- Provides protection from ddos attacks (such as SYN/UDP Floods - layer 4 transport, Reflection attacks - layrt 3 network, HTTPS flood and dns query flood - application layer 7 ) on layer 3 ( network ) and layer 4 (transport)and layer 7 ( application ) attacks.
- Include WAF in free of cost.
- need 1 year subscription commitment.


### S3 Encryption for Objects
- There are 4 methods of encrypting objects in S3
   - SSE-S3: encrypts S3 objects using keys handled & managed by AWS | Must set header: “x-amz-server-side-encryption": "AES256" | HTTP / HTTPS both
   - SSE-KMS: leverage AWS Key Management Service to manage encryption keys | Must set header: “x-amz-server-side-encryption": ”aws:kms" | KMS Advantages: user control + audit trail | HTTP / HTTPS both
   - SSE-C: when you want to manage your own encryption keys | HTTPS must be used
   - Client Side Encryption 


## EC2 Instance Types - see pdf page from 43 of S.M
### You can use cloudfront OAI only with s3. To get functionality like OAI in ELB or EC2 we have to change security group using lambda which will allow connection from cloudfront only. CLoudfront keep changes their internal IP. OAI is only possible with s3.

### Lead times are often longer than 1 month to establish a new connection of direct connection.
### to transfer data within 1 month - use snowball.

### You can use CloudFront to deliver video on demand (VOD) or live streaming video using any HTTP origin. One way you can set up video workflows in the cloud is by using CloudFront together with AWS Media Services.

### We can use cloudfront for static and dynamic content and on demand video and live streamig ( real time ). mainly use HTTP. 

### Global Accelerator is mainly for TCP or UDP like gaming.

### Cloudfront vs Global accelerator
- You can use CloudFront to deliver video on demand (VOD) or live streaming video using any HTTP origin. CloudFront improves performance for both cacheable content (such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery).

- Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions. 2 Anycast IP are created for your application. Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover. 

- both services integrate with AWS Shield for DDoS protection.

### The File Gateway backs off of Amazon S3 which has much higher availability and durability than EFS.

### Amazon RedShift cannot provide millisecond responsiveness. But dynamodb can provide millisecond responsiveness.

## Resiliency of direct connect -
### High Resiliency for Critical Workloads -
  one connection from each DX location to on prem.
  ![image](https://user-images.githubusercontent.com/95282173/186422630-580ea734-b3aa-425c-b249-a3f3848c8b44.png)
### Maximum Resiliency for Critical Workloads -
Two connection from each location to on prem
![image](https://user-images.githubusercontent.com/95282173/186422757-921c7476-51b4-40b5-bf5e-42a17def9417.png)

### Non-Critical Production Workloads or Development Workloads -
two connection from only one dx location to on-prem
![image](https://user-images.githubusercontent.com/95282173/186422983-955be12c-d789-4d7e-8a23-f0b4f9b6b68c.png)

### Multi-Region Resiliency
For additional resiliency, customers can also explore the use of multi-region failover. This can be done using Transit Gateway Cross Region peering and Direct Connect Gateway. One such implementation is explained in this blog https://aws.amazon.com/blogs/networking-and-content-delivery/influencing-traffic-over-hybrid-networks-using-longest-prefix-match/


## There is no standard metric in CloudWatch for collecting EC2 memory usage. However, you can use the CloudWatch agent to collect both system metrics and log files from Amazon EC2 instances and on-premises servers. The metrics can be pushed to a CloudWatch custom metric.

### Auto-scaling life cycle hook -
 Auto Scaling group lifecycle hooks enable you to perform custom actions as the Auto Scaling group launches or terminates instances. For example, you could install or configure software on newly launched instances, or download log files from an instance before it terminates.


### To reduce wait time / disk wait time in ec2 host database = increase iops means provisioned IOPS SSD (io1)

### To increase cpu performance in ec2 host database = change instance type

### EC2 Enhanced Networking (SR-IOV)
- Higher bandwidth, higher PPS (packet per second), lower latency
- Option 1: Elastic Network Adapter (ENA) up to 100 Gbps 
- Option 2: Intel 82599 VF up to 10 Gbps – LEGACY
### Elastic Fabric Adapter (EFA)
- Improved ENA for HPC, only works for Linux
- Great for inter-node communications, tightly coupled workloads
- Leverages Message Passing Interface (MPI) standard 
- Bypasses the underlying Linux OS to provide low-latency, reliable transport

### Elastic Network Adapter (ENA) is used to enhanced networking
