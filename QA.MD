## An application is running on Amazon EC2 behind an Elastic Load Balancer (ELB). Content is being published using Amazon CloudFront and you need to restrict the ability for users to circumvent CloudFront and access the content directly through the ELB. How can you configure this solution?
- **ANS** Create a VPC Security Group for the ELB and use AWS Lambda to automatically update the CloudFront internal service IP addresses when they change
- The only way to get this working is by using a VPC Security Group for the ELB that is configured to allow only the internal service IP ranges associated with CloudFront. As these are updated from time to time, you can use AWS Lambda to automatically update the addresses. This is done using a trigger that is triggered when AWS issues an SNS topic update when the addresses are changed.

## An application stores transactional data in an Amazon S3 bucket. The data is analyzed for the first week and then must remain immediately available for occasional analysis. What is the MOST cost-effective storage solution that meets the requirements?
- **ANS** Configure a lifecycle policy to transition the objects to Amazon S3 Standard-Infrequent Access (S3 Standard-IA) after 30 days. ( we have to wait at least 30 days to move data to standard IA.).
- Configure a lifecycle policy to transition the objects to Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA) after 30 days" is incorrect Because the question says that **must remain** means there should be high availability.

## A company has acquired another business and needs to migrate their 50TB of data into AWS within 1 month. They also require a secure, reliable and private connection to the AWS cloud. How are these requirements best accomplished?

- **ANS** Migrate data using AWS Snowball. Provision an AWS VPN initially and order a Direct Connect link.
- AWS Direct Connect provides a secure, reliable and private connection. However, lead times are often longer than 1 month so it cannot be used to migrate data within the timeframes. Therefore, it is better to use AWS Snowball to move the data and order a Direct Connect connection to satisfy the other requirement later on. In the meantime the organization can use an AWS VPN for secure, private access to their VPC.
- Because set up of direct connect will take moee than 1 month

## A Solutions Architect is designing a web application that runs on Amazon EC2 instances behind an Elastic Load Balancer. All data in transit must be encrypted. Which solution options meet the encryption requirement? (choose 2)
- Use a Network Load Balancer (NLB) with a TCP listener, then terminate SSL on EC2 instances
- Use an Application Load Balancer (ALB) with an HTTPS listener, then install SSL certificates on the ALB and EC2 instances.

## A solutions architect is optimizing a website for real-time streaming and on-demand videos. The website’s users are located around the world and the solutions architect needs to optimize the performance for both the real-time and on-demand streaming. Which service should the solutions architect choose?
- **ANS** AWS Cloudfront
- amazon CloudFront can be used to stream video to users across the globe using a wide variety of protocols that are layered on top of HTTP. This can include both on-demand video as well as real time streaming video.
- "AWS Global Accelerator" is incorrect as this would be an expensive way of getting the content closer to users compared to using CloudFront. As this is a use case for CloudFront and there are so many edge locations it is the better option.

## An organization is migrating data to the AWS cloud. An on-premises application uses Network File System shares and must access the data without code changes. The data is critical and is accessed frequently. Which storage solution should a Solutions Architect recommend to maximize availability and durability?

- AWS Storage Gateway – File Gateway
- AWS EFS is wrong because as per the qurstion still on prem application will access it. So for hybrid cases we will use AWS Storage Gateway – File Gateway. Also the solution asks to maximize availability and durability. The File Gateway backs off of Amazon S3 which has much higher availability and durability than EFS which is why it is the best solution for this scenario.
-  "Amazon Simple Storage Service - S3" is incorrect. Amazon S3 does not offer an NFS interface.

## An IoT sensor is being rolled out to thousands of a company’s existing customers. The sensors will stream high volumes of data each second to a central location. A solution must be designed to ingest and store the data for analytics. The solution must provide near-real time performance and millisecond responsiveness. Which solution should a Solutions Architect recommend?

- Ingest the data into an Amazon Kinesis Data Stream. Process the data with an AWS Lambda function and then store the data in Amazon DynamoDB
- "Ingest the data into an Amazon Kinesis Data Stream. Process the data with an AWS Lambda function and then store the data in Amazon RedShift" is incorrect. Amazon RedShift cannot provide millisecond responsiveness.

