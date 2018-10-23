Databases
----------

* What is a relational database
  * Relational databases are what most of us are used to. Similar to traditional spreadsheet: database, tables, row, fields (cols)
  * SQL Server
  * Oracle
  * MySQL server
  * PostgreSQL
  * Aurora
  * MariaDB
* Non Relational Databases
  * Datbase
    * Collection (Table)
    * Document (Row)
    * Key Value Pairs (Fields)
* What is Data Warehousing?
  * Used for business intelligence. Tools like Cognos, Jaspersoft, SQL Server Reporting Services, Oracle Hyperion, SAP NetWeaver
  * Used to pull in very large and complex data sets. Usually used by management to do queries on data (such as current performance vs targets etc)
* OLTP vs OLAP
  * Online Transaction Processing (OLTP) differs from OLAP Online Analytics Processing (OLAP) in terms of the types of queries you will run.
  * OLTP example
    * Order number 2120121
    * Pulls up a row of data such as Name, Date, Address to Deliver to, Delivery Status etc
  * OLAP transaction example:
    * Net profit for EMEA and Pacific for the Digital Radio Product.
    * Pulls in large numbers of records.
    * Sums of Radios sold in EMEA
    * Sums of Radios Sold in Pacific
    * Unit Cost of Radio in each region
    * Sales price of each radio
    * Sales price - unit cost
    * Data Warehousing datbases use differnt type of architecture both from a database  perspective and infrastructure layer.
* What is Elasticache
  * ElastiCache is a web service that makes it easy to deploy, operate, and scale in-memory cache in the cloud. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.

  * Elasticache supports two open-source in-memory caching engines:
    * Memcached
    * Redis
* AWS Database Types - Summary
  * RDS - OLTP
    * SQL
    * MySQL
    * PostrgreSQL
    * Oracle
    * Aurora
    * MariaDB
  * DynamoDB - No SQL
  * RedShift - OLAP
  * Elasticache - In Memory Caching
* RDS
  * Lab notes
    * You can open an RDS security group to _another_ security group. (e.g. open up RDS security group 3306 to inbound traffic from EC2 instance security group)
  * Automated backups
    * There are two different types of Backups for AWS: Automated Backups and Database Snapshots.
    * Automated Backups allow you to recover your database to any point in time within a "retention period". The retention period can be between one and 35 days. Automated Backups will take a full daily snapshot and will also store transaction logs throughout the day. When you do a recovery, AWS will first choose the most recent daily back up, and then apply transaction logs relevant to that day. This allows you to do a point in time recovery down to a second, within the retention period.
    * Automated backups are enabled by default. The backup data is stored in S3 and you get free storage space equal to the size of your database. So if you have an RDS instance of 10Gb, you will ge 10Gb worth of storage.
    * Backups are taken within a defined window. During the backup window, storage I/O may be suspended while your data is being backed up and you may experience elevated latency.
  * Snapshots
    * DB Snapshots are done manually (ie they are user initiaded.) They are stored even after you delete the original RDS instance, unlike automated backups.
  * Restoring backups
    * Whenever you restore either an Automatic Backup or a manual Snapshot, the restored version of the database will be a new RDS instance with a new DNS endpoint.
  * Encryption
    * Encryption at rest is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB & Aurora. Encryption is done using the AWS Key Management Service (KMS) service. Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas, and snapshots.
    * At the present time, encrpyting an existing Db Instance is not supported. To use Amazon RDS encryption for an existing database, you must first create a snapshot, make a copy of that snapshot and ecrypt a copy.
  * What is Multi-AZ
    * data synchronously replicated from one AZ to another
    * Multi-AZ allows you to have an exact copy of your production database in another Availability Zone. AWS handles the replication fro you, so when your production database is written to, this write will automatically be synchronized to the stand by database.
    * In the event of planned database maintenance, DB instance failure, or an Availability Zone failure, Amazon RDS will automatically failover to the standby so that database operations can resume quickly wihtout administrative intervention.
    * Multi-AZ is for Disaster recovery only - not for improving performance. For performance improvement, you need Read Replicas.
    * Multi-AZ available for
      * SQL Server
      * Oracle
      * MySQL server
      * PostgreSQL
      * MarioDB
      * (Aurora has this by default)
  * What is a Read Replica
    * 5 read replicas per prod database by default
    * Read replicas allow you to have a read-only copy of your production database. This is achieved by using Asynchronous replication from the primary RDS instance to the read replica. You use read replicas primarily for very read-heavy database workloads.
    * Read replicas are asynchronous, multi-az is syncronous
    * Read replicas available for
      * MySQL server
      * PostgreSQL
      * MariaDB
      * Aurora
      * (Not SQL server or Oracle)
    * Use for scaling, not for DR!
    * Must have automatic backups turned on in order to deploy a read replica.
    * You can have up to 5 read replica copies of any database.
    * You can have read replicas of read replicas (but watch out for latency.)
    * Each read replica will have it's own DNS end point.
    * You can have read replicas that have Multi-AZ
    * Read replicas can be promoted to be their own databases. This breaks replication.
    * You can have a read replica in a second region.
