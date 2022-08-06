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
