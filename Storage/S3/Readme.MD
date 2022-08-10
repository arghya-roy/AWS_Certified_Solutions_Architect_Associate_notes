### S3 bucket - 
- Amazon S3 allows people to store objects (files) in “buckets” (directories)
- Buckets must have a globally unique name
- Buckets are defined at the region level
- Naming convention
    - No uppercase
    - No underscore
    - 3-63 characters long
    - Not an IP
    - Must start with lowercase letter or number
- There’s no concept of “directories” within buckets
(although the UI will trick you to think otherwise)
- Objects (files) have a Key 
- The key is the FULL path: 
    - s3://my-bucket/my_file.txt 
    - s3://my-bucket/my_folder1/another_folder/my_file.txt 
- The key is composed of prefix + object name 
    - s3://my-bucket/my_folder1/another_folder/my_file.txt
   
- Max Object Size is 5TB (5000GB)
- If uploading more than 5GB, must use “multi-part upload”

### Versioning -
I know this

## S3 Encryption for Objects -
- There are 4 methods of encrypting objects in S3 ( 3 server side and  client side )
   - server side encryption
     - SSE-S3: encrypts S3 objects using keys handled & managed by AWS
     - SSE-KMS: leverage AWS Key Management Service to manage encryption keys
     - SSE-C: when you want to manage your own encryption keys
   - Client Side Encryption 
     
### SSE-S3  ( encryption happens in bucket but key is managed by s3 )
- SSE-S3: encryption using keys handled & managed by Amazon S3
- Object is encrypted server side
- AES-256 encryption type
- Must set header: `"x-amz-server-side-encryption": "AES256"`
- HTTP or HTTPS both can be used

### SSE-KMS ( encryption happens in bucket but key is managed by KMS, This key is CMK means  Customer Master Key )

- SSE-KMS: encryption using keys handled & managed by KMS
- KMS Advantages: user control + audit trail
- Object is encrypted server side
- Must set header: `"x-amz-server-side-encryption": "aws:kms"`
- HTTP or HTTPS both can be used

### SSE-C ( encryption happens in bucket but key is managed by client )
- SSE-C: server-side encryption using data keys fully managed by the customer outside of AWS
- Amazon S3 does not store the encryption key you provide
- Encryption key must provided in HTTP headers, for every HTTP request made
- HTTPS must be used

### Client Side Encryption ( encryption happens in outside bucket, encrypted object comes )
- Client library such as the Amazon S3 Encryption Client 
- Clients must encrypt data themselves before sending to S3 
- Clients must decrypt data themselves when retrieving from S3 
- Customer fully manages the keys and encryption cycle

## Encryption in transit (SSL/TLS)
- Amazon S3 exposes:
   - HTTP endpoint: non encrypted
   - HTTPS endpoint: encryption in flight
- You’re free to use the endpoint you want, but HTTPS is recommended
- Most clients would use the HTTPS endpoint by default

## S3 Websites -
- S3 can host static websites and have them accessible on the www
- The website URL will be:
    - <bucket-name>.s3-website-<AWS-region>.amazonaws.com
     OR
    - <bucket-name>.s3-website.<AWS-region>.amazonaws.com
- If you get a 403 (Forbidden) error, make sure the bucket policy allows
public reads!

## S3 CORS -
- CORS means Cross-Origin Resource Sharing
- Suppose we have one .html file in a bucket and that html file calling a image from another bucket, after that the image will be visible to user. This process is called Cross-Origin Resource Sharing.
- To do this we have to follow below steps -
     - allow for a specific origin or for * (all origins) in 2nd bucket ( so 1st bucket can access 2nd buckets objects )
     - When we call to 2nd bucket from 1st bucket's html then we have to add **Access-Control-Allow-Origin** header


## Amazon S3 - Consistency Model
- amazon s3 shows Strong consistency
- means After a successful write of a new object (new PUT) subsequent read request immediately receives the latest version of the object
(read after write consistency)


## S3 MFA-Delete
- MFA (multi factor authentication) forces user to generate a code on a device (usually a mobile phone or hardware) before doing important operations on S3
- To use MFA-Delete, enable Versioning on the S3 bucket
- You will need MFA to
    - permanently delete an object version
    - suspend versioning on the bucket
- You won’t need MFA for
    - enabling versioning
    - listing deleted versions
- Only the bucket owner (root account) can enable/disable MFA-Delete
- MFA-Delete currently can only be enabled using the CLI


## S3 Replication (CRR & SRR)
- Cross Region Replication (CRR)
- Same Region Replication (SRR)
- CRR - Use cases: compliance, lower latency access, replication across accounts
- SRR – Use cases: log aggregation, live replication between production and test accounts
- After activating, only new objects are replicated
- Optionally, you can replicate existing objects using S3 Batch Replication
- For DELETE operations:
    - Can replicate delete markers from source to target (optional setting)
    - Deletions with a version ID are not replicated (to avoid malicious deletes)

