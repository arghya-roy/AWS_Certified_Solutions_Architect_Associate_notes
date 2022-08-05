- The same way RDS is to get managed Relational Databases.
- Also have to create a cluster which will give you a different endpoint. 
- Then inside your code you have to write a code which will at first check your query in elasticache, if not available then will search it inside cluster.
- elasticaches are in-memory databases with really high performance, low latency.
- Helps reduce load off of databases for read intensive workloads.
- Elasticache mainly works for read purposes.
- Helps make your application stateless.
- We can use s3 as a backend of elasticache.
- AWS takes care of OS maintenance / patching, optimizations, setup, configuration, monitoring, failure recovery and backups.
## There are two types of elasticcache -
### elasticache for redis -
- Multi AZ with Auto-Failover
- auto failover is optional for Redis (cluster mode disabled) and required for Redis (cluster mode enabled)
- Read Replicas to scale reads and have high availability
- Data Durability using AOF persistence
- Backup and restore features
- single threaded architecture
- **Cluster mode disabled** - Disabled The Redis cluster will have a single shard (node group) with one primary node and up to 5 read replica.
- **Cluster mode enabled** - Cluster mode enables replication across multiple shards for enhanced scalability and availability.




### elasticache for Memcached -
- Multi-node for partitioning of data (sharding)
- Can spread nodes acress multiple az.
- No auto failover.
- No high availability (replication)
- Non persistent
- No backup and restore
- Multi-threaded architecture
### For more https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/SelectEngine.html
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
### Lazy Loading: 
all the read data is cached, data can become stale in cache
### Write Through:
Adds or update data in the cache when written to a DB (no stale data)
### Session Store: 
store temporary session data in a cache (using TTL features)


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

## ElastiCache in-transit encryption implements the following features:

- Encrypted connections — both the server and client connections are Secure Socket Layer (SSL) encrypted.

- Encrypted replication — data moving between a primary node and replica nodes is encrypted.

- Server authentication — clients can authenticate that they are connecting to the right server.

- Client authentication — using the Redis AUTH feature, the server can authenticate the clients.

--
## A company is deploying an Amazon ElastiCache for Redis cluster. To enhance security a password should be required to access the database. What should the solutions architect use?
### ANS -
- Redis AUTH command.
- Redis authentication tokens enable Redis to require a token (password) before allowing clients to execute commands, thereby improving data security. You can require that users enter a token on a token-protected Redis server. To do this, include the parameter --auth-token (API: AuthToken) with the correct token when you create your replication group or cluster. Also include it in all subsequent commands to the replication group or cluster.

## An Amazon ElastiCache for Redis cluster runs across multiple Availability Zones. A solutions architect is concerned about the security of sensitive data as it is replicated between nodes. How can the solutions architect protect the sensitive data?
### ANS -
- When it staes that while replication, it means w have to enable encrypt in transit.
## A company runs a streaming media service and the content is stored on Amazon S3. The media catalog server pulls updated content from S3 and can issue over 1 million read operations per second for short periods. Latency must be kept under 5ms for these updates. Which solution will provide the BEST performance for the media catalog updates?
### ANS - 
- Update the application code to use an Amazon ElastiCache for Redis cluster
- Some applications, such as media catalog updates require high frequency reads, and consistent throughput. For such applications, customers often complement S3 with an in-memory cache, such as Amazon ElastiCache for Redis, to reduce the S3 retrieval cost and to improve performance.
- "Implement Amazon CloudFront and cache the content at Edge Locations" is incorrect. CloudFront is good for getting media closer to users but in this case we’re trying to improve performance within the data center moving data from S3 to the media catalog server.

