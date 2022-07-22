## Amazon EMR
- EMR stands for “Elastic MapReduce”
- Here you need to manage a cluster.
- EMR helps creating Hadoop clusters (Big Data) to analyze and process 
vast amount of data
- The clusters can be made of hundreds of EC2 instances
- Also supports Apache Spark, HBase, Presto, Flink.
- Easily run and scale Apache Spark, Hive, Presto, and other big data workloads.
- EMR takes care of all the provisioning and configuration
- Auto-scaling and integrated with Spot instances
- Use cases: data processing, machine learning, web indexing, big data.
- Run big data applications and petabyte-scale data analytics faster, and at less than half the cost of on-premises solutions.
- Build applications using the latest open-source frameworks, with options to run on customized Amazon EC2 clusters, Amazon EKS, AWS Outposts, or Amazon EMR Serverless.
- Get up to 2X faster time-to-insights with performance-optimized and open-source API-compatible versions of Spark, Hive, and Presto.
- Easily develop, visualize, and debug your applications using EMR Notebooks and familiar open-source tools in EMR Studio.
- Amazon EMR is a cloud big data platform for running large-scale distributed data processing jobs, interactive SQL queries, and machine learning (ML) applications using open-source analytics
frameworks such as Apache Spark, Apache Hive, and Presto.

## details -
- Apache Spark, Apache Hive, and Presto are data processing framework which are used to analysis big data like data petabytes of data from social media.
- Those framework runs on multiple instances.
- So here amazon EMR or amazon elastic mapreduce used to manage clusrer of those data processing framework. Also it has Auto-scaling feature and integrated with Spot instances.
- Using amazon EMR you can run those instances on Amazon EC2 clusters, Amazon EKS, AWS Outposts, or Amazon EMR Serverless.
- You will have one EMR master node which manages other nodes (core nodes)
- You can pick data as a source from s3, kinesis, dynamodb etc.
- Go to EMR and click on create cluser then you get a option for data processing framework - Hadoop, Hbase, presto, spark. You can select any of them then that will be installed on your cluster automatically. As an exanple you choose spark.
- Inside hardware section you can select instance type and auto scaling config as per your workload.
- download key pair to do ssh to your master node.
- in your visual studio write a script for big data analysis ( as an example you write a script which will pick a csv file from s3 then select some raw as per **where query** then made a another csv and put that inside another bucket ). 
- Then ssh to master node and run `spark submit demo.py`

## use cases -
### Perform big data analytics - 
Run large-scale data processing and what-if analysis using statistical algorithms and predictive models to uncover hidden patterns, correlations, market trends, and customer preferences.

### Build scalable data pipelines -
Extract data from a variety of sources, process it at scale, and make it available for applications and users.

### Process real-time data streams -
Analyze events from streaming data sources in real-time to create long-running, highly available, and fault-tolerant streaming data pipelines.

### Accelerate data science and ML adoption -
Analyze data using open-source ML frameworks such as Apache Spark MLlib, TensorFlow, and Apache MXNet. Connect to Amazon SageMaker Studio for large-scale model training, analysis, and reporting.

---
## Amazon EMR Serverless -
Amazon EMR Serverless is a new option in Amazon EMR that makes it easy and cost-effective for data engineers and analysts to run applications built using open source big data frameworks such as Apache Spark, Hive or Presto, without having to tune, operate, optimize, secure or manage clusters.