## S3 Pre-Signed URLs
- will generate a url which has a time limit to access object.
- Can generate pre-signed URLs using SDK or CLI
     - For downloads (easy, can use the CLI)
     - For uploads (harder, must use the SDK)
- Valid for a default of 3600 seconds, can change timeout with --expires-in
[TIME_BY_SECONDS] argument

- Users given a pre-signed URL inherit the permissions of the person who generated the URL for GET / PUT
- Examples :
     - Allow only logged-in users to download a premium video on your S3 bucket
     - Allow an ever changing list of users to download files by generating URLs dynamically
     - Allow temporarily a user to upload a file to a precise location in our bucket
     
     
## S3 Storage Classes
- **Read pdf 303 to 308
- Amazon S3 Standard - General Purpose
- Amazon S3 Standard-Infrequent Access (IA)
- Amazon S3 One Zone-Infrequent Access
- Amazon S3 Glacier Instant Retrieval
- Amazon S3 Glacier Flexible Retrieval
- Amazon S3 Glacier Deep Archive
- Amazon S3 Intelligent Tiering


## S3 Durability and Availability
- Durability:
     - High durability (99.999999999%, 11 9’s) of objects across multiple AZ
     - If you store 10,000,000 objects with Amazon S3, you can on average expect to incur a loss of a single object once every 10,000 years
     - Same for all storage classes
- Availability:
     - Measures how readily available a service is
     - Varies depending on storage class
     - Example: S3 standard has 99.99% availability = not available 53 minutes a year


## S3 Analytics – Storage Class Analysis
- You can setup S3 Analytics to help determine when to transition objects
from Standard to Standard_IA
- Does not work for ONEZONE_IA or GLACIER
- Report is updated daily
- Takes about 24h to 48h hours to first start
- Good first step to put together Lifecycle Rules (or improve them)!

## S3 – Baseline Performance

- Amazon S3 automatically scales to high request rates, latency 100-200 ms
- Your application can achieve at least 3,500 PUT/COPY/POST/DELETE and
5,500 GET/HEAD requests per second per prefix in a bucket.
- There are no limits to the number of prefixes in a bucket.
- Example (object path => prefix):
     - bucket/folder1/sub1/file => /folder1/sub1/
     - bucket/folder1/sub2/file => /folder1/sub2/
     - bucket/1/file => /1/
     - bucket/2/file => /2/
- If you spread reads across all four prefixes evenly, you can achieve 22,000
requests per second for GET and HEAD

## S3 – KMS Limitation
- If you use SSE-KMS, you may be impacted by the KMS limits
- When you upload, it calls the GenerateDataKey KMS API
- When you download, it calls the Decrypt KMS API
- Count towards the KMS quota per second (5500, 10000, 30000 req/s based on region)
- You can request a quota increase using the Service Quotas Console


## S3 Performance

###  Multi-Part upload:
- recommended for files > 100MB, must use for files > 5GB
- Can help parallelize uploads (speed up transfers)

### Amazon S3 Transfer Acceleration -
Amazon S3 Transfer Acceleration is a bucket-level feature that enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket. Transfer Acceleration is designed to optimize transfer speeds from across the world into S3 buckets.

### S3 Byte-Range Fetches
- Means you can get partial object.
- you can call it by specific bytes.
- If you need only header of a object then you only call those bytes which contain header.


## S3 Event Notifications -
We can sent all enent or specific event to eventbridge then using eventbridge rule we can take action according to those enents.
    
## S3 – Requester Pays
- In general, bucket owners pay for all Amazon S3 storage and data transfer costs associated with their bucket
- With Requester Pays buckets, the requester instead of the bucket owner pays the cost of the request and the data download from the bucket
- Helpful when you want to share large datasets with other accounts
- The requester must be authenticated in AWS (cannot be anonymous)
    
    
 ## Glacier Vault Lock 

- Adopt a WORM (Write Once Read Many) model
- Lock the policy for future edits (can no longer be changed)
- Helpful for compliance and data retention
- as an example we can create a vault lock policy which defines that object can not be deleted after that put a object there. Then the object will not deleted ever.

    
## S3 Object Lock (versioning must be enabled)
- Adopt a WORM (Write Once Read Many) model
- Block an object version deletion for a specified amount of time
- Object retention:
      - Retention Period: specifies a fixed period
      - Legal Hold: same protection, no expiry date
- Modes:
      - Governance mode: users can't overwrite or delete an object version or alter its lock settings unless they have special permissions
      - Compliance mode: a protected object version can't be overwritten or deleted by any user, including the root user in your AWS account. When an object is locked in compliance mode, its retention mode can't be changed, and its retention period can't be shortened.


