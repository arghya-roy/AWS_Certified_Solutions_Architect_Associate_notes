## Amazon GuardDuty
- It does not protect to from attacking, It notifies you after attack happended ( it come to know about attack by reading logs )
- Amazon GuardDuty is a threat detection service that continuously monitors your AWS accounts and workloads for malicious activity and delivers detailed security findings for visibility and remediation.

- Amazon GuardDuty is a threat detection service provided by Amazon Web Services (AWS). Threat detection is a cybersecurity practice that continuously monitors a system for malicious activities and generates alerts and security events. With GuardDuty, teams can monitor AWS resources and receive alerts and notifications around potential threats. Security teams respond to these notifications and take preventive actions to protect your infrastructure and AWS cloud resources. This article describes a set of best practices that will help you to develop a robust threat detection solution using GuardDuty.

- continuously monitors your AWS accounts and workloads for malicious activity and delivers detailed security findings for visibility and remediation.
- Intelligent Threat discovery to Protect AWS Account
- Uses Machine Learning algorithms, anomaly detection, 3rd party data
- One click to enable (30 days trial), no need to install software
- Input data includes:
    - CloudTrail Events Logs – unusual API calls, unauthorized deployments
         - CloudTrail Management Events – create VPC subnet, create trail, …
         - CloudTrail S3 Data Events – get object, list objects, delete object, …
    - VPC Flow Logs – unusual internal traffic, unusual IP address
    - DNS Logs – compromised EC2 instances sending encoded data within DNS queries
    - Kubernetes Audit Logs – suspicious activities and potential EKS cluster compromises
- Can setup CloudWatch Event rules to be notified in case of findings
- CloudWatch Events rules can target AWS Lambda or SNS
- Can protect against CryptoCurrency attacks (has a dedicated “finding” for it)

### How GuardDuty Works
- A threat detection service depends on logs and traces for monitoring a system. For GuardDuty, logs and events are provided by AWS CloudTrail, VPC Flow Logs, and DNS Logs. CloudTrail records all actions performed on your AWS resources either via CLI, GUI console, or the AWS API. VPC Flow Logs captures and records information about the IP traffic traversing through network interfaces. AWS Route 53 which is the DNS service from AWS, generates DNS Logs when your EC2 instances use Route 53 for name resolution.

- GuardDuty implements a complex internal ruleset to analyze these logs and traces to identify threats. As an AWS user, you do not need to be concerned about these internal rules as AWS fully takes care of that complexity. However, when relying on GuardDuty, your team must consider certain configuration and operational settings. We are going to discuss these considerations in the best practices below.

## Option in GuardDuty -
### Trusted IP List
A trusted IP list is a list of IP addresses or subnets you can define in GuardDuty so that GuardDuty does not generate findings for trusted IPs. This can be useful in a hybrid cloud architecture where your EC2 instances are frequently communicating with certain on-premise resources. You can trust these on-premise IP addresses, by defining a trusted IP list in GuardDuty. Creating a trusted IP list can help your team reduce some noise and false positives created in GuardDuty findings.

 ### Threat lists 
 Threat lists consist of known malicious IP addresses. GuardDuty generates findings for IP addresses that are included in threat lists.

### S3 Protection 
Monitor and generate findings on S3 data events ( CloudTrail S3 Data Events )

### Kubernetes Protection 
Monitor and generate findings from Kubernetes Audit Logs

### Malware Protection
Initiate a malware scan when GuardDuty generates a finding related to an EC2 instance or container workload that is indicative of malware.

### Accounts 
You can add organization account here to scan

### Findings
This page shows you all finding

### Usage
The GuardDuty usage page provides cost estimates to help you understand the projected cost of using the GuardDuty service.

### Malware scans
After using malware protection, you can the scan output here.
