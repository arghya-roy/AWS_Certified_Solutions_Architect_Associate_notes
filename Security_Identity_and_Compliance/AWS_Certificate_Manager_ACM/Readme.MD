## AWS Certificate manager -
- Create, store, and renew SSL/TLS X.509 certificates
- Single domains, multiple domain names and wildcards
- Integrates with several AWS services including:
      - Elastic Load Balancing.
      - Amazon CloudFront.
      - AWS Elastic Beanstalk.
      - AWS Nitro Enclaves.
      - AWS CloudFormation.
- Public certificates are signed by the AWS public Certificate Authority.
- you can also create a Private CA with ACM.
- Can then issue private certificates.
- You can also import certificates from third-party issuers.

## What we can do using ACM?
- can request a public certificate ( used to access from internet )
- can request a private certificate ( used to access inside vpc or internally )
- Can import a certificate by giving certificate body, certificate private key, certificate chain.
