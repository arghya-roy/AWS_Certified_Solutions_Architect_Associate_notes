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

## AWS Inspector vs GuardDuty

- Guardduty protects your aws account against treat but Inspector give you best security practices about ec2, repository
- Amazon Inspector provides you with security assessments of your applications’ settings and configurations while Amazon GuardDuty helps with analysing the entirety of your AWS accounts for potential threats.
- you can have Inspector set up at the start when you deploy your applications, and then GuardDuty immediately after that in order to receive alerts on potential threats.
- For Inspector, it’s worth noting that when we speak of ‘applications’ it only covers EC2 at the moment. There is an agent that you can install in order to have it assess a wider set of configurations. For Inspector, the assessments are done based on ‘rules’ that help you to identify whether you are adhering to security best practices.
- Guadrduty works only in ec2 level but inspector works on application level which is configured inside ec2
