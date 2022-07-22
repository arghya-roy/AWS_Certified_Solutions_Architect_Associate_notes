- You can compare Amazon ES with apache solr.
- amazon elastic search is a managed opensearch.
- Amazon OpenSearch Service makes it easy for you to perform interactive log analytics, real-time application monitoring, website search, and more. 
- OpenSearch is an open source, distributed search and analytics suite derived from Elasticsearch. 
- Amazon OpenSearch Service is the successor to Amazon Elasticsearch Service, and offers the latest versions of OpenSearch, support for 19 versions 
of Elasticsearch (1.5 to 7.10 versions)
- You have visualization capabilities to check seaches powered by OpenSearch Dashboards and Kibana (1.5 to 7.10 versions). 
- Amazon OpenSearch Service currently has tens of thousands of active customers with hundreds of thousands of clusters under management processing hundreds of trillions of requests per month.
- As an example amazon / google search bar use amazon elastic search.
- amazon es operation is similer to rds.
- Amazon OpenSearch is successor to Amazon ElasticSearch
- Example: In DynamoDB, you can only find by primary key or indexes.
- With OpenSearch, you can search any field, even partially matches
- It’s common to use OpenSearch as a complement to another database
- OpenSearch also has some usage for Big Data applications
- You can provision a cluster of instances
- Built-in integrations: Amazon Kinesis Data Firehose, AWS IoT, and Amazon 
CloudWatch Logs for data ingestion
- Security through Cognito & IAM, KMS encryption, SSL & VPC
- Comes with OpenSearch Dashboards (visualization).


## OpenSearch for Solutions Architect - 
- Operations: similar to RDS
- Security: Cognito, IAM, VPC, KMS, SSL
- Reliability: Multi-AZ, clustering
- Performance: based on ElasticSearch project (open source), petabyte scale
- Cost: pay per node provisioned (similar to RDS)
- Remember: OpenSearch = Search / Indexin
## Configuration -
- create domain.
- create nodes cluster
- select vpc, az
- click on create
- upload json data through curl and api which you will get after click on create.
- will get a kibana url, using this you can search your key inside that json data
