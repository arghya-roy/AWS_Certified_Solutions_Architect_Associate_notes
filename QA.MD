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