---

- The S3 managed keys will be AES-256 (not AES-128) bit keys
- HTTPS is mandatory for SSE-C
- Encryption in flight is also called SSL / TLS
### What is S3 Select?
Amazon S3 Select is new feature that allows you to perform simple SQL operations against your raw data stored in S3. One of the requirements is that your data needs to be in a structured format, i.e. JSON, CSV, Parquet. Do note that it will also work on compressed version of files so you don’t need to decompress them before reading.
S3 Select is a completely serverless solution. You don’t provision any servers or databases to make this run. </br>
One of the big limits though is that S3 Select only supports the SELECT clause in SQL. That means no joins, no groupings, and no other sophisticated SQL operations. In your SELECT statement, only the following other clauses are supported: </br>
- FROM
- WHERE
- LIMIT
Also note that nested json fields can also be accessed, so if you have deeply nested objects you should still be good to go. </br>
The other, most important constraint of S3 SELECT is that you can only perform a query on one object at at time. This makes S3 select not a suitable option for many use cases requiring parsing of entire bucket paths or collections of objects. </br>
- Retrieve less data using SQL by performing server side filtering
- Can filter by rows & columns (simple SQL statements)
- Less network transfer, less CPU cost client-side

### S3 select vs athena 
S3 Select is a lightweight solution designed to let you use SQL to perform simple SELECT clauses on a maximum of one file. Amazon Athena is an analytics workhorse that allows you to perform SQL on extremely large datasets spanning many files with great performance.

### Amazon S3 Transfer Acceleration -
Amazon S3 Transfer Acceleration is a bucket-level feature that enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket. Transfer Acceleration is designed to optimize transfer speeds from across the world into S3 buckets.

### Differnece between Amazon S3 Transfer Acceleration and cloudformation
-  CloudFront is for content delivery (mainly download, upload also possible). S3 Transfer Acceleration is for faster transfers and higher throughput to S3 buckets (mainly uploads but download also possible ).
- Amazon S3 Transfer Acceleration is an S3 feature that accelerates uploads to S3 buckets using AWS Edge locations - the same Edge locations as in AWS CloudFront service.
- However, (a) creating a CloudFront distribution with an origin pointing to your S3 bucket and (b) enabling S3 Transfer acceleration for your bucket - are two different things serving two different purposes.
- When you create a CloudFront distribution with an origin pointing to your S3 bucket, you enable caching on Edge locations. Consequent requests to the same objects will be served from the Edge cache which is faster for the end user and also reduces the load on your origin. CloudFront is primarily used as a content delivery service.
- When you enable S3 Transfer Acceleration for your S3 bucket and use <bucket>.s3-accelerate.amazonaws.com instead of the default S3 endpoint, the transfers are performed via the same Edge locations, but the network path is optimized for long-distance large-object uploads. Extra resources and optimizations are used to achieve higher throughput. No caching on Edge locations.
  
## Access control -
### IAM policy for s3 -
It will be attached with user. The S3 Access IAM policy grants an IAM role the permission to access the specified S3 bucket. An IAM role requires a minimum level of permissions set in its policy in order for Aspera to upload, download, or list contents in an S3 buckets.

### Bucket policy -
It will be attached with bucket. A bucket policy is a resource-based AWS Identity and Access Management (IAM) policy. You add a bucket policy to a bucket to grant other AWS accounts or IAM users access permissions for the bucket and the objects in it. Object permissions apply only to the objects that the bucket owner creates.

### Amazon S3 access control lists (ACLs) -
Amazon S3 access control lists (ACLs) enable you to manage access to S3 buckets and objects. Every S3 bucket and object has an ACL attached to it as a subresource. The ACLs define which AWS accounts or groups are granted access along with the type of access.

### S3 bucket policy vs access control list (ACLs) - 
- Access Control Lists (ACLs) are legacy (but not deprecated). bucket/IAM policies are recommended by AWS.
- ACLs give control over buckets AND objects, bucket policies are only at the bucket level.
- If you want to implement fine grained control over individual objects in your bucket use ACLs. If you want to implement global control, such as making an entire bucket public, use policies.
- ACLs were the first authorization mechanism in S3. Bucket policies are the newer method, and the method used for almost all AWS services. Policies can implement very   complex rules and permissions, ACLs are simplistic (they have ALLOW but no DENY). To manage S3 you need a solid understanding of both.
### bucket policy vs iam policy which one takes the precedence? 

