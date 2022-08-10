### AWS Secrets Manager
- Newer service, meant for storing secrets
- Capability to force rotation of secrets every X days
- Automate generation of secrets on rotation (uses Lambda)
- Integration with Amazon RDS (MySQL, PostgreSQL, Aurora)
- Secrets are encrypted using KMS
- Mostly meant for RDS integration

### AWS Secrets Manager vs Systems Manager Parameter Store
- AWS Secrets Manager can store value upto 64kb, Parameter store can store value upto 4kb or 8kb
- Values can be encrypted with KMS for both.
- Can be referenced in CloudFormation for both.
- Secret manager can generate new password but parameter store can not generate.
- Secret manager can do automated secret rotation but parameter store can not do that.
- Cross-account access is available for secret manager but that is unavailable for parameter store.
- Secret manager has additional cost but paramter store Free for standard parameters. Advanced parameters are charged per parameter and API transaction