* DynamoDB
  * Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit ms latency at any scale. It is a fully managed database and supports both document and key-value data models. Its flexible data model and reliable performance make it a great fit for mobile, web, gaming, ad-tech, IoT, and many other applications.
  * Stored on SSD storage.
  * Spread Across 3 geographically distinct data centres.
  * Eventual Consistent Reads (Default)
    * Consistency across all ocpies of data is usually reached within a second. Repeating a read after a short time should return the updated data. (Best Read Performance)
  * Strongly Consistent Reads
    * A strongly consistent read returns a result that reflects all writes that received a successful reponse prior to the read.
  * DynamoDB pricing
    * Provisioned throughput capacity
      * Write throughput $0.0065 per hour for every 10 units
      * Read throughput $0.0065 per hour for every 50 units
    * Storage costs of $0.25GB per month
    * Example
      * Let's assume that your application needs to perform 1 million writes and 1 million reads per day, while storing 3GB of data.
      * First, you need to calculate how many writes and reads per second you need.
      * 1 million evently spread writes per day is equivalent to 1,000,000 (writes) / 24 (hours) / 60 (minutes) / 60 (seconds) = 11.6 writes per second
      * A DynamoDB write capacity unit can handle 1 write per second, so you need 12 Write Capacity units
      * Similarly, to handle 1 million strongly consistent reads per day, you need 12 Read Capacity Units.
      * With Read Capacity Units, you are billed in blocks of 50, with Write Capacity Units you are billed in blocks of 10.
      * To calculate Write Capacity Units = (0.0065/10) * 12 * 24 = $0.1872 / day
      * To calculate Read Capacity Units = (0.0065/50) * 12 * 24 = $0.0374 / day
    * Bottom line - somewhat expensive for writes, cheap for reads - scales well
