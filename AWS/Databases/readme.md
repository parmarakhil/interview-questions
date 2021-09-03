# Databases

1. Types
    1. RDBMS (SQL/OLTP)
        1. RDS, Aurora
        2. Great for joins, normalised data
    2. NoSQL 
        1. DynamoDB
        2. ElastiCache (key/value pairs)
        3. Neptune (graphs)
        4. No joins, No SQL to query
    3. Object Store
        1. S3 - big objects
        2. Glacier - for backups
    4. Data warehouse (SQL analytics/BI)
        1. Redshift - Online Analytical Processing OLAP
        2. Athena
    5. Search
        1. ElasticSearch
    6. Graphs
        1. Neptune
        2. Display relationships between data
2. RDS
    1. Managed PostgreSQL, MySQL, Oracle, SQL server
    2. Must provision an EC2 instance & EBS volume type and size
    3. Support read replica and Multi AZ
    4. Security through IAM, Security groups, KMS SSL in transit
    5. Backup, Snapshot, point in time restore
    6. Managed and scheduled infra
    7. Monitoring through cloud watch
    8. Use
        1. Store relational datasets
        2. Perform SQL queries
        3. Transactional insets
    9. Operations
        1. Small downtime when failover
        2. Scaling in read replicas/ Ec2 instances
        3. Restore EBS volumes implies manual intervention
        4. Application changes
    10. Security
        1. AWS responsible for OS security 
        2. We are responsible for setting up KMS, Security groups, IAM policies, authorising user in DB
    11. Reliability
        1. Multi AZ
        2. Failover in case of failure
    12. Performance
        1. Depends on EC2 instance type, EBS volume type 
        2. Storage auto-scaling & manual scaling
    13. Cost
        1. Pay per hour based on provisioned EC2 & EBS
3. Aurora
    1. Compatible with PosttgreSQL/ MYSQl
    2. Auto healing
    3. Data is stored in 6 replicas in 3 AZ
    4. Multi AZ, Auto scaling read replica
    5. Read replica can be globalDefine EC2 instance type for aurora instances
    6. Aurora serverless
        1. For unpredictable workloads
    7. Aurora Multi-master
        1. For continuous writes failover
    8. Operations
        1. Less operations
    9. Security
        1. AWS responsible for OS security 
        2. We are responsible for setting up KMS, Security groups, IAM policies, authorising user in DB
    10. Reliability
        1. Multi AZ, more than RDS
        2. Failover in case of failure
    11. Performance
        1. 5x performance
        2. Upto 15 read replica
    12. Cost
        1. Pay per hour based on EC2
        2. Amt of Storage
4. ElastiCache
    1. Managed Redis, memcached 
    2. In-memory data store
    3. Sub-millisecond latency
    4. Must provision EC2 instance type
    5. Support for Clustering
    6. Security through IAM,S security groups
    7. Backup, point in time restore
    8. Managed and scheduled maintenance
    9. Monitoring through cloud watch
    10. Uses
        1. Frequent reads, less write
        2. Key/value store
    11. Operation
        1. Same as RDS
    12. Security
        1. AWS responsible for OS security 
        2. We are responsible for setting up KMS, Security groups, IAM policies, users (Redis Auth)
    13. Reliability
        1. Multi AZ
    14. Performance
        1. Sub-millisecond performance
    15. Cost
        1. Pay per hour based on EC2 and storage usage
5. DynamoDB
    1. NoSQL, global Db
    2. Cloud native Was proprietary
    3. Serverless, provisioned capacity, on demand capacity
    4. Can replace elasticache as key/value store 
    5. Highly available, DAX for read cache
    6. Reads and writes are decoupled
    7. Reads can be eventually or strongly consistent
    8. Security , authentication and authorisation is done through IAM
    9. DynamoDB streams to integrate with lambda
        1. Global tables
    10. Backup/Restore
    11. Can only query on primary key, sort key or indexes
    12. Monitoring through cloud watch
    13. Use case
        1. Item size less than 100Kbs
        2. Distributed serverless cache
        3. Transactions capability
    14. Operations
        1. No operations needed
    15. Security
        1. Full security through IAM policies, KMS encryption,, SSL in-transit
    16. Reliability
        1. Multi AZ
        2. Failover in case of failure
    17. Performance
        1. Single digit milliseconds
        2. Can be used as cache, DAX
        3. Performance doesn’t degrade with inc in size
    18. Cost