## A solutions architect has been tasked with designing a highly resilient hybrid cloud architecture connecting an on-premises data center and AWS. The network should include AWS Direct Connect (DX). Which DX configuration offers the HIGHEST resiliency?
- **ANS** Configure DX connections at multiple DX locations
- "Configure a DX connection with an encrypted VPN on top of it" is incorrect. A VPN that is separate to the DX connection can be a good backup. But a VPN on top of the DX connection does not help. Also, encryption provides security but not resilience.
-  "Configure multiple public VIFs on top of a DX connection" is incorrect. Virtual interfaces do not add resiliency as resiliency must be designed into the underlying connection.
-  "Configure multiple private VIFs on top of a DX connection" is incorrect. Virtual interfaces do not add resiliency as resiliency must be designed into the underlying connection.

## A company runs an internal browser-based application. The application runs on Amazon EC2 instances behind an Application Load Balancer. The instances run in an Amazon EC2 Auto Scaling group across multiple Availability Zones. The Auto Scaling group scales up to 20 instances during work hours, but scales down to 2 instances overnight. Staff are complaining that the application is very slow when the day begins, although it runs well by mid-morning. How should the scaling be changed to address the staff complaints and keep costs to a minimum?
- A. Implement a scheduled action that sets the desired capacity to 20 shortly before the office opens.
- B. Implement a step scaling action triggered at a lower CPU threshold, and decrease the cooldown period.
- **C. Implement a target tracking action triggered at a lower CPU threshold, and decrease the cooldown period.** ( ANS )
- D. Implement a scheduled action that sets the minimum and maximum capacity to 20 shortly before the office opens.

- details 
     - Answers A & D are incorrect because the question states to keep costs to a minimum.
This means, NOT running 20 instances from the start.

## A social gaming startup has its flagship application hosted on a fleet of EC2 servers running behind an Elastic Load Balancer. These servers are part of an Auto Scaling Group. 90% of the users start logging into the system at 6 pm every day and continue till midnight. The engineering team at the startup has observed that there is a significant performance lag during the initial hour from 6 pm to 7 pm. The application is able to function normally thereafter. As a solutions architect, which of the following steps would you recommend addressing the performance bottleneck during that initial hour of traffic spike?

- **ANS** Configure your Auto Scaling group by creating a scheduled action that kicks-off before 6 pm. This causes the scale-out to happen even before peak traffic kicks in at 6 pm
- Configure your Auto Scaling group by creating a target tracking policy. This causes the scale-out to happen even before peak traffic kicks in at 6 pm. It is in correct because it will not scale out before 6 pm.


## An application is hosted on the U.S west coast. Users there have no problems, but users on the east coast are experiencing performance issues. The users have reported slow response times with the search bar autocomplete and display of account listings. How can you improve the performance for users on the east coast?

- **ANS** Create an ElastiCache database in the U.S east region
- This is not static content, So can not host to s3.


## You have created a file system using Amazon Elastic File System (EFS) which will hold home directories for users. What else needs to be done to enable users to save files to the EFS file system?

- Create a subdirectory for each user and grant read-write-execute permissions to the users. Then mount the subdirectory to the users’ home directory

## An application launched on Amazon EC2 instances needs to publish personally identifiable information (PII) about customers using Amazon SNS. The application is launched in private subnets within an Amazon VPC. Which is the MOST secure way to allow the application to access service endpoints in the same region?

- AWS Privatelink
- To publish messages to Amazon SNS topics from an Amazon VPC, create an interface VPC endpoint. Then, you can publish messages to SNS topics while keeping the traffic within the network that you manage with the VPC. This is the most secure option as traffic does not need to traverse the Internet.

## A company runs a number of core enterprise applications in an on-premises data center. The data center is connected to an Amazon VPC using AWS Direct Connect. The company will be creating additional AWS accounts and these accounts will also need to be quickly, and cost-effectively connected to the on-premises data center in order to access the core applications. What deployment changes should a Solutions Architect implement to meet these requirements with the LEAST operational overhead?
- Configure AWS Transit Gateway between the accounts. Assign Direct Connect to the transit gateway and route network traffic to the on-premises servers
- "Create a Direct Connect connection in each new account. Route the network traffic to the on-premises servers" is incorrect. This is an expensive solution as you would need to have multiple Direct Connect links.

