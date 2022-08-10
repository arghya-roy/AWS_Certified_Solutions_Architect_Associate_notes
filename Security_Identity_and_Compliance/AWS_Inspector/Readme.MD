## Amazon Inspector
- Automated Security Assessments
- For EC2 instances
     - Leveraging the AWS System Manager (SSM) agent
     - Analyze against unintended network accessibility
     - Analyze the running OS against known vulnerabilities
- For Containers push to Amazon ECR
     - Assessment of containers as they are pushed
- Reporting & integration with AWS Security Hub
- Send findings to Amazon Event Bridge

## What does AWS Inspector evaluate?
- EC2, ECR Repository, ECR Image, AMI
- Continuous scanning of the infrastructure, only when needed
- Package vulnerabilities (EC2 & ECR) – database of CVE, Network reachability (EC2)
- A risk score is associated with all vulnerabilities for prioritization
