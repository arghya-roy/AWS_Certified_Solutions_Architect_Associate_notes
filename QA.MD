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
