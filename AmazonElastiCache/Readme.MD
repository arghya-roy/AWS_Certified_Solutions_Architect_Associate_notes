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
## Use cases -
### DB Cache -
- Applications queries ElastiCache, if not available, get from RDS and store in ElastiCache.
- Helps relieve load in RDS
- Cache must have an invalidation strategy to make sure only the most current data is used in there.
### User Session Store -
- User logs into any of the application
- The application writes the session data into ElastiCache
- The user hits another instance of our application
- The instance retrieves the data and the user is already logged in

## Patterns for ElastiCache
### Lazy Loading: all the read data is cached, data can become stale in cache
### Write Through: Adds or update data in the cache when written to a DB (no stale data)
### Session Store: store temporary session data in a cache (using TTL features)


## ElastiCache – Cache Security
### All caches in ElastiCache:
- Do not support IAM authentication
- IAM policies on ElastiCache are only used for AWS API-level security
### Redis AUTH
- You can set a “password/token” when you create a Redis cluster
- This is an extra level of security for your cache (on top of security groups)
- Support SSL in flight encryption
### Memcached
- Supports SASL-based authentication (advanced)

