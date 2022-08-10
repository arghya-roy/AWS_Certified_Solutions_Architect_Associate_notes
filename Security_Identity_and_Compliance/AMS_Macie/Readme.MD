### Amazon Macie
- Amazon Macie is a fully managed data security and data privacy service
that uses machine learning and pattern matching to discover and protect your sensitive data in AWS.
- Macie helps identify and alert you to sensitive data, such as personally identifiable information (PII)

### Example -
- You have a S3 bucket which stores user information (pdf). But users cannot put andhar number (inside pdf) there. If they put pdf with andhar number then macie will nofify you.
- To configure macie to scan, you have to create a reg expression which matches with andhar number patthen. Then have to attach it. After that whenever the pattern will match with some string inside pdf, it will notify you.