![alt text](https://github.com/arghya-roy/AWS_Certified_Solutions_Architect_Associate_notes/blob/main/Storage/S3/Screenshot%20(10)..png)

### User Security:
- MFA Delete: MFA (multi factor authentication) can be required in versioned
buckets to delete objects
- Pre-Signed URLs: URLs that are valid only for a limited time (ex: premium video
service for logged in users)
--
## A company has over 2000 users and is planning to migrate data into the AWS Cloud. Some of the data is user’s home folders on an existing file share and the plan is to move this data to Amazon S3. Each user will have a folder in a shared bucket under the folder structure: bucket/home/%username%. What steps should a Solutions Architect take to ensure that each user can access their own home folder and no one else’s? (choose 2)
### ANS -
Create an IAM policy that applies folder-level permissions and Create an IAM group and attach the IAM policy, add IAM users to the group.
## An application stores encrypted data in Amazon S3 buckets. A Solutions Architect needs to be able to query the encrypted data using SQL queries and write the encrypted results back the S3 bucket. As the data is sensitive fine-grained control ( Fine-grained access control is a method of controlling who can access certain data ) must be implemented over access to the S3 bucket. What combination of services represent the BEST options support these requirements? (choose 2)
### ANS -
- Use IAM policies to restrict access to the bucket.
- Use Athena for querying the data and writing the results back to the bucket

## An application will gather data from a website hosted on an EC2 instance and write the data to an S3 bucket. The application will use API calls to interact with the EC2 instance and S3 bucket. Which Amazon S3 access control method will be the MOST operationally efficient? (choose 2)
### ANS -
- Grant programmatic access.
- Create an IAM policy.

## A Solutions Architect would like to store a backup of an Amazon EBS volume on Amazon S3. What is the easiest way of achieving this?
### ANS -
- Create a snapshot of the volume. ( Snapshots capture a point-in-time state of an instance. Snapshots of Amazon EBS volumes are stored on S3 by design so you only need to take a snapshot and it will automatically be stored on Amazon S3. )
## A company has over 200 TB of log files in an Amazon S3 bucket. The company must process the files using a Linux-based software application that will extract and summarize data from the log files and store the output in a separate Amazon S3 bucket. The company needs to minimize data transfer charges associated with the processing of this data. How can a Solutions Architect meet these requirements?
### ANS -
- Launch an Amazon EC2 instance in the same Region as the S3 bucket. Process the log files and upload the output to another S3 bucket in the same Region.
- "Connect an AWS Lambda function to the S3 bucket via a VPC endpoint. Process the log files and store the output to another S3 bucket in the same Region" is incorrect. You cannot install a Linux-based software application on AWS Lambda. For lambda we can select runtime, we can not select operating system

## An Amazon S3 bucket is going to be used by a company to store sensitive data. A Solutions Architect needs to ensure that all objects uploaded to an Amazon S3 bucket are encrypted. How can this be achieved?
### ANS -
- Create a bucket policy that denies Put requests that do not have an **x-amz-server-side-encryption** header set.
- To encrypt an object at the time of upload, you need to add a header called x-amz-server-side-encryption to the request to tell S3 to encrypt the object using SSE-C, SSE-S3, or SSE-KMS.
- To enforce object encryption, create an S3 bucket policy that denies any S3 Put request that does not include the x-amz-server-side-encryption header. There are two possible values for the x-amz-server-side-encryption header: AES256, which tells S3 to use S3-managed keys, and aws:kms, which tells S3 to use AWS KMS–managed keys.
-  "Create a bucket policy that denies Put requests that do not have an **aws:Secure Transport header set to true**" is incorrect. This header is used for SSL/TLS.

## A customer has a public-facing web application hosted on a single Amazon Elastic Compute Cloud (EC2) instance serving videos directly from an Amazon S3 bucket. Which of the following will restrict third parties from directly accessing the video assets in the bucket?
### ANS -
- Use a bucket policy to only allow referrals from the main website URL.
- "Use a bucket policy to only allow the public IP address of the Amazon EC2 instance hosting the customer website" is incorrect. You can use condition statements in a bucket policy to restrict access via IP address. However, using the referrer condition in a bucket policy is preferable as it is a best practice to use DNS names / URLs instead of hard-coding IPs whenever possible.
- To allow read access to the S3 video assets from the public-facing web application, you can add a bucket policy that allows s3:GetObject permission with a condition, using the aws:referer key, that the get request must originate from specific webpages. This is a good answer as it fully satisfies the objective of ensuring the that EC2 instance can access the videos but direct access to the videos from other sources is prevented.

## A Solutions Architect works for a systems integrator running a platform that stores medical records. The government security policy mandates that patient data that contains personally identifiable information (PII) must be encrypted at all times, both at rest and in transit. Amazon S3 is used to back up data into the AWS cloud. How can the Solutions Architect ensure the medical records are properly secured? (choose 2)
- Enable Server Side Encryption with S3 managed keys on an S3 bucket using AES-256 and Before uploading the data to S3 over HTTPS, encrypt the data locally using your own encryption keys

