- The same way RDS is to get managed Relational Databases.
- Also have to create a cluster which will give you a different endpoint. 
- Then inside your code you have to write a code which will at first check your query in elasticache, if not available then will search it inside cluster.
- elasticaches are in-memory databases with really high performance, low latency.
- Helps reduce load off of databases for read intensive workloads.
- Elasticache mainly works for read purposes.
- Helps make your application stateless.
- AWS takes care of OS maintenance / patching, optimizations, setup, configuration, monitoring, failure recovery and backups.
## There are two types of elasticcache -
### elasticache for redis -
- Multi AZ with Auto-Failover
- Read Replicas to scale reads and have high availability
- Data Durability using AOF persistence
- Backup and restore features
### elasticache for Memcached -
- Multi-node for partitioning of data (sharding)
- No high availability (replication)
- Non persistent
- No backup and restore
- Multi-threaded architecture