* Redshift
  * Amazon Redshift is a fast and powerful, fully managed, petabyte-scale data warehouse service in the cloud. Customers can start small for just $0.25 per hour with no commitments or upfront costs and scale to a petabyte or more for $1,000 per terabyte per year, less than a tenth of most other data warehousing solutions.
  * OLAP transaction example
    * Net profit for EMEA and Pacific for the Digital Radio Product.
    * Pulls in large numbers of records
    * Sum of radios sold in EMEA
    * sum of radios sold in pacific
    * unit cost of radio in each region
    * sales price of each radio
    * sales price - unit cost
  * Data warehousing databases use different type of architecture both from a database perspective and infrastructure layer.
  * Redshift configuration
    * Single Node (160GB)
    * Multi-node
      * Leader Node (manages client connections and receives queries)
      * Compute Node (store data and perform queries and computations). Up to 128 Compute Nodes
    * Columnar Data Storage: Instead of storing data as a series of rows, Amazon Redshift organizes data by column. Unlike row-based systems, which are ideal for transaction processing, column-based systems are ideal for datawarehousing and analytics, wher equeries often involve aggregates performed over large data sets. Since only the columns involved in the queries are processes and columnar data is stored sequentially on the storage media, column-based systems require far fewer I/Os, greatly improving query performance.
    * Advanced Compression: Columnar data stores can be compressed much more than row-based data stores because similar data is stored sequentially on disk. Amazon Redshift employs multiple compression techniques and can often achieve significant compression relative to traditional relational data stores. In addition, Amazon Redshift doesn't require indexes or materialized views and so uses less space than traditional relational database systems. When loading data into an empty table, Amazon Redshift automatically samples your data and selects the most appropriate compression scheme.
    * Massively Parallel Processing (MPP): Amazon Redshift automatically distributes data and query load across all nodes. Amazon Redshift makes it easy to add nodes to your data warehouse and enables you to maintain fast query performance as your data warehouse grows.
    * Pricing
      * Compute Node Hours (total number of hours you run across all your compute nodes for the billing period. You are billed for 1 unit per node per hour, so a 3-node data warehouse cluster running persistently for an entire month would incur 2,160 instance hours. You will not be charged for elader node hours; only compute nodes will incur charges.)
      * backup
      * data transfer (only within a VPC, not outside it)
    * Security
      * Encrypted in transit using SSL
      * Encrypted at rest using AES-256 encryption
      * By default Redshift takes care of key management
        * You can manage your own keys through HSM
        * AWS Key Management Service
    * Availability
      * Currently only available in 1 AZ
      * Can restore snapshots to new AZ's in the event of an outage.
* Elasticache
  * ElastiCache is a web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud. The service improves the perofmance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.
  * Caching improves application performance by storing critical pieces of data in memory for low-latency access. Cached information may include the results of I/O-intensive database queries or the results of computationally-intensive calculations.
  * memcached
    * a widely adopted memory object caching system. ElastiCache is a protocol compliant with Memcached, so popular tools that you use today with existing Memcached environments will work seamlessly with the service.
  * Redis
    * popular open-source in-memory key-value store that supports data structures such as sorted sets and lists. ElastiCache supports Master/Slave replication and Multi-AZ which can be used to achieve cross AZ redundancy.
  * Exam tips
    * Typically you will be given a secnario where a particular database is under a lot of stress/load. You may be asked which service you should use to allerviate this.
    * Elasticache is a good choice if your database is particularly read heavy and not prone to frequent changing.
    * Redshift is a good answer if the reason your db is feeling stress is because management keep running OLAP transactions on it etc.
* Aurora
  * Amazon Aurora is a MySQL-compatible, relational database engine that combines the speed and availability of high-end commercial databases with the simplicity and cost-effectiveness of open source databases. Amazon Aurora provides up to five times better performance than MySQL at a price point one tenth that of a commercial database while delivering similar performance and availability.
  * Probably won't be on the exam yet...
  * Aurora Scaling
    * Start with 10GB, Scales in 10GB increments to 64TB (Storage autoscaling)
    * Compute resources can scale up to 32vCPUs and 244GB of Memory
      * during maintenance window... will be downtime
    * 2 copies of your data is contained in each availability zone, with minimum of 3 az's. 6 copies of your data.
    * Aurora is designed to transparently handle the loss of up to two copies of data without affecting db write availability and up to three copies without affecting read availability.
    * Aurora storage is also self-healing. Data blocks and disks are continuously scanned for errors and repaired automatically.
  * Aurora Replicas
    * 2 types of replicas are available
    * aurora replicas (currently 15)
      * failover will auto occur
    * mysql read replicas (currently 5)
      * failover will not auto occur
* Summary
  * Read RDS FAQ: https://aws.amazon.com/rds/faqs/ 
  * Quiz notes
    * When replicating data from primary RDS instance to secondary RDS instance there is no charge.
    * https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Storage.html#USER_PIOPS
    * For MySQL/Oracle provisioned IOPS max 16TB storage
    * When taking a snapshot I/O operations to the database are suspended for the duration of the snapshot.
      
  
   