## A company runs an application on Amazon EC2 instances which requires access to sensitive data in an Amazon S3 bucket. All traffic between the EC2 instances and the S3 bucket must not traverse the internet and must use private IP addresses. Additionally, the bucket must only allow access from services in the VPC. Which combination of actions should a Solutions Architect take to meet these requirements? (Select TWO.)
- Create a VPC endpoint for Amazon S3
- Apply a bucket policy to restrict access to the S3 endpoint

## A company has divested a single business unit and needs to move the AWS account owned by the business unit to another AWS Organization. How can this be achieved?

- Migrate the account using the AWS Organizations console" is the correct answer.
- "Migrate the account using AWS CloudFormation" is incorrect. You do not need to use AWS CloudFormation. You can use the Organizations API or AWS CLI for when there are many accounts to migrate and therefore you could use CloudFormation for any additional automation but it is not necessary for this scenario.

## An application upgrade caused some issues with stability. The application owner enabled logging and has generated a 5 GB log file in an Amazon S3 bucket. The log file must be securely shared with the application vendor to troubleshoot the issues. What is the MOST secure way to share the log file?

- Generate a presigned URL and ask the vendor to download the log file before the URL expires" is the correct answer.
- A presigned URL gives you access to the object identified in the URL. When you create a presigned URL, you must provide your security credentials and then specify a bucket name, an object key, an HTTP method (PUT for uploading objects), and an expiration date and time. The presigned URLs are valid only for the specified duration. That is, you must start the action before the expiration date and time.
- "Create an IAM user for the vendor to provide access to the S3 bucket and the application. Enforce multi-factor authentication" is incorrect. This is less secure as you have to create an account to access AWS and then ensure you lock down the account appropriately.

## A Solutions Architect must select the most appropriate database service for two use cases. A team of data scientists perform complex queries on a data warehouse that take several hours to complete. Another team of scientists need to run fast, repeat queries and update dashboards for customer support staff. Which solution delivers these requirements MOST cost-effectively?

-  "RedShift for both use cases" is the correct answer.
-  RedShift is a columnar data warehouse DB that is ideal for running long complex queries. RedShift can also improve performance for repeat queries by caching the result and returning the cached result when queries are re-run. Dashboard, visualization, and business intelligence (BI) tools that execute repeat queries see a significant boost in performance due to result caching.

## Amazon s3 for cold storage means glacier, glacier archive etc.

## A solutions architect is finalizing the architecture for a distributed database that will run across multiple Amazon EC2 instances. Data will be replicated across all instances so the loss of an instance will not cause loss of data. The database requires block storage with low latency and throughput that supports up to several million transactions per second per server. Which storage solution should the solutions architect use?
- Amazon EC2 instance store **because question is saying that "loss of an instance will not cause loss of data"**

## An AWS workload in a VPC is running a legacy database on an Amazon EC2 instance. Data is stored on a 2000GB Amazon EBS (gp2) volume. At peak load times, logs show excessive wait time. What should be implemented to improve database performance using persistent storage?

- **ANS** Migrate the data on the EBS volume to provisioned IOPS SSD (io1)
- "Change the EC2 instance type to one with burstable performance" is incorrect. Burstable performance instances provide a baseline of CPU performance with the ability to burst to a higher level when required. However, the issue in this scenario is disk wait time, not CPU performance, therefore we need to improve I/O not CPU performance.
- "Change the EC2 instance type to one with EC2 instance store volumes" is incorrect. Using an instance store volume may provide high performance but the data is not persistent so it is not suitable for a database.
-  "Migrate the data on the Amazon EBS volume to an SSD-backed volume" is incorrect as the data is already on an SSD-backed volume (gp2).


### To reduce wait time / disk wait time in ec2 host database = increase iops means provisioned IOPS SSD (io1)

### To increase cpu performance in ec2 host database = change instance type





